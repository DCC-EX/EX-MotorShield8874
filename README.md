# EX-Motorshield8874

## Overview
![Produktfoto_3_1](https://user-images.githubusercontent.com/52371300/231068292-36178ca7-ed09-493d-87c2-605b19090bf4.jpg)

The EX-Motorshield8874 is a pin compatible with the original [Arduino Motor Shield Rev3](https://store.arduino.cc/products/arduino-motor-shield-rev3) but provides significantly improved electrical performance for driving higher loads, with lower power dissipation, and improved usability.

The EX-Motorshield8874 is based on two DRV8874 H-bridge motor drivers with integrated current sensing from Texas Instruments (TI). It is used to drive inductive loads like relays, solenoids, DC and stepping motors.

Powering of Arduino motherboard is possible due to the onboard DC/DC buck converter, supporting a wide input supply range from 9 to 30V. The reverse polarity protection prevents damage to the circuit and its components in case the power supply is accidentally connected with reversed polarity.

This Shield features a green status LED which provides a visual indication of the power supply status.


### Compatibility with [Arduino Motor Shield Rev3](https://store.arduino.cc/products/arduino-motor-shield-rev3)

The EX-MotorShield8874 is pin compatible with the original Arduino Motor Shield but provides significantly improved electrical performance for driving higher loads. Input voltage range is 9-30VDC and the maximum peak output is 5A per channel, in contrast to 5-12VDC and 2A peak for the original Arduino Motor Shield.

There is also almost no voltage drop incurred from the input voltage due to the MOSFET based design, unlike the bipolar L298 used in the Arduino Motor Shield. For DCC and DC PWM model railway use, a range of 10-20VDC is recommended depending on scale.

## Default Pin Assignment for DCC-EX/Arduino motor control

The EX-MotorShield8874 has the following default pin assignment for control pins on the Arduino header, and is used for full Arduino Motor Shield R3 compatibility when used for DCC-EX EX-CommandStation.

| Function | Channel A Pin | Channel B Pin |
|-----------|-------|-------|
| PWM       | D3  | D11 |
| Direction | D12 | D13 |
| Brake     | D9  | D8 |
| Current sensing | A0 | A1 |
| Fault_N   | A4  | A5 |

Default pin assignment is used for DCC-EX command stations, and has the DRV8874 mode select pin `PMODE` = high.

### Alternative Pin Assignment for DCC-EX/Arduino motor control 

All motor control signals can be connected to two different Adruino header pins. Selecting between the default pin out and the alternative pin out is done via solder jumpers on the PCB which must be first cut to disable the default position, then solder applied to select the alternate position.

| Function | Channel A Pin | Channel B Pin |
|-----------|-------|-------|
| PWM       | D2  | D5 |
| Direction | D10 | D4 |
| Brake     | D7  | D6 |
| Current sensing | A2 | A3 |
| Fault_N   | D0  | D1 |

NB: For DCC-EX control, these are not ideal pin assignments. Further documentation updates will be available once testing of this mode is complete.

### Fault indicator

The H-Bridges are protected against supply undervoltage, charge pump undervoltage, output overcurrent and device overtemperature. Fault conditions are indicated on the pin `nFAULT` of the H-Bridge driver. The open drain output of the fault indicator is pulled low during a fault condition and pulled to high with the on board pull-up resistor. There is one fault indicator per channel.

### Alternative pin assignment for other motor control applications

The alternative pin assignment for motor control (PH/EN mode) allows to control the motor in a speed and direction type interface. This mode is selected via Jumper J101 (DRV8874 mode select pin `PMODE` = low) and is NOT required for use with DCC-EX. It is documented for completeness.

| Function | Channel A Pin | Channel B Pin |
|-----------|-------|-------|
| PH       | D3  | D11 |
| EN       | D12 | D13 |
| Brake     | D9  | D8 |
| Current sensing | A0 | A1 |
| Fault_N   | A4  | A5 |

## Electrical Parameters

The DCC-EX Motor Shield provides the following electrical parameters.

| Parameter | Value |
|-----------|-------|
| Operating voltage range | 9-30VDC, polarity protected|
| Maximum H-bridge current  | 5A peak per channel |
| Arduino supply voltage output (VIN) | 7.2V@2A max |
| IO voltage              | 3.3 and 5V, using IOREF by default |
| I2C connectivity        | Dupont, 2.54mm dual row pin, and STEMMA QT/Qwiic Headers |
| Current sensing         | Yes, adjusts range to IOREF voltage |
| Control modes possible | PWM, by default, PH/EN via jumper |


## Current sensing

Current sensing is independently available for each channel. The Arduino IOREF supply voltage is sensed automatically, and adjusts the gain factor for the current sensing to take advantage of the full ADC input voltage range for 5V or 3.3V microcontrollers. The sense factors are calculated as follows for DCC-EX motor driver definitions:

| IOREF Voltage: | 5V | 3V3 |
|----------------|----|-----|
| 10-bit ADC, 1024 count | 5.08 | 4.94 |
| 12-bit ADC, 4096 count | 1.27 | 1.24 |

## Track LEDs

LEDs are provided for each channel, indicating the corresponding H-Bridge is supplying power to output connectors.

## Header Pin Assignments

The following pin assignments have been used for the various connectors.
### Arduino Headers

| Function | Left Header Pin |
|-----------|-------|
| IOREF | 1 |
| SDA | 3 |
| GND | 5 |
| SCL | 7 |


### Expansion Headers

Three I2C expansion headers (Dupont, dual-row 8-pin, and STEMMA QT/Qwiic) allow connecting either an OLED display or other additional I2C based devices.

On the Arduino header, the default upper right I2C pins are used for I2C:

| Function | UNO R3 Pin | Mega Pin |
|-----------|-------|-------|
| SCL | D18 | D21 |
| SDA | D19 | D20 |

The dual-row 8-pin header has the following pin assignments:

| Function | Odd Pin | Even Pin |
|-----------|-------|-------|
| IOREF | 1 | 2 |
| SDA | 3 | 4 |
| GND | 5 | 6 |
| SCL | 7 | 8 |


Pull-up resistors for the I2C communication are not populated by default. If required, pull-up resistors (R101, R102) can be populated on the board, though this is typically not necessary.

## Reset button

A reset button is provided to reset the Arduino board.

## Stacking multiple boards

It is possibile to stack two EX-MotorShield8874s, though as yet this is not fully tested and supported in DCC-EX EX-CommandStation. There are two different operating modes possible.

![Produktfoto_3_4](https://user-images.githubusercontent.com/52371300/231068582-4eb4e3a1-c307-405c-8cc4-71c3db39e954.jpg)


1. **Independent district mode:** The DCC-EX Motor Shields are controlled independently using different control signals. This allows a total 4 independent H-Bridges to be driven completely independently for separate DCC or DC PWM districts.
2. **Parallel booster mode:** Both EX-MotorShield8874s are controlled with the same control signals so both H-bridges are running in parallel. This mode is used to increase the current capabilities of the 2 DCC or DC PWM districts.

The independent mode uses the following pin assignment for controlling the two channels of the second DCC-EX Motor Shield

## Reference

- [Schematic](https://github.com/semify-eda/motor-shield/blob/main/motor-shield.pdf)
- [DRV8874 Datasheet](https://www.ti.com/product/DRV8874?keyMatch=DRV8874&tisearch=search-everything&usecase=GPN)

 
