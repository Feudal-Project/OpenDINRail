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

## Wiring
Wiring your controller only includes supply 24V power and connecting the ethernet cable. To power other module, simply connect them via the side connector. To find out more about wiring look at the wiring section of the [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module)

<p align="center">
  <img src="/images/OpenDINRail-simple-schematic.png" width="80%">
  <img src="/images/OpenDINRail-simple-schematic-cover.png" width="80%">
</p>
