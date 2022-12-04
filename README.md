# MKS THR36&THR42
## Overview
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

## Wiring diagram
### MKS THR36 diagram
![size](https://user-images.githubusercontent.com/12979070/205477677-9275c0c7-0b38-4316-8744-873c80a18c54.jpg)

### MKS THR42 diagram
![size42](https://user-images.githubusercontent.com/12979070/205477698-f892b829-272b-4767-9ed1-cb4e134433ea.jpg)

## Firmware compile and update
The firmware of the module has been flashed by default (the default firmware is usb communication), if you want to update for CAN communication, you can download the compiled firmware from our github to update, or follow the steps below to configure and compile the firmware to update

### Klipper Compile
You should know how to use a klipper host to config and compile firmware for MCU, if not, please refer to http://www.klipper3d.org/Installation.html?h=menuconfig#building-and-flashing-the-micro-controller

After run "make menuconfig":  
**THR 36/42 Configuration (connect with Can) **   
![config_can](https://user-images.githubusercontent.com/12979070/205478259-2dd5f8c5-26bf-440f-84d8-aec1adb23618.png)

**THR 36/42 Configuration (connect with USB) **  
![config_usb](https://user-images.githubusercontent.com/12979070/205478264-b9398b7a-d880-4b49-a26b-bfafcadf9fa4.png)

Then run "make" to generate the "klipper.uf2" on the direction of "~/klipper/out/"

### THR36/42 firmware update
Press and hold the boot button on the MKS THR36/42 board, connect to the computer with a Type_C cable, the computer can recognize the RPI_RP2 disk, copy the compiled firmware klipper.uf2 (path: klipper/out) to the disk, just wait serval seconds and the firmware will be updated automatically.  
![udisk](https://user-images.githubusercontent.com/12979070/205478314-b7905623-3d5c-45bb-b456-214ceef92a45.png)

## Configure printer configuration
We have uploaded an indenpent "MKS_THR.cfg" [here](https://github.com/makerbase-mks/MKS-THR36-THR42-UTC/blob/main/MKS_THR.cfg), which has configuared the hardware infomation of MKS THR36/42. You just need to copy it to the same direction as your "printer.cfg", check the "serial" section on the "[mcu MKS_THR]" node, and include the "MKS_THR.cfg" on your "printer.cfg" file.  
![printer cfg](https://user-images.githubusercontent.com/12979070/205478993-5ebc6275-ddb4-4ae1-918b-bba750cc6aef.png)

### USB communication
- Keep the usb connection is ok between the MKS THR36/42 and your Klipper host board, and power on.
- SSH login to your Klipper console and run
> ls /dev/serial/by-id/*   

Copy the return string(if not return, please check the connection and reboot) to rewrite the "serial" section on the "[mcu MKS_THR]" node of "MKS_THR.cfg" file. For example:  
![usb_configu](https://user-images.githubusercontent.com/12979070/205479233-397f18d3-aaab-43bb-8d17-23193c80ff52.png)  

### CANBUS communication
- Keep the CAN connection is ok between the MKS THR36/42 and your Klipper host board, and power on.
- Check whether you have the the file "/etc/network/interfaces.d/can0", if not, create it:
> sudo nano /etc/network/interfaces.d/can
- Edit the "/etc/network/interfaces.d/can" like below(Reference link:https://www.klipper3d.org/CANBUS.html?h=canbus):
> auto can0  
> iface can0 can static  
> bitrate 250000  
> up ifconfig $IFACE txqueuelen 128  
- Press ctrl+S to save, and ctrl+X to exit
- Run the command to get the uuid of CAN interface:  
> ~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0  
- Copy the return string(if not return, please check the connection and reboot) to rewrite the "serial" section on the "[mcu MKS_THR]" node of "MKS_THR.cfg" file. For example:  
![can-configu](https://user-images.githubusercontent.com/12979070/205479488-813104f5-040b-4f1e-8655-36f1c22df56c.png)


# MKS UTC
MKS UTC is an USB to CAN communication module, which is used for communication between THR modules and SOC like RasPI/MKS PI.

## MKS UTC Wiring diagram
![utc](https://user-images.githubusercontent.com/12979070/205477726-b6ac7069-92d7-4b6c-80e6-ab29e2f077f5.jpg)

## MKS UTC firmware update
**The firmware of the module has been flashed by default, commonly, it is no need to update the firmware.**
- Download the [update package](https://github.com/makerbase-mks/MKS-THR36-THR42-UTC/blob/main/MKS%20UTC%20DFU-Upload.rar)  
- Press and hold the boot button on the MKS UTC board, connect it to the computer with a TypeC cable, run the DFU-upload-firmware.bat(On windows OS) to update the firmware(You can replace with your own klipper.bin firmware if you want)  
![utc_update](https://user-images.githubusercontent.com/12979070/205479861-236ce417-46a5-480d-a280-3fad873f04d6.png)

# More Reference
## Connection with motherboard (MKS Monster8、MKS PI,Can communication)
![monster8_with](https://user-images.githubusercontent.com/12979070/205477776-01c49927-f670-4f89-aa5e-530c13e2bb32.jpg)

## Connection with motherboard (MKS SKIPR,USB communication)
![skipr_usb](https://user-images.githubusercontent.com/12979070/205477817-13bf5808-f870-49af-8819-ad20a2bb9889.jpg)



                               
