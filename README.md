# BBBmini

Linux ArduPilot DIY Cape for the BeagleBone Black / Green  (BBB / BBG)

![alt text](doc/pic/bbbmini.png "BBBMINI breadboard")

![alt text](doc/pic/bbbminiquad.png "BBBMINI Quad")

![alt text](doc/pic/bbbminipcbquad.png "BBBMINI Quad")

## Why?
* Have fun to build your own BeagleBone ArduPilot Cape
* Easy start to ArduPilot Linux development
* No SMD soldering required
* DIY friendly connector

## [Hardware](doc/hardware/hardware.md)
* BeagleBone Black or BeagleBone Green
* [BBBMINI-PCB](https://github.com/mirkix/BBBMINI-PCB) (recommended) or BeagleBone Proto Cape with IMU MPU-9250 breakout board and Baro MS5611 breakout board (try to get a GY-9250 and GY-63 breakout board)
* RC receiver (S.BUS, PPM-Sum, Spektrum Satellit SPM 9645)
* optional GPS receiver
* optional HC-SR04 Ultrasonic Module

Click [here](doc/hardware/hardware.md) for further instruction how to assemble the board and the pin assignment.

## [Software](doc/software/software.md)
For instructions how to get, build, test and run the software click [here](doc/software/software.md).

## 

## Status

### Working
* RT-Kernel
* MPU-9250 (via SPI)
* MS5611 (via SPI)
* RCInput with Spektrum SPM 9645, FrSky X8R
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
* Dual IMU

### ToDo
* Documentation redesign 

## Support

### Support Chat

[![Join the chat at https://gitter.im/mirkix/BBBMINI](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mirkix/BBBMINI?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

### User Group

[DIY DRONES BBBMINI User Group](http://diydrones.com/group/bbbmini)

### License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">BBBmini</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/mirkix" property="cc:attributionName" rel="cc:attributionURL">Mirko Denecke</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

UNLESS OTHERWISE MUTUALLY AGREED TO BY THE PARTIES IN WRITING, LICENSOR OFFERS THE WORK AS-IS AND MAKES NO REPRESENTATIONS OR WARRANTIES OF ANY KIND CONCERNING THE WORK, EXPRESS, IMPLIED, STATUTORY OR OTHERWISE, INCLUDING, WITHOUT LIMITATION, WARRANTIES OF TITLE, MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NONINFRINGEMENT, OR THE ABSENCE OF LATENT OR OTHER DEFECTS, ACCURACY, OR THE PRESENCE OF ABSENCE OF ERRORS, WHETHER OR NOT DISCOVERABLE. SOME JURISDICTIONS DO NOT ALLOW THE EXCLUSION OF IMPLIED WARRANTIES, SO SUCH EXCLUSION MAY NOT APPLY TO YOU. EXCEPT TO THE EXTENT REQUIRED BY APPLICABLE LAW, IN NO EVENT WILL LICENSOR BE LIABLE TO YOU ON ANY LEGAL THEORY FOR ANY SPECIAL, INCIDENTAL, CONSEQUENTIAL, PUNITIVE OR EXEMPLARY DAMAGES ARISING OUT OF THIS LICENSE OR THE USE OF THE WORK, EVEN IF LICENSOR HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.
