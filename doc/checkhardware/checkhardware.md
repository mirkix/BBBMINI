# Check hardware
If your board is ready you can check that everything is working as expected.

To build the example code / test code follow the instructions below.

## Compile example / test code native on BeagleBone
1. `cd ardupilot`
2. `git checkout master`
3. `git submodule update --init --recursive`
4. `alias waf="$PWD/modules/waf/waf-light"`
5. `waf configure --board=bbbmini`
6. `waf example` (take some time)
7. `cp build/bbbmini/examples/* /home/debian/`

## Cross compile example / test code (faster) with Ubuntu computer

1. `cd ardupilot`
2. `git checkout master`
3. `git submodule update --init --recursive`
6. `alias waf="$PWD/modules/waf/waf-light"`
7. `waf configure --board=bbbmini`
8. `waf example`
9. `scp build/bbbmini/examples/* debian@beaglebone:/home/debian/`

## Check IMU
`sudo /home/debian/INS_generic`

## Check baro
`sudo /home/debian//BARO_generic`

## Check GPS
`sudo /home/debian/GPS_AUTO_test -B /dev/ttyO5`

## Check rcinput
`sudo /home/debian/RCInput`
