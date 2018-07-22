# pic16f1-mcu

I graduated from Physics department some ten years ago, but I have forgetten all the theories and equations.

I am relearning Physics for some reason.

## PIC16F1 as measuring instrument for learning Physics

I think PIC16F1 DIP package (14 pins, such as PIC16F18326 or PIC16F1825) is a perfect solution to develop a measuring instrument for learning Physics on my own (one exception is that STM32L476RG is perfect when audio signal processing is required).

It is very small and very cheap, but it has a lot of capabilities comparable to Arduino.

I developed my original PIC16F1 evaluation board in 2017, and I have used this board for a number of IoT demonstrations so far. When a demo is expected to be small and simple, the board is more useful than other commercial boards such as Arduino or STM32 Nucleo.

![](https://docs.google.com/drawings/d/e/2PACX-1vTHoT0TZIyVhAgkDVHyuWkc1-_6oFHT2mF53g2q36bgH_qxplkvvRIkJ3PqJBNuTZauhhMmSiemMoZO/pub?w=680&h=400)

For example, below is a hamster wheel to which a hall sensor is attached to count the number of pulses: how long a hamster runs at night.

![](./doc/hamster_wheel.jpg)

I usually use the board with RasPi or Android, but I use it as a stand-alone system for physics experiments this time.

## PIC16F18326

I develop a small 9-axis sensor unit with [PIC16F18326](http://ww1.microchip.com/downloads/en/DeviceDoc/40001839B.pdf) and [MPU9250](https://www.invensense.com/products/motion-tracking/9-axis/mpu-9250/). I will use this for experiments of mechanics (physics).

```
     5V
      |
     LDO
      | (3.3V)                     5V system
      V                         +-------------+               +---------+
  [MPU9250]--- I2C --+--(3.3V)--|             |--- Tx(5V) --->|USB-UART |
  [EEPROM]---- I2C --+--(5V)----| PIC16F18326 |<-- Rx(3.3V) --|converter|
                     |          +------+------+               +---------+
  [Character LCD] ---+                 |
                  (5V)             GPIO out (5V)
                                       |
                                 [Tactile SW]
                           
```
Datasheet

- [8bit MCU "PIC16F18326"](http://ww1.microchip.com/downloads/en/DeviceDoc/40001839B.pdf)
- [Nine-axis motion detector "MPU9250"](https://www.invensense.com/products/motion-tracking/9-axis/mpu-9250/)
- [EEPROM "AT24C256B"(256kbits)](http://akizukidenshi.com/download/at24c256b.pdf)

#### Nine-axis motion detector

- 100Hz sampling via I2C for gyroscope and accelerometer, with the built-in low pass filter enabled to cut off frequencies over 100Hz.
- 1Hz sampling via I2C for digital compass.

Data rate estimation: 12 bytes * 8 bits * 100 Hz = 10kbps

#### EEPROM

I2C address: 1 0 1 0 [A2] [A1] [A0] [R/W]

#### Circuit diagram

- [schematic](./kicad/motion_detector/motion_detector.pdf)

