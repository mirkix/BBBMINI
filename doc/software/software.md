# Software

How to prepare your BeagleBone Black to use as BBBMINI.

* Debian 8.3 jessie
* GCC 4.9
* Kernel 4.1 PREEMPT RT
* Devicetree for the BBBMINI is already loaded at startup.

## Prepare microSD with your host computer
1. Download Debian image [https://rcn-ee.com/rootfs/bb.org/testing/2016-01-31/console/BBB-eMMC-flasher-debian-8.3-console-armhf-2016-01-31-2gb.img.xz](https://rcn-ee.com/rootfs/bb.org/testing/2016-01-31/console/BBB-eMMC-flasher-debian-8.3-console-armhf-2016-01-31-2gb.img.xz)
2. Decompress image: `unxz BBB-eMMC-flasher-debian-8.3-console-armhf-2016-01-31-2gb.img.xz`
3. Copy image to microSDcard (>= 4GB): `sudo dd bs=4M if=./BBB-eMMC-flasher-debian-8.3-console-armhf-2016-01-31-2gb.img of=/dev/sdX` /dev/sdX should point to your microSD, be careful here!!! Use `lsblk` to figure out, which is your mircroSD.
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
9. Update software: `sudo apt-get update && sudo apt-get upgrade -y`
10. Install software: `sudo apt-get install -y cpufrequtils g++ gawk git make ti-pru-cgt-installer device-tree-compiler screen python`
11. Update scripts: `cd /opt/scripts && sudo git pull`
12. Install RT Kernel: `sudo /opt/scripts/tools/update_kernel.sh --bone-rt-kernel --lts-4_1`
13. Add BBBMINI DTB: `sudo sed -i 's/#dtb=$/dtb=am335x-boneblack-bbbmini.dtb/' /boot/uEnv.txt`
14. Adjusting the BBB clock `sudo sed -i 's/GOVERNOR="ondemand"/GOVERNOR="performance"/g' /etc/init.d/cpufrequtils`
15. Reboot system: `sudo reboot`
16. Login again: `ssh debian@beaglebone`
17. Clone overlays: `git clone https://github.com/beagleboard/bb.org-overlays`
18. Change dir: `cd ./bb.org-overlays`
19. Update DTC: `./dtc-overlay.sh`
20. Build and install overlays: `./install.sh`
21. Add ADC DTBO: `sudo sed -i 's/#cape_enable=bone_capemgr.enable_partno=/cape_enable=bone_capemgr.enable_partno=BB-ADC/g' /boot/uEnv.txt`
22. Reboot system: `sudo reboot`
23. Login again: `ssh debian@beaglebone`
24. Clone ArduPilot code: `git clone https://github.com/diydrones/ardupilot.git`
25. Init submodule: `git submodule init`
26. Clone submodule: `git submodule update`
27. Change dir: `cd ardupilot/Tools/Linux_HAL_Essentials/pru/rangefinderpru`
28. Build Rangefinder firmware: `make`
29. Install Rangefinder firmware: `sudo make install`
30. Your BeagleBone is now ready to use.

## Compile ArduPilot native on BeagleBone
1. `cd ardupilot`
2. `alias waf="$PWD/modules/waf/waf-light"`
3. `waf configure --board=bbbmini`
4. `waf` (take about 1h20m)

ArduCopter:

1. `cd build/bbbmini/bin`
2. `sudo ./arducopter` (plus parameter) 

ArduPlane:

1. `cd build/bbbmini/bin`
2. `sudo ./arduplane` (plus parameter) 

ArduRover:

1. `cd build/bbbmini/bin`
2. `sudo ./ardurover` (plus parameter) 

## Cross compile ArduPilot 

To compile ArduPilot for BeagleBone on a Ubuntu computer the following packages are required:

`sudo apt-get install git gawk g++-arm-linux-gnueabihf`

Get the source code:

1. `git clone https://github.com/diydrones/ardupilot.git`
2. `cd ardupilot`
3. `git submodule init`
4. `git submodule update`
5. `alias waf="$PWD/modules/waf/waf-light"`
6. `waf configure --board=bbbmini`
7. `waf -j8`
8. `cd build/bbbmini/bin`

use `scp` to copy the executable to the BeagleBone.

## Run ArduPilot
Now you can check your hardware [here.](../checkhardware/checkhardware.md)

then you can start ArduPilot:

`sudo ardupilot/ArduCopter/ArduCopter.elf`

or

`sudo ardupilot/ArduPlane/ArduPlane.elf`

or

`sudo ardupilot/APMrover2/APMrover2.elf`

To connect a MAVLink groundstation add `-C udp:192.168.178.26:14550`

To use MAVLink via radio connected to UART4 add `-C /dev/ttyO4`. 

If there is a GPS connected to UART5 add `-B /dev/ttyO5`. 

Example: MAVLink groundstation with IP 192.168.178.26 on port 14550 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -C udp:192.168.178.26:14550 -B /dev/ttyO5`

Example: MAVLink groundstation via radio connected to UART4 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -B /dev/ttyO5 -C /dev/ttyO4`

