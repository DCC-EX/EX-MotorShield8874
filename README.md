# EX-Motorshield8874

## Overview
![Produktfoto_3_1](https://user-images.githubusercontent.com/52371300/231068292-36178ca7-ed09-493d-87c2-605b19090bf4.jpg)

The EX-Motorshield8874 is a pin compatible with the original [Arduino Motor Shield Rev3](https://store.arduino.cc/products/arduino-motor-shield-rev3) but provides significantly improved electrical performance for driving higher loads, and improved usability.

The EX-Motorshield8874 is based on two DRV8874 H-bridge motor drivers with integrated current sensing from Texas Instruments (TI). It is used to drive inductive loads like relays, solenoids, DC and stepping motors.

Powering of Arduino boards is possible due to the on board DCDC buck converter, supporting a wide input supply range from 9 to 30V. The reverse polarity protection prevents damage to the circuit and its components in case the power supply is accidentally connected with reversed polarity.

This Shield features a status LED for supply, which provides a visual indication of the power supply status.


### Compatibility with [Arduino Motor Shield Rev3](https://store.arduino.cc/products/arduino-motor-shield-rev3)

The DCC-EX Motor Shield is pin compatible with the original Arduino Motor Shield but provides significantly improved electrical performance for driving higher loads. The supply voltage range is 9-30V (instead of 5-12V) and the maximal peak current is 5A per channel (instead of 2A).

## Pin Assignment for motor control

The DCC-EX Motor Shield has the following pin assignment for the Arduino header

Default pin assignment (DRV8874 mode select pin `PMODE` = high) in PWM motor control mode.

| Function | Pin |
|-----------|-------|
| Channel A | |
| Direction | D12 |
| PWM       | D3  |
| Brake     | D9  |
| Fault_N   | A4  |
| Current sensing | A0 |
| Channel B | |
| Direction | D13 |
| PWM       | D11 |
| Brake     | D8  |
| Fault_N   | A5  |
| Current sensing | A1 |

### Alternative pin assignment for motor control

The alternative pin assignment for motor control (PH/EN mode) allows to control the motor in a speed and direction type interface. This mode is selected via Jumper J101 (DRV8874 mode select pin `PMODE` = low).

_TBD_ fix table

| Function | Pin |
|-----------|-------|
| Channel A | |
| EN | D12 |
| PH       | D3  |
| Brake     | D9  |
| Fault_N   | A4  |
| Current sensing | A0 |
| Channel B | |
| Direction | D13 |
| PWM       | D11 |
| Brake     | D8  |
| Fault_N   | A5  |
| Current sensing | A1 |


### Fault indicator

The H-Brides are prodeted against supply undervoltage, charge pump undervoltage, output overcurrent and device overtemperature. Fault conditions are indicated on the pin `nFAULT` of the H-Bridge driver. The open drain output of the fault indicator is pulled low during a fault condition and pulled to high with the on board pull-up resistor. There is one fault indicator per channel.

### Alternative pinout for motor control  

All motro control signals can be connected to two different Adruino header pins. Selecting between the default pin out and the alternative pin out is done via solder jumper on the PCB.

| Function | Pin |
|-----------|-------|
| Channel A | |
| Direction | D10 |
| PWM       | D2  |
| Brake     | D7  |
| Fault_N   | D0  |
| Current sensing | A2 |
| Channel B | |
| Direction | D4  |
| PWM       | D5 |
| Brake     | D6  |
| Fault_N   | D1  |
| Current sensing | A3 |


## Parameter

The DCC-EX Motor Shield provides the following electrical parameters.

| Parameter | Value |
|-----------|-------|
|Operating voltage range | 9-30V|
| Maximal current         | 5A peak |
| Arduino supply voltage output (VIN) | 7.2V |
| IO voltage              | 3.3 and 5V |
| I2C connectivity        | Dupont and STEMMA QT Headers |
| Current sensing         | Yes |
| Control modes (selected via jumper) | PH/EN, PWM |  


## Current sensing

Current sensing is independently available for each channel. The VDDIO supply voltage sensing automatically adjusts the gain factor for the current sensing to take advantage of the full ADC input voltage range. The translation factor is 4.82 A/V.

## Track LEDs

_TBD_

## Stacking multiple boards

It is possibile to stack two DCC-EX Motor Shields. There are two different operating modes possible.

![Produktfoto_3_4](https://user-images.githubusercontent.com/52371300/231068582-4eb4e3a1-c307-405c-8cc4-71c3db39e954.jpg)


1. **Parallel mode:** The DCC-EX Motor Shields controlled with the same control signals and both H-bridges are running in parallel. This mode is used to increase the current capabilities.
1. **Independent mode:** The DCC-EX Motor Shields controlled independently using different control signals. This allows to drive in total 4 independent H-Bridges completely independently.

The independent mode uses the following pin assignment for controlling the two channels of the second DCC-EX Motor Shield



## Header

### Arduino Header
### Expansion Header

Two I2C expansion headers (Dupont and STEMMA QT) allow connecting either an OLED display or other additional I2C based devices.

| Function | Pin |
|-----------|-------|
| SCL | A5 |
| SDA | A4 |

Pull-up resistors for the I2C communication are not assembled by default. If required pull-up resistors can be assembled (R101, R102).

## Reset button

To reset the Arduino board a reset button is available.

## Reference

- [Schematic](https://github.com/semify-eda/motor-shield/blob/main/motor-shield.pdf)
- [DRV8874 Datasheet](https://www.ti.com/product/DRV8874?keyMatch=DRV8874&tisearch=search-everything&usecase=GPN)

 
