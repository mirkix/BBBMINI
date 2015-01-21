# Software
To start here, Debian should be allready installed on your BBB.

## Get required software on the BBB
###Tools
`apt-get install git make gawk g++ arduino-core`

### ArduPilot sourcecode 
`git clone git://github.com/diydrones/ardupilot.git`

## BBB configuration 

###Disable HDMI
HDMI output should be disabled. Edit `/boot/uEnv.txt` and add `capemgr.disable_partno=BB-BONELT-HDMI,BB-BONELT-HDMIN` to `optargs` argument.

###Enable UART5
UART5 is disabeld by default. To enable UART5 at startup we can edit `/boot/uEnv.txt`. Add `capemgr.enable_partno=BB-UART5` to the optargs argument.

### `/boot/uEnv.txt` `optargs`example
`optargs=fixrtc quiet capemgr.disable_partno=BB-BONELT-HDMI,BB-BONELT-HDMIN capemgr.enable_partno=BB-UART5 `

## Compile ArduPilot
`cd ardupilot/ArduCopter`

or

`cd ardupilot/ArduPlane`

or 

`cd ardupilot/APMrover2`

then

`make configure`

`make bbbmini`

## Run ArduPilot
Before you can start ArduPilot you have to enable the hardware once after startup:

`sudo ardupilot/Tools/Linux_HAL_Essentials/startup.sh load`

Now you can check your hardware [here.](../checkhardware/checkhardware.md)

then you can start ArduPilot:

`sudo ardupilot/ArduCopter/ArduCopter.elf`

or

`sudo ardupilot/ArduPlan/ArduPlan.elf`

or

`sudo ardupilot/APMrover2/APMrover2.elf`

To connect a MAVLINK groundstation add `-A udp:192.168.178.26:14550`

If there is a GPS connected to UART5 add `-B /dev/ttyO5`. 

Example: MAVLINK groundstation with IP 192.168.178.26 on port 14550 and GPS connected to `/dev/ttyO5` UART5.

`sudo ardupilot/ArduCopter/ArduCopter.elf -A udp:192.168.178.26:14550 -B /dev/ttyO5`

