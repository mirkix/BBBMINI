# Software

How to prepare your BeagleBone Black to use as BBBmini.

* Debian 8.5 jessie
* GCC 4.9
* Kernel 4.4 PREEMPT RT
* BBBmini devicetree loaded at startup.

## Prepare microSD with your host computer
1. Download Debian image [https://rcn-ee.com/rootfs/bb.org/testing/2016-07-04/console/BBB-blank-debian-8.5-console-armhf-2016-07-04-2gb.img.xz](https://rcn-ee.com/rootfs/bb.org/testing/2016-07-04/console/BBB-blank-debian-8.5-console-armhf-2016-07-04-2gb.img.xz)
2. Decompress image: `unxz BBB-blank-debian-8.5-console-armhf-2016-07-04-2gb.img.xz`
3. Copy image to microSDcard (>= 2GB): `sudo dd bs=4M if=./BBB-blank-debian-8.5-console-armhf-2016-07-04-2gb.img of=/dev/sdX` /dev/sdX should point to your microSD, be careful here!!! Use `lsblk` to figure out, which is your mircroSD.
The process can take 15-30 minutes depending on the speed of your microSD card.
4. `sync` and remove mircroSD 

## Install Debian to your BeagleBone eMMC
1. Plug prepared microSD into BeagleBone
2. While holding down the boot button, apply power to the board. If there is a newer Debian installed, holding down the boot button is not necessary.
3. Wait some minutes until Debian is installed (all four LEDs turned on).
4. Remove power.
5. Remove microSD.
6. Apply power again.
7. Connect to the BeagleBone `ssh debian@beaglebone`
8. Password `temppwd`
9. Update software: `sudo apt update && sudo apt upgrade -y`
10. Install software: `sudo apt install -y cpufrequtils g++ gawk git make device-tree-compiler screen python`
11. Update scripts: `cd /opt/scripts && sudo git pull`
12. Expend partiion: `sudo /opt/scripts/tools/grow_partition.sh`
13. Install RT Kernel: `sudo /opt/scripts/tools/update_kernel.sh --bone-rt-kernel --lts-4_4`
14. Add BBBMINI DTB: `sudo sed -i 's/#dtb=$/dtb=am335x-boneblack-bbbmini.dtb/' /boot/uEnv.txt`
15. Adjusting the BBB clock `sudo sed -i 's/GOVERNOR="ondemand"/GOVERNOR="performance"/g' /etc/init.d/cpufrequtils`
16. Reboot system: `sudo reboot`
17. Login again: `ssh debian@beaglebone`
18. Clone overlays: `git clone https://github.com/beagleboard/bb.org-overlays`
19. Build and install overlays: `cd ./bb.org-overlays && ./install.sh`
20. Add ADC DTBO: `sudo sed -i 's/#cape_enable=bone_capemgr.enable_partno=/cape_enable=bone_capemgr.enable_partno=BB-ADC/g' /boot/uEnv.txt`
21. Reboot system: `sudo reboot`
22. Login again: `ssh debian@beaglebone`
23. Clone ArduPilot code: `git clone https://github.com/ArduPilot/ardupilot.git`
24. Change dir: `cd ardupilot/Tools/Linux_HAL_Essentials/pru/rangefinderpru`
25. Install Rangefinder firmware: `sudo make install`
26. Your BeagleBone is now ready to use.

## Compile ArduPilot native on BeagleBone
1. `cd ardupilot`
2. `git checkout Copter-3.4` for ArduCopter or `git checkout ArduPlane-3.6.0` for ArduPlane
3. `git submodule update --init --recursive`
4. `alias waf="$PWD/modules/waf/waf-light"`
5. `waf configure --board=bbbmini`
6. `waf` (take about 1h20m)
7. `cp build/bbbmini/bin/* /home/debian/`

## Cross compile ArduPilot (faster) with Ubuntu computer

Get the source code:

1. `git clone https://github.com/diydrones/ardupilot.git`
2. `cd ardupilot`
3. `./Tools/scripts/install-prereqs-ubuntu.sh`
4. `git checkout Copter-3.4` for ArduCopter or `git checkout ArduPlane-3.6.0` for ArduPlane
5. `git submodule update --init --recursive`
6. `alias waf="$PWD/modules/waf/waf-light"`
7. `waf configure --board=bbbmini`
8. `waf`
9. `scp build/bbbmini/bin/* debian@beaglebone:/home/debian/`

## Run ArduPilot
Now you can check your hardware [here.](../checkhardware/checkhardware.md)

ArduCopter:

1. `sudo /home/debian/arducopter-quad` (plus parameter) 

ArduPlane:

1. `sudo /home/debian/arduplane` (plus parameter) 

ArduRover:

1. `sudo /home/debian/ardurover` (plus parameter) 

To connect a MAVLink groundstation with IÜ 192.168.178.26 add `-C udp:192.168.178.26:14550`

To use MAVLink via radio connected to UART4 add `-C /dev/ttyO4`. 

If there is a GPS connected to UART5 add `-B /dev/ttyO5`. 

Example: MAVLink groundstation with IP 192.168.178.26 on port 14550 and GPS connected to `/dev/ttyO5` UART5.

`sudo /home/debian/arducopter-quad -C udp:192.168.178.26:14550 -B /dev/ttyO5`

Example: MAVLink groundstation via radio connected to UART4 and GPS connected to `/dev/ttyO5` UART5.

`sudo /home/debian/arducopter-quad -B /dev/ttyO5 -C /dev/ttyO4`
