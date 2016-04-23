#Hardware

## Schematic
![Schematic](https://github.com/mirkix/BBBMINI-PCB/blob/master/schematic/bbbmini.pdf)

## PCB
![PCB](https://github.com/mirkix/BBBMINI-PCB/blob/master/picture/bbbmini.png)

## Assemble BBBmini

### Step 1: Solder resistor R4 and R5.

For 3.3V RC input signal use R4 = 0Ω (bridge) and R5 = open (see picture)

For 5V RC input signal use R4 = 1kΩ and R5 = 2kΩ

![alt text](../pic/build/build_step1.jpg "Solder R4 and R5")

### Step 2:

Solder resistor

R1 = 120Ω

R2 = 1kΩ

R3 = 2kΩ

R6 = 20kΩ 0.1%

R7 = 10kΩ 0.1%

R8 = 20kΩ 0.1%

R9 = 10kΩ 0.1%

to the bottom layer. 

![alt text](../pic/build/build_step2.jpg "Solder R1, R2, R3, R6, R7, R8 and R9")

### Step 3:

Solder CAN transceiver on the top layer

![alt text](../pic/build/build_step3.jpg "Solder CAN transceiver")

### Step 4:

Solder male pin-header on top layer

P1, P2, P3, P4, P7, P10, P11, P12, P13, P14, P15, P16, P17, P18, P19, P20, P21

![alt text](../pic/build/build_step4.jpg "Solder P1, P2, P3, P4, P7, P10, P11, P12, P13, P14, P15, P16, P17, P18, P19, P20, P21")

### Step 5:

Solder C1 and C2

![alt text](../pic/build/build_step5.jpg "Solder C1 and C2")

### Step 6:

Solder female pin-header P5 and P6 on top layer

Solder P5 and P6

![alt text](../pic/build/build_step6.jpg "Solder P5 and P6")

### Step 7:

Solder male pin-header P8 and P9 to bottom layer

![alt text](../pic/build/build_step7.jpg "Solder P8 and P9")

### Step 8:

Solder male pin-header to bottom layer of GY-9250 and GY-63

![alt text](../pic/build/build_step8.jpg "Solder pin-header for GY-9250 and GY-63")

### Step 9:

Mount spacer to BBBmini

![alt text](../pic/build/build_step9.jpg "Mount spacer")

### Step 10:

Mount GY-9250 and GY-63

![alt text](../pic/build/build_step10.jpg "Mount GY-9250 and GY-63")

### Finish! BBBmini is ready to use for Copter, Planes or Rover.

![alt text](../pic/build/build_step11.jpg "BBBmini")


## Connect BBBmini

### Connect motors and ESC
![alt text](../pic/connect/esc.png "Connect motors and ESC")

### Connect power distribution

* Connect each ESC to the power distribution board
* Connect the 5V power distribution board output to BBBmini P11 power input
* Connect the voltage and current sensing power distribution board output to BBBmini P21 voltage and current sensing pins

![alt text](../pic/connect/power.png "Connect power distribution")

### Connect RC receiver
![alt text](../pic/connect/rcrx.png "Connect RC receiver")

### Connect display
![alt text](../pic/connect/display.png "Connect display")

### Connect GPS

* Connect your GPS to P10.
* P10 +3.3V to GPS VCC
* P10 GND to GPS GND
* P10 RX to GPS TX
* P10 TX to GPS RX

![alt text](../pic/connect/gps.png "Connect GPS")

### Connect telemetry

* Connect your telemetry radio to P7.
* P7 +5V to telemetry radio VCC
* P7 GND to telemetry radio GND
* P7 RX to telemetry radio TX
* P7 TX to telemetry radio RX

![alt text](../pic/connect/telemetry.png "Connect telemetry")

### Connect HC-SR04

* Connect your HC-SR04 ultrasonic rangefinder
* P19 +5V to HC-SR04 VCC
* P19 GND to HC-SR04 GND
* P19 TRIG to HC-SR04 TRIG
* P19 ECHO to ECHO TRIG

![alt text](../pic/connect/hcsr04.png "Connect HC-SR04")
