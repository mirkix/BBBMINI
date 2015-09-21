# Software

There is now a prebuild image which make things easier.

The image includes:
* Debian 8.1 jessie
* GCC 4.9
* Kernel 4.0.8 PREEMPT RT
* Devicetree for the BBBMINI is already loaded at startup.

## Prepare BBB
1. Download Debian image here: [bone-debian-8.2-console-armhf-2015-09-11-2gb.img.xz](https://rcn-ee.com/rootfs/2015-09-11/microsd/bone-debian-8.2-console-armhf-2015-09-11-2gb.img.xz)
2. Decompress image: `unxz one-debian-8.1-console-armhf-2015-06-11-2gb.img.xz`
3. Copy image to microSDcard (>= 4GB): `sudo dd if=./one-debian-8.1-console-armhf-2015-06-11-2gb.img of=/dev/sdX` /dev/sdX should point to your microSDcard, be careful here!!! Use `lsblk` to figure out, which is your mircroSDcard.
4. `sync` and remove mircroSDcard 
5. Put microSDcard into BBB
6. Connect BBB to power
7. Connect to the BBB `ssh debian@arm`
8. Password `temppwd`
9. Update software: `sudo apt-get update`
10. Update software: `sudo apt-get upgrade`
11. Install Kernel: `sudo apt-get install linux-image-4.0.8-bone-rt-r8 linux-firmware-image-4.0.8-bone-rt-r8`
12. Add BBBMINI DTB: `sudo sed -i 's/#dtb=$/dtb=am335x-boneblack-bbbmini.dtb/' /boot/uEnv.txt`
13. Install software: `sudo apt-get install g++ gawk git make ti-pru-cgt-installer device-tree-compiler`
14. Uninstall Apache2: `sudo apt-get remove apache2`
15. Reboot system: `sudo reboot`
16. Login again
17. Get latest Device Tree files: `git clone https://github.com/RobertCNelson/dtb-rebuilder.git`
18. Change dir: `cd dtb-rebuilder`
19. Choose branch: `git checkout 4.0.x`
20. Make clean: `make clean`
21. Build Device Tree files: `make`
22. Install Device Tree files: `sudo make install`
23. Change to home dir: `cd`
24. Get Ardupilot code: `git clone https://github.com/diydrones/ardupilot.git`
25. Change dir: `cd ardupilot/Tools/Linux_HAL_Essentials/pru/rangefinderpru`
26. Build Rangefinder firmware: `make`
27. Install Rangefinder firmware: `sudo make install`

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

