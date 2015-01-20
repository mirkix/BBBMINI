# BBBMINI
Simple ArduPilot DIY Cape for the BeagleBone Black (BBB)

## Why?
* Have fun to build your own BBB Ardupilot Cape.
* Easy start to the Linux development for ArduPilot.
* No SMD soldering required.

## Hardware
* BeagleBone Black
* IMU MPU-9250, Baro MS 5611 (try to get a Combi Breakout Board)
* Spektrum Satellit SPM 9645, PPM-sum should also work
* Level Shifter 3.3 Volt to 5 Volt (bidirectional)
* GPS

## Software

### Get required software
`apt-get install git make gawk g++ arduino-core`

`git clone git://github.com/diydrones/ardupilot.git`

### Compile ArduPilot
`cd ardupilot/ArduCopter`

or

`cd ardupilot/ArduPlane`

or 

`cd ardupilot/APMrover2`

then

`make configure`

`make bbbmini`

### Run ArduPilot
Before you can start ArduPilot you have to enable the hardware once after startup:

`sudo ardupilot/Tools/Linux_HAL_Essentials/startup.sh load`

then you can start Ardupilot:

`sudo ardupilot/ArduCopter/ArduCopter.elf`

or

`sudo ardupilot/ArduPlan/ArduPlan.elf`

or

`sudo ardupilot/APMrover2/APMrover2.elf`


## Pin assigment
Please keep in mind that the CPU of the BBB can be destroyed, if the voltage at the expansion header pins is higher than 3.3 Volt. So it is a good choice to use Level Shifter on each used expansion header pin (P8 and P9). You can use Level Shifter in 3.3 Volt to 3.3 Volt configuration to protect BBB expansion header pins which are connected to 3.3 Volt signals.

### RCInput
BBB | RC Receiver | Remark
------------ | ------------- | -------------
P9.01 DGND | GND
P9.03 VDD_3V3 | VDD | 3.3 Volt for Spektrum Satellit SPM 9645
P8.15 RC_IN_3V3 | RC Out (Spektrum / PPM-sum) | The Spektrum output is 3 Volt, check if Level Shifter is required 

### RCOutput
BBB | ESC / Servo | Remark
------------ | ------------- | -------------
P9.01 DGND | GND | 
P8.27 | RC_OUT_CH_2 | Use Level Shifter 3.3 Volt to 5 Volt
P8.28 | RC_OUT_CH_1 | Use Level Shifter 3.3 Volt to 5 Volt
P8.29 | RC_OUT_CH_4 | Use Level Shifter 3.3 Volt to 5 Volt
P8.30 | RC_OUT_CH_3 | Use Level Shifter 3.3 Volt to 5 Volt
P8.39 | RC_OUT_CH_6 | Use Level Shifter 3.3 Volt to 5 Volt
P8.40 | RC_OUT_CH_5 | Use Level Shifter 3.3 Volt to 5 Volt
P8.41 | RC_OUT_CH_8 | Use Level Shifter 3.3 Volt to 5 Volt
P8.42 | RC_OUT_CH_7 | Use Level Shifter 3.3 Volt to 5 Volt
P8.43 | RC_OUT_CH_10 | Use Level Shifter 3.3 Volt to 5 Volt
P8.44 | RC_OUT_CH_9 | Use Level Shifter 3.3 Volt to 5 Volt
P8.45 | RC_OUT_CH_12 | Use Level Shifter 3.3 Volt to 5 Volt
P8.46 | RC_OUT_CH_11 | Use Level Shifter 3.3 Volt to 5 Volt

### IMU / Baro
BBB | MPU-9250 / MS 5611 (Combi) Breakout Board
------------ | -------------
P9.01 DGND | GND
P9.03 VDD_3V3 | VDD
P9.23 MPU9250_CS | MPU9250_CS
P9.29 SPI1_MOSI | MOSI / SDA (MPU-9250 and MS5611)
P9.30 SPI1_MISO | MISO / SDO (MPU-9250 and MS5611)
P9.31 SPI1_SCLK | SCLK / SCL
P9.42 MS5611_CS | MS5611_CS

### GPS
BBB | GPS | Remark
------------ | ------------- | -------------
P9.01 DGND | GND | 
P8.37 GPS_TX | GPS_RX | Maybe Level Shifter required 
P8.38 GPS_RX | GPS_TX | Maybe Level Shifter required 







