# Onager
The Onager is a DIN rail mountable ESP32 based controller module which can be connected to the [Trebuchet](https://github.com/Feudal-Project/Trebuchet) module (IO module). It is intended as a DIY project for anyone who is already familiar with ESPHome and has a basic to advanced level of soldering skills.

## Features
- Power by 24V external powersupply
- connected via ethernet (makes use of the olimex ESP32 POE)
- Side connector for daisy chaining up to 4 [Trebuchet](https://github.com/Feudal-Project/Trebuchet) modules.
- Can be powered by POE to sense external power loss
- additional 3.3V and 5V voltage converters
- 3D printable housing with engraved port descriptions and DIN Rail compatibility with 3D printed locking keys.
- Highly versatile in its use due to the vast possibilities of ESPHome.
- 
<p align="center">
  <img src="/images/Onager.jpg" width="50%">
</p>

## Background
In 2023 I had the opportunity to work on a smart home for a house being newly built at that time. The owner is a big fan of Home Assistant and the general concepts of the local smart home as well as open-source soft- and hardware. We discussed many options. Simple WiFi and Zigbee relays (like shelly and others), as well as wired approaches (like KNX) were taken into consideration. We agreed that a wireless setup would not make use of the potential a newly built home provides. Wired bus-based solutions like KNX, would lock him in forever and a truly “dumb home” would from there on not be possible as you have to rely on the bus routed throughout your home. The only type of solution which came close, was to use a lot of shelly pro devices (DIN rail mountable shellies) and wire all lights/blinds/etc. back to the control cabinet. Such a solution would “hardwire” input switches to specific devices though. While calculating the cost of using shellies, I came up with the idea of creating an ESPhome based solution. Basically an ESP32 on steroids making use of dozens of IOs. We settled on using ESPHome not only because of the price difference but also because I always wanted to create such a behemoth of a system.

## Buying guide for the Onager

This section will be completed soon! Come back later to see how and where you will be able to get all necessary components for creating your own Onager controller!

## FAQs
### Who is the Feudal project for?
It’s for people who:
- want to have a fully local smart home.
- want to have an open source smart home.
- want to have a central smart home and are willing to wire everything necessary towards that central point (or multiple, if you scatter the controllers around your home).
- want to have a smart home with ESPHome at the core, with all its perks and problems.
- want a DIY smart home, to fully create a unique experience.
- are prepared to take responsibility for the functionality of their smart home and are aware of their accountability towards the other residents of the home.
- don’t have a fundamental problem with things needing a bit of tweaking and maintenance now and then.
- are able to test as much of their setup before it gets implemented into the house.
- have basic to advanced skills in soldering and have already successfully completed a few ESPHome projects.
- do have a 3D printer or at least know how to get things printed elsewhere.

Do you recognize yourself above? That’s great! You should be good to go for this project! If not, just tell me about your concerns in the [Q&A discussion section](https://github.com/Feudal-Project/Onager/discussions/categories/q-a), I will try to help you to make the right decision!

### What is the idea behind the Onager?
The main idea is to create an ESP32 based DIN rail mountable controller, which is connected to your Home Assistant locally over ethernet. To control your appliances you need additionals modules, like the [Trebuchet IO module](https://github.com/Feudal-Project/Trebuchet). The Onager itself does not have controllable outputs by itself.

### Why are there no Gerber files or project file?
This question is absolutely valid and should not be dismissed or ignored! I created this module after spending many hours of my personal time, both while studying at university and later working a full-time job. Therefore, I personally believe it is fair to make the module available only through a PCB manufacturer that credits my work with a small percentage of the revenue (with no extra cost to you). This way, you can order your PCBs (and even select a few parameters, such as color, etc.) from a well-known manufacturer, while I receive a small commission for my design work. If you still need the production files, however, I believe you're capable of designing your own PCB.

## Wiring
Wiring your Onager only includes supply 24V power and connecting the ethernet cable. To power other module, simply connect them via the side connector. To find out more about wiring look at the wiring section of the [trebuchet](https://github.com/Feudal-Project/Trebuchet#wiring)

<p align="center">
  <img src="/images/Treb-Onager-simple-schematic.png" width="80%">
  <img src="/images/Treb-Onager-simple-schematic-cover.png" width="80%">
</p>

## ESPHome configuration
The Onager is uses a ESP32 POE with **16MB** of flash made by [Olimex](https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/open-source-hardware). All configurations specific for the onager, can be included as a remote package. Simply include the code below into your config (look [here](https://esphome.io/components/packages.html#packages-as-templates) for more info about ESPHome packages). For a complete ESPHome config, including 4 [Trebuchet modules](https://github.com/Feudal-Project/Trebuchet), look at the basic example provided [here](https://github.com/Feudal-Project/Onager/blob/main/esphome/examples/onager_complete.yaml). Keep in mind to follow the [guide](https://github.com/Feudal-Project/Trebuchet#esphome-configuration) to include the Trebuchet.

## Cost
The cost of implementing the feudal project will be highly unique to your home, because the wiring cost will be by far the highest expense! Therefore you should consult an electrician for pricing on that topic, if you are not doing it on your own.

Concerning the cost of the modules and the needed additional hardware, a rough estimation is below (prices were looked up in January of 2025)

#### Component Price (excluding shipping)
- 150W Meanwell Power supply (for 1 Onager, 4 [Trebuchets](https://github.com/Feudal-Project/Trebuchet) and many relays): ~40€
- One [Trebuchet](https://github.com/Feudal-Project/Trebuchet) modul including all the necessary components (excluding the casing):  ~15-20€ **will be updated soon!** (depending on the number of modules you order)
- [Trebuchet](https://github.com/Feudal-Project/Trebuchet) casing printed at home: ~5€
- One Relay (16A, 24V): ~10€
- One Onager: **will be updated soon!**
- Wall switches: entirely up to you!

#### Setup Price (excluding shipping)
A small setup (64 Inputs, 64 Outputs) would cost somewhere around 700-800€, without the wall switches and excluding shipping and wiring costs. As an example, 16 Shelly Pro 4PM (comparable in terms of IO, but having additional power measurement) would land you around 1.800€. If you don’t need power measurement and want to create your own system on a budget, the Feudal project is a valid alternative.