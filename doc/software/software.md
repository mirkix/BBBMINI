# Software

How to prepare your BeagleBone Black to use as BBBMINI.

* Debian 8.2 jessie
* GCC 4.9
* Kernel 4.1 PREEMPT RT
* Devicetree for the BBBMINI is already loaded at startup.

## Prepare microSD with your host computer
1. Download Debian image [https://rcn-ee.com/rootfs/bb.org/testing/2015-11-29/console/BBB-eMMC-flasher-debian-8.2-console-armhf-2015-11-29-2gb.img.xz](https://rcn-ee.com/rootfs/bb.org/testing/2015-11-29/console/BBB-eMMC-flasher-debian-8.2-console-armhf-2015-11-29-2gb.img.xz)
2. Decompress image: `unxz BBB-eMMC-flasher-debian-8.2-console-armhf-2015-11-29-2gb.img.xz`
3. Copy image to microSDcard (>= 4GB): `sudo dd bs=4M if=./BBB-eMMC-flasher-debian-8.2-console-armhf-2015-11-29-2gb.img of=/dev/sdX` /dev/sdX should point to your microSD, be careful here!!! Use `lsblk` to figure out, which is your mircroSD.
The process can take 15-30 minutes depending on the speed of your microSD card.
4. `sync` and remove mircroSD 

## Install Debian to your BeagleBone Black eMMC
1. Plug prepared microSD into BBB
2. While holding down the boot button, apply power to the board. If there is a newer Debian installed, holding down the boot button is not necessary.
3. Wait some minutes until Debian is installed (all four LEDs turned on).
4. Remove power.
5. Remove microSD.
6. Apply power again.
7. Connect to the BBB `ssh debian@beaglebone`
8. Password `temppwd`
9. Update software: `sudo apt-get update`
10. Update software: `sudo apt-get upgrade`
11. Install software: `sudo apt-get install cpufrequtils g++ gawk git make ti-pru-cgt-installer device-tree-compiler screen -y`
12. Install RT Kernel: `sudo /opt/scripts/tools/update_kernel.sh --bone-rt-kernel --lts`
13. Add BBBMINI DTB: `sudo sed -i 's/#dtb=$/dtb=am335x-boneblack-bbbmini.dtb/' /boot/uEnv.txt`
14. Adjusting the BBB clock `sudo sed -i 's/GOVERNOR="ondemand"/GOVERNOR="performance"/g' /etc/init.d/cpufrequtils`
15. Reboot system: `sudo reboot`
16. Login again: `ssh debian@beaglebone`
17. Get Ardupilot code: `git clone https://github.com/diydrones/ardupilot.git`
18. Change dir: `cd ardupilot/Tools/Linux_HAL_Essentials/pru/rangefinderpru`
19. Build Rangefinder firmware: `make`
20. Install Rangefinder firmware: `sudo make install`
21. Your BeagleBone Black is now ready to use.

## Compile ArduPilot natively on the BBB
`cd ardupilot/ArduCopter` for ArduCopter

or

`cd ardupilot/ArduPlane` for ArduPlane

or 

`cd ardupilot/APMrover2` for APMRover

then

`make bbbmini`

## Cross compile ArduPilot 

To compile ArduPilot for the BBB on a Ubuntu computer the following packages are required:

`sudo apt-get install git gawk g++-arm-linux-gnueabihf`

Now get the source code:

`git clone https://github.com/diydrones/ardupilot.git`

choose what to build:

`cd ardupilot/ArduCopter` for ArduCopter

or

`cd ardupilot/ArduPlane` for ArduPlane

or 

`cd ardupilot/APMrover2` for APMRover

then

`make bbbmini`

use `scp` to copy the .ELF executable to the BBB.

## Run ArduPilot
Now you can check your hardware [here.](../checkhardware/checkhardware.md)

then you can start ArduPilot:

`sudo ardupilot/ArduCopter/ArduCopter.elf`

or

`sudo ardupilot/ArduPlane/ArduPlane.elf`

or

`sudo ardupilot/APMrover2/APMrover2.elf`

To connect a MAVLink groundstation add `-A udp:192.168.178.26:14550`

To use MAVLink via radio connected to UART4 add `-C /dev/ttyO4`. 

If there is a GPS connected to UART5 add `-B /dev/ttyO5`. 

Example: MAVLink groundstation with IP 192.168.178.26 on port 14550 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -A udp:192.168.178.26:14550 -B /dev/ttyO5`

Example: MAVLink groundstation via radio connected to UART4 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -B /dev/ttyO5 -C /dev/ttyO4`

