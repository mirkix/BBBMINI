# BBBMINI
Simple ArduPilot DIY Cape for the BeagleBone Black (BBB)

![alt text](doc/pic/bbbmini.png "BBBMINI breadboard")

![alt text](doc/pic/bbbminiquad.png "BBBMINI Quad")

![alt text](doc/pic/bbbminipcbquad.png "BBBMINI Quad")

## Why?
* Have fun to build your own BBB ArduPilot Cape
* Easy start to ArduPilot Linux development
* No SMD soldering required
* DIY friendly connector

## [Hardware](doc/hardware/hardware.md)
* BeagleBone Black
* [BBBMINI-PCB](https://github.com/mirkix/BBBMINI-PCB) (recommended) or BeagleBone Black Proto Cape with IMU MPU-9250 breakout board and Baro MS5611 breakout board (try to get a GY-9250 and GY-63 breakout board)
* Spektrum Satellit SPM 9645, SBUS, PPM-Sum
* GPS
* HC-SR04 Ultrasonic Module

Click [here](doc/hardware/hardware.md) for further instruction how to assemble the board and the pin assignment.

## [Software](doc/software/software.md)
For instructions how to get, build, test and run the software click [here](doc/software/software.md).

## Status

### Working
* RT-Kernel
* MPU-9250 (via SPI)
* MS5611 (via SPI)
* RCInput with Spektrum SPM 9645
* RCOutput
* GPS uBlox NEO-M8N (5Hz with GPS + GLONASS)
* IP connection via WLAN to Ground Station (APM Planner) 
* Connection to Ground Station (APM Planner) via radio module
* dts file for BBBMINI
* Solder the breakout boards on a prototype cape, so it is reliable to fly.
* First flight on March 16, 2015
* Create documentation / [schematic](https://github.com/mirkix/BBBMINI-PCB/blob/master/schematic/bbbmini.pdf)
* Develop a BBBMINI printed circuit board
* Add CAN bus for UAVCAN
* Add HC-SR04 Ultrasonic Module support to BBBMINI

### ToDo
