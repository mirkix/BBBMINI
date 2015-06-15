# Software

There is now a prebuild image which make things easier.

The image includes:
* Debian 8 jessie
* GCC 4.9
* Kernel 4.0.4 PREEMPT RT
* Devicetree for the BBBMINI is already loaded at startup.

## Prepare BBB
1. Download Debian image with BBBMINI support here: [bone-debian-8.0-console-bbbmini-armhf-2015-05-08-2gb.img.xz](https://goo.gl/jmjDcO)

2. Decompress image: `unxz bone-debian-8.0-console-bbbmini-armhf-2015-05-08-2gb.img.xz`

3. Copy image to microSDcard (>= 4GB): `sudo dd if=./bone-debian-8.0-console-bbbmini-armhf-2015-05-08-2gb.img of=/dev/sdX` /dev/sdX should point to your microSDcard, be careful here!!! Use `lsblk` to figure out, which is your mircroSDcard.

4. `sync` and remove mircroSDcard 

5. Put microSDcard into BBB
6. Connect BBB to power
7. Connect to the BBB `ssh debian@arm`
8. Password `temppwd`
9. Install software: `sudo apt-get update && sudo apt-get install gawk make g++`
10. Uninstall Apache2: `sudo apt-get remove apache2`
11. Get Ardupilot code: `git clone https://github.com/diydrones/ardupilot.git`
12. Grow partition to mircroSDcard size: `sudo /opt/scripts/tools/grow_partition.sh`
13. Reboot: `sudo reboot`
 
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

`sudo ardupilot/ArduPlan/ArduPlan.elf`

or

`sudo ardupilot/APMrover2/APMrover2.elf`

To connect a MAVLink groundstation add `-A udp:192.168.178.26:14550`

To use MAVLink via radio connected to UART4 add `-C /dev/ttyO4`. 

If there is a GPS connected to UART5 add `-B /dev/ttyO5`. 

Example: MAVLink groundstation with IP 192.168.178.26 on port 14550 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -A udp:192.168.178.26:14550 -B /dev/ttyO5`

Example: MAVLink groundstation via radio connected to UART4 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -B /dev/ttyO5 -C /dev/ttyO4`

