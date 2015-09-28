# Check hardware
If your board is ready, check the functionality.

## Check IMU
`cd ardupilot/libraries/AP_InertialSensor/examples/INS_generic`

`make bbbmini`

`sudo ./INS_generic.elf`

## Check baro
`cd ardupilot/libraries/AP_Baro/examples/BARO_generic`

`make bbbmini`

`sudo ./BARO_generic.elf`

## Check GPS
`cd ardupilot/libraries/AP_GPS/examples/GPS_AUTO_test`

`make bbbmini`

`sudo ./GPS_AUTO_test.elf -B /dev/ttyO5`

## Check rcinput
`cd ardupilot/libraries/AP_HAL/examples/RCInput`

`make bbbmini`

`sudo ./RCInput.elf`

## Check rcoutput
`cd ardupilot/libraries/AP_HAL/examples/RCOutput`

`make bbbmini`

`sudo ./RCOutput.elf`

