# MKS THR36&THR42
## MKS THR36&THR42
MKS THR36&THR42 is two tool header modules that can simplify the wiring between 3D printing motherboard and extrusion related parts(You can choose to use usb cable or usb-to-Can to connect). THR36 is for NEMA14 stepper, while THR42 is for NEMA17 stepper. Both the modules integrate TMC2209 driver(for E-axis) and ADXL345 sensor, support interfaces for BLtouch, neopixel, three controllable fans, X, Y, Z enstops. What is more, they support USB or Can bus to communicate with SOC, which makes the wiring of the printer easier and allows users to reflect the superior performance of the klipper firmware.

## Features and advantages
- Integrated RP2040 MCU, 8M NOR FLASH.
- Integrated TMC2209 silent driver, with UART driver mode.
- Integrated CAN transceiver, integrated 120Ω terminal resistance. Can be used for CAN communication to connect to MKS UTC.
- Integrated ADXL345 acceleration sensor.
- 3-channel controllable fan outputs, 1 heating head output, 1 NTC100K temperature measurement.
- Integrated interfaces for X, Y, Z enstops(Z enstop can be set to 5V or VIN power supply, compatible with proximity switch), filament detection, Neopixel, 3D TOUCH etc .
- The BOOT button can be used for RP2040 to update the firmware on USB mode. USB can also be used for communication to connect to MKS Pi, Raspberry Pi.
- MKS THR36 is compatible with NEMA14 stepper; MKS THR36 is compatible with NEMA17 stepper.
- Support DC12-24V power input.
- The modules integrates TVS peak absorption protection, and also Schottky diode clamping protection circuit. What is more, built-in phase circuit protection for stepper.
- Easy wiring with screw terminals.

## Parameters
| MKS THR36      |   |
|------------|--------------------|
| Input voltage | DC12V~24V |
| MCU        | RP2040 | 
| Stepper driver | TMC2209 | 
| Temperature sensor interface | NTC 100K |
| Firmware | klipper | 
| Dimension | R=25mm | 
| Mounting hole size | 43.85mm | 

| MKS THR42      |   |
|------------|--------------------| 
| Input voltage | DC12V~24V |
| MCU        | RP2040 | 
| Stepper driver | TMC2209 | 
| Temperature sensor interface | NTC 100K | 
| Firmware | klipper | 
| Dimension | 42mm*42mm | 
| Mounting hole size | 31mm*31mm | 

# MKS UTC
MKS UTC is an USB to CAN communication module, which is used for communication between THR modules and SOC like RasPI/MKS PI.





                               
