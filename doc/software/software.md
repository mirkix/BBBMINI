# Software
To start here, Debian should already be installed on your BBB.

## Get required software on the BBB
###Tools
`apt-get install git make gawk g++ arduino-core`

### ArduPilot sourcecode 
`git clone git://github.com/diydrones/ardupilot.git`

## BBB configuration 

###Disable HDMI
HDMI output should be disabled. Edit `/boot/uEnv.txt` and add `capemgr.disable_partno=BB-BONELT-HDMI,BB-BONELT-HDMIN` to `optargs` argument.

### `/boot/uEnv.txt` `optargs`example
`optargs=fixrtc quiet capemgr.disable_partno=BB-BONELT-HDMI,BB-BONELT-HDMIN`

## Install device tree overlay
You have to install the device tree overlay once.

`sudo ardupilot/Tools/Linux_HAL_Essentials/devicetree/bbbmini/make install`

## Compile ArduPilot natively on the BBB
`cd ardupilot/ArduCopter` for ArduCopter

or

`cd ardupilot/ArduPlane` for ArduPlane

or 

`cd ardupilot/APMrover2` for APMRover

then

`make configure`

`make bbbmini`

At the moment is it not possible to compile ArduPilot natively on the BBB, because the compiler `gcc` 4.6 and `gcc` 4.7 crash when compiling the file `AP_InertialSensor.cpp` ([ APM for Linux does not compile natively #1986 ](https://github.com/diydrones/ardupilot/issues/1986)). As a workaround compile ArduPilot with a Ubuntu computer, see Cross compile ArduPilot for further instructions.

## Cross compile ArduPilot 

To compile ArduPilot for the BBB on a Ubuntu computer the following packages are required:

`sudo apt.get install git gawk g++-arm-linux-gnueabihf`

Now get the source code:

`git clone https://github.com/diydrones/ardupilot.git`

choose what to build:

`cd ardupilot/ArduCopter` for ArduCopter

or

`cd ardupilot/ArduPlane` for ArduPlane

or 

`cd ardupilot/APMrover2` for APMRover

then

`make configure`

`make bbbmini`

use `scp` to copy the .ELF executable to the BBB.

## Run ArduPilot
Before you can start ArduPilot you have to enable the hardware (load device tree overlay) once after (re)boot:

`sudo ardupilot/Tools/Linux_HAL_Essentials/devicetree/bbbmini/startup.sh load`

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

