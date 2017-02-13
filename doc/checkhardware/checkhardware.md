# Check hardware
If your board is ready you can check that everything is working as expected.

To build the example code / test code follow the instructions below.

## Compile example / test code native on BeagleBone
1. `cd ardupilot`
2. `git checkout master`
3. `git submodule update --init --recursive`
4. `./waf configure --board=bbbmini`
5. `./waf examples` (take some time)
6. `cp build/bbbmini/examples/* /home/debian/`

## Cross compile example / test code (faster) with Ubuntu computer

1. `cd ardupilot`
2. `git checkout master`
3. `git submodule update --init --recursive`
4. `./waf configure --board=bbbmini`
5. `./waf examples`
6. `scp build/bbbmini/examples/* debian@beaglebone:/home/debian/`

## Check IMU
`sudo /home/debian/INS_generic`

## Check baro
`sudo /home/debian/BARO_generic`

## Check GPS
`sudo /home/debian/GPS_AUTO_test -B /dev/ttyO5`

## Check rcinput
`sudo /home/debian/RCInput`
