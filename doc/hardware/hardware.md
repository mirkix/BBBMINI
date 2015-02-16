#Hardware
## Pin assigment

### RCInput
BBB | RC Receiver | Remark
------------ | ------------- | -------------
P9.01 DGND | GND
P8.15 RC_IN | RC Out (Spektrum / PPM-sum) | 

### RCOutput
BBB | ESC / Servo | Remark
------------ | ------------- | -------------
P9.01 DGND | GND | 
P8.27 | RC_OUT_CH_2 | Use level shifter 3.3 Volt to 5 Volt
P8.28 | RC_OUT_CH_1 | Use level shifter 3.3 Volt to 5 Volt
P8.29 | RC_OUT_CH_4 | Use level shifter 3.3 Volt to 5 Volt
P8.30 | RC_OUT_CH_3 | Use level shifter 3.3 Volt to 5 Volt
P8.39 | RC_OUT_CH_6 | Use level shifter 3.3 Volt to 5 Volt
P8.40 | RC_OUT_CH_5 | Use level shifter 3.3 Volt to 5 Volt
P8.41 | RC_OUT_CH_8 | Use level shifter 3.3 Volt to 5 Volt
P8.42 | RC_OUT_CH_7 | Use level shifter 3.3 Volt to 5 Volt
P8.43 | RC_OUT_CH_10 | Use level shifter 3.3 Volt to 5 Volt
P8.44 | RC_OUT_CH_9 | Use level shifter 3.3 Volt to 5 Volt
P8.45 | RC_OUT_CH_12 | Use level shifter 3.3 Volt to 5 Volt
P8.46 | RC_OUT_CH_11 | Use level shifter 3.3 Volt to 5 Volt

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
Baudrate 38400, 8, n, 1

BBB | GPS | Remark
------------ | ------------- | -------------
P9.01 DGND | GND | 
P8.37 GPS_TX | GPS_RX | Use level shifter 
P8.38 GPS_RX | GPS_TX | Use level shifter

