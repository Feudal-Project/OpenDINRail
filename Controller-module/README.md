# Controller module
The Controller module is a DIN rail mountable ESP32 which can be connected to the [IO module](https://github.com/Feudal-Project/Trebuchet). It is intended as a DIY project for anyone who is already familiar with ESPHome and has a basic to advanced level of soldering skills.

## Features
- Powered by 24V external powersupply.
- connected via ethernet (makes use of the Olimex ESP32 POE).
- Side connector for daisy-chaining up to 4 [IO modules](https://github.com/Feudal-Project/Trebuchet).
- Can be powered by POE to sense external power loss.
- additional 3.3V and 5V voltage converters.
- 3D printable housing with engraved port descriptions and DIN Rail compatibility with 3D printed locking keys.
- Highly versatile in its use due to the vast possibilities of ESPHome.
- Can interact with other modules over I2C and SPI.

<p align="center">
  <img src="/images/Controller-module.jpg" width="50%">
</p>

## FAQs
### What is the idea behind the controller module?
The main idea is to create an ESP32 based DIN rail mountable controller, which is connected to your Home Assistant locally over ethernet. To control your appliances you need additional modules, like the [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module). The controller module itself does not have controllable outputs by itself.

### What are those jumpers about?
The controller module has three different jumpers scattered on the pcb (JP1, JP3 and JP4). Those jumpers are used to connect different power paths on the PCB. 
- JP1: overwrites the Input Power Shut Off circuit. Set this Jumper, if the circuit for an automatic Power Shut off is not placed (ESP32 loses POE power => Modules get their power cut). In general, if you power the module over the external power supply and NOT with POE, this Jumper must be set.
- JP3: connects the 5V line with the 5V Pin of the ESP32 POE. Set this jumper, to power the ESP32 over the external Powersupply, if no POE is used.
- JP4: connects the 3.3V line with 3.3V Pin of the ESP32 POE. This jumper can be used to power IO Modules over the ESP32 POEs DCDCs, if the module internal DCDCs are not placed (U2 and U3). With the onboard DCDC from the ESP32 POE beeing quite weak, this setup is not recommended!

## Wiring
Wiring your controller only includes supply 24V power and connecting the ethernet cable. To power other module, simply connect them via the side connector. To find out more about wiring look at the wiring section of the [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module)

<p align="center">
  <img src="/images/OpenDINRail-simple-schematic.png" width="80%">
  <img src="/images/OpenDINRail-simple-schematic-cover.png" width="80%">
</p>
