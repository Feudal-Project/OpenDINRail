# OpenDINRail
OpenDINRail is a DIY open source DIN rail mountable smart home system based on ESPHome. It can control any on/off appliance and can sense any switch-like input. It consists of two different modules, one being an ethernet connected esp32 based controller, the other being an input-output module able to control relays, and sense binary outputs.

<p align="center">
  <img src="/images/intro-picture.png" width="50%">
</p>

# Table of Contents
1. [Buying guide for the IO module](buying-guide-for-the-io-module)
2. [Background](#background)
3. [FAQs](#faqs)
4. [ESPHome configuration](#esphome-configuration)
5. [Cost](#cost)

## Buying guide for the OpenDINRail project

This section will be completed soon! Come back later to see how and where you will be able to get all necessary components for creating your own IO module!

## Background
In 2023 I had the opportunity to work on a smart home for a house being newly built at that time. The owner is a big fan of Home Assistant and the general concepts of the local smart home as well as open-source soft- and hardware. We discussed many options. Simple WiFi and Zigbee relays (like shelly and others), as well as wired approaches (like KNX) were taken into consideration. We agreed that a wireless setup would not make use of the potential a newly built home provides. Wired bus-based solutions like KNX, would lock him in forever and a truly “dumb home” would from there on not be possible as you have to rely on the bus routed throughout your home. The only type of solution which came close, was to use a lot of shelly pro devices (DIN rail mountable shellies) and wire all lights/blinds/etc. back to the control cabinet. Such a solution would “hardwire” input switches to specific devices though. While calculating the cost of using shellies, I came up with the idea of creating an ESPhome based solution. Basically an ESP32 on steroids making use of dozens of IOs. We settled on using ESPHome not only because of the price difference but also because I always wanted to create such a behemoth of a system.

## FAQs
### Who is OpenDINRail for?
It’s for people who:
- want to have a fully local smart home.
- want to have an open source smart home.
- want to have a central smart home and are willing to wire everything necessary towards that central point (or multiple, if you scatter the controllers around your home).
- want to have a smart home with ESPHome at the core, with all its perks and problems.
- want a DIY smart home, to create a fully unique experience.
- are prepared to take responsibility for the functionality of their smart home and are aware of their accountability towards the other residents of the home.
- don’t have a fundamental problem with things needing a bit of tweaking and maintenance now and then.
- are able to test as much of their setup before it gets implemented into the house.
- have basic to advanced skills in soldering and have already successfully completed a few ESPHome projects.
- do have a 3D printer or at least know how to get things printed elsewhere.

Do you recognize yourself above? That’s great! You should be good to go for this project! If not, just tell me about your concerns in the [Q&A discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a), I will try to help you to make the right decision!

### What exactly can be connected to the OpenDINRail system?
The following appliances can (usually) be controlled via relays and therefore get connected to the IO module (XXX Link):

- Basic lights.
- Blinds/covers with separate control wires for up/down (most of them do). If you are unsure, ask a question in the [Q&A discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a), or consult your local electrician.
- Garage doors which are capable of being wired to a wall switch.
- Any type of binary valve, like infloor heating valves.
-  Many more ESPHome components which use a binary output at the core.

The following devices can be sensed by the IO module:
- Static and momentary wall switches.
- Any type of binary window sensor (switch-based, reed contact).
- Basic motion sensors (PIRs) outputting a binary value.
- Floating switches for water level measurement.
- Many more ESPHome components which use a binary input at the core.

You found another use for the OpenDINRail system? Awesome! Share it in the [ideas discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/ideas) so others can benefit from your discovery!

### What is possible with the OpenDINRail system at the base of my ESPHome setup?
The possibilities of using the OpenDINRail system are close to limitless, due to the sheer number of ESPHome components relying on basic binary inputs and outputs. Nonetheless here are a few examples of typical use cases:

- Using double press on your blind switch, to lower them all the way and tilt them to 50%
- Using long press on a light switch to apply a specific scene, which lowers the blinds, sets the lights to 30% and turns on the TV
- Using a window sensor to automatically turn off the valve for the heating in that room
- Using a PIR to turn on the light if someone is home or send a Home Assistant notification if no one should be home.
- Using five quick presses to activate the house alarm on any light switch all over the home
- Turn down the blinds if a window is left open for an extended period of time.

### Why should I use the OpenDINRail system instead of other solutions?
If the points listed in “Who is OpenDINRail for?” are more a nice to have than a must for you, this system is probably not for you. Nonetheless, here are a few reasons why I think you should still consider this system over others available on the market:

- It allows you to strip out the whole system and use your home without any smartness, if you keep a few important points in mind (see [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module) for more information).
- Very few other systems can be setup so cheaply (see the [Cost section](#cost) for more information).
- Many systems rely on some sort of network connection between them. This system can handle a decently sized flat or even a small home all on one controller. A system more centralized than this is hard to find!
- Define everything yourself! You are a quick with your Fingers? Just set the double press timeout to 20ms, and no one can trigger the scene except you! You are not as fit as you might once were? Set the triple press on any wall switch to send an emergency message to someone over Home Assistant or else. The possibilities are endless, and no company can tell you what to do next, it’s all up to you!
- Modularity at its best! You hate to throw away working tech, even if only one aspect does not work any longer? Just replace it, or even better: get your soldering iron out and repair it yourself using the schematics and information provided here!

### What else is possible with this system?
Being open source, you can create your own modules and attach them to the controller. To learn more about the capabilities of the controller module, look [here](https://github.com/Feudal-Project/OpenDINRail/tree/main/Controller-module).

### Why are there no Gerber files or a general project file?
This question is absolutely valid and should not be dismissed or ignored! I created this system after spending many hours of my personal time, both while studying at university and later working a full-time job. Therefore, I personally believe it is fair to make the module available only through a PCB manufacturer that credits my work with a small percentage of the revenue (with no extra cost to you). This way, you can order your PCBs (and even select a few parameters, such as color, etc.) from a well-known manufacturer, while I receive a small commission for my design work. If you still need the production files, however, I believe you're capable of designing your own PCB.

### How exactly do I get started?
Now that you have chosen to create your own OpenDINRail setup, let me guide you through the steps. Read all of them, before doing anything!

**Imagine your setup**

First of all, you have to imagine your system and think of anything that you want to connect to it. This step is crucial for you to be happy with the end result. It doesn't matter if you built an completely new home, or just want to have the worlds smartest shed in the backyard. Imagine every output and input, and list them as detailed as necessary. Take your time to really think about it! This system being hardwired, makes it really hard to add stuff late on.

**Divide and conquer**

If you are designing the system for an entire house, it will most likely be necessary to implement more then one controller module. With one controller being able to support 64 inputs and 64 outputs, dividing your endless list into multiple controllers can be quite hard. As a first step, you should think of Outputs and Inputs which will be used together more often then not. Using one controller for shades, and another for Lights therefore might make sense to you. Separating the system by floor or area can also be useful, if you plan to place the controllers apart from each other.

**Get to know the cost**

Knowing the cost before going any further will be useful. With the OpenDINRail system being hardwired, wires are most likely the most expensive part of it all. Consult a local electrician for pricing and thing about good places to hide the electric cabinet. Splitting the setup into areas of floors, might save a lot in wiring! For a rough estimation of component cost, look at the [cost section](#cost)

**Test your system in a safe space**

Although the modules are tested and have proven to work for myself, there is no guarantee for them to work in your scenario. Components outside of the modules (like relays, switches, door window contacts, valves, etc.) can simply have a very big impact on the system. So get yourself one or two of every component you plan to connect to the system, as well as at least one controller and IO module and just test it. If you have any questions are unsure about component selection, consult a local electrician or write an entry into the [Q&A section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a)

**Wire everything up**

Now the great wiring takes place. Make sure you keep a clear mind and don't stress yourself. Being impatient will lead to errors, which will end in broken parts! Wiring up a view hundred wires, will take time, so enjoy the process or consult an electrician which is willing to help you out. I personally believe that, being overwhelmed by the thought of wiring this yourself, is a great indicator for you not being ready for such a project yet. Just take your time to learn the subject, or use an of the shelve system.

**Configure the controllers**

At last, program all your controllers and configure everything to your liking. Read the [ESPHome section](#ESPHome-configuration) for more.

## ESPHome configuration
The OpenDINRail system uses a ESP32 POE with **16MB** of flash made by [Olimex](https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/open-source-hardware). The unusual large flash size is necessary in order to support such a high number of inputs and outputs. A ESPHome configuration for the OpenDINRail system is highly unique, so there is no real plug and play solution. With ESPHome improving on their ability to share device configurations, we can get close to an easy implementation, but with only you knowing which input is a switch, or just a door sensor (for example) you will always need to program the system yourself!
Nonetheless, I tried to increase ease of use, as much as possible. Therefore, I created [packages](https://esphome.io/components/packages.html) and [templates](https://esphome.io/automations/templates.html) which can be used to create your custom config. Keep in mind, that you have to use both the controller as well as the IO packages/templates in order to get the system working.

**If you want a copy paste example for testing, simply look [here](https://github.com/Feudal-Project/OpenDINRail/blob/main/Controller-module/esphome/examples/opendinrail_complete.yaml)**

### Controller config
The controller is the heart of any ESPHome config, not only because there can be only one of it, but because it controls the entire system, and all IO modules depend on it. The following lines contain everything necessary for the controller module to function by itself.

````
esphome:
  name: OpenDINRail

# Enable logging
logger:

# Enable Home Assistant API
api:
  password: !secret api_key

# Enable OTA
ota:
  - platform: esphome
    password: !secret ota_password

web_server:
  port: 80

packages:
  remote_package_shorthand: github://Feudal-Project/OpenDINRail/Controller-module/esphome/packages/controller_basics.yaml@main
````

The remote package contains all the necessary configs to make use of the ethernet port, the I2C Bus, as well as the whole 16MB of flash. (NOTE: If you buy a 4MB version, this package will lead to strange behavior or even errors!)

### IO module config
The IO module makes use of a template, which defines all the inputs and outputs, while providing substitutions for customization. With ESPHome being not able to use external packages as a template at the moment, you need to download the files located [here](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module/esphome/packages) and copy them in your ESPHome directory. An explanation on where you can find your ESPHome directory, can be looked up [here](https://esphome.io/guides/getting_started_hassio.html#device-builder-interface). To know more about ESPHome packages look [here](https://esphome.io/components/packages.html#packages-as-templates) for official information.  The package allows you to configure each input/output with the following parameters:

- ***Module_Name:***
Name your module to your liking.

- ***Module_I2C_Address_input:***
This parameter is the I2C address of the input side of the module. Valid values are between *0x20* and *0x27*. The address must be unique over the whole ESPHome configuration and can be set on the module at the side via the dip switches. A picture explaining how to set the address can be found below.

- ***Module_I2C_Address_output:***
This parameter is the I2C address of the output side of the module. Valid values are between *0x20* and *0x27*. The address must be unique over the whole ESPHome configuration and can be set on the module at the side via the dip switches. A picture explaining how to set the address can be found below.

- ***Outx:***
This parameter sets a part of the name and ID of the respective output (*Out0*-*Out15*). The name and ID of the output is a combination of *Module_Name* and *Outx* value separated with “_”. If you wish to reference the Output in a script, or automation reference it by its ID (<*Module_Name*>\_<*Outx*>)

- ***Outx_restore_mode:***
Set the restore mode of the output to a desired value. Look at the [official ESPHome configuration](https://esphome.io/components/switch/index.html#base-switch-configuration) for more details.

- ***Outx_interlock:***
Set the interlock parameter of the output to a desired value. Look at the [official ESPHome configuration](https://esphome.io/components/switch/gpio.html#interlocking) for more details.

- ***Outx_internal:***
Set the internal boolean of the output to a desired value. Look at the [official ESPHome configuration](https://esphome.io/components/switch/index.html#base-switch-configuration) for more details.

- ***Inx:***
This parameter sets a part of the name and ID of the respective input (*In0*-*In15*). The name and ID of the input is a combination of *Module_Name* and *Inx* value separated with “_”. If you wish to reference the input in a script, or automation reference it by its ID (<*Module_Name*>\_< *Inx* >)

- ***Inx_internal:***
Set the internal boolean of the input to a desired value. Look at the [official ESPHome configuration](https://esphome.io/components/binary_sensor/#base-binary-sensor-configuration) for more details.

<p align="center">
  <img src="/images/IO_module_cut_marked.jpg" width="80%">
</p>

Using the multiclick feature of ESPHome, it is possible to create your own click patterns. As a basis the IO module uses a simple package introducing single, double and long press click patterns. If you are missing features, you can always create your own. Keep in mind, that the configuration provided is a compromise between easy of use and customizability.

- ***Inx_script_singlepress:***
Set the script ID which should be called if a “singlepress” is recognized by the multiclick feature. Information about scripts can be found [here](https://esphome.io/components/script.html), while information about the multiclick feature can be found [here](https://esphome.io/components/binary_sensor/index.html#on-multi-click).

- ***Inx_script_doublepress:***
Set the script ID which should be called if a “doublepress” is recognized by the multiclick feature. Information about scripts can be found [here](https://esphome.io/components/script.html), while information about the multiclick feature can be found [here](https://esphome.io/components/binary_sensor/index.html#on-multi-click).

- ***Inx_script_longpress:***
Set the script ID which should be called if a “longpress” is recognized by the multiclick feature. Information about scripts can be found [here](https://esphome.io/components/script.html), while information about the multiclick feature can be found [here](https://esphome.io/components/binary_sensor/index.html#on-multi-click).

- ***Inx_on_press:***
Set the script ID which should be called if an “on press” is event is called by ESPHome. Information Information about scripts can be found [here](https://esphome.io/components/script.html), while information about the multiclick feature can be found [here](https://esphome.io/components/binary_sensor/index.html#on-multi-click).

- ***Inx_on_release:***
Set the script ID which should be called if an “on release” is event is called by ESPHome. Information about scripts can be found [here](https://esphome.io/components/script.html), while information about the multiclick feature can be found [here](https://esphome.io/components/binary_sensor/index.html#on-multi-click).

The package uses scripts, which get called if a specific event is triggered. Using this method, I was able to extract all the config code for an IO module, while also using the automation feature of ESPHome. At a first glance, the scripts might overcomplicate the configuration, but they allow to organize the configuration into different files and allow reuse. Examples of typical configurations can be found below.

````
packages:
  io_module_basics: !include 
    file: io_module_basics.yaml
  io_module1: !include 
    file: io_module.yaml
    vars:
      Module_Name: io_1
      Module_I2C_Address_input: 0x27
      Module_I2C_Address_output: 0x26
      In0_script_singlepress: example_script
  io_module2: !include 
    file: trebuchet_module.yaml
    vars:
      Module_Name: io_2
      Module_I2C_Address_input: 0x25
      Module_I2C_Address_output: 0x24
      In2_script_doublepress: example_script

script:
  - id: example_script
    then:
      - switch.turn_on: io_1_Out0
      - switch.turn_off: io_1_Out1
      - switch.turn_on: io_2_Out2
````

## Cost
The cost of implementing the feudal project will be highly unique to your home, because the wiring cost will be by far the highest expense! Therefore you should consult an electrician for pricing on that topic, if you are not doing it on your own.

Concerning the cost of the modules and the needed additional hardware, a rough estimation is below (prices were looked up in January of 2025)

#### Component Price (excluding shipping)
- 150W Meanwell Power supply (for 1 controller, 4 [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module) and many relays): ~40€
- One [IO module](https://github.com/Feudal-Project/OpenDINRail/tree/main/IO-module) including all the necessary components (excluding the casing):  ~15-20€ **will be updated soon!** (depending on the number of modules you order)
- module casing printed at home: ~5€
- One relay (16A, 24V): ~10€
- One controller module: **will be updated soon!**
- Wall switches: entirely up to you!

#### Setup Price (excluding shipping)
A small setup (64 Inputs, 64 Outputs) would cost somewhere around 700-800€, without the wall switches and excluding shipping and wiring costs. As an example, 16 Shelly Pro 4PM (comparable in terms of IO, but having additional power measurement) would land you around 1.800€. If you don’t need power measurement and want to create your own system on a budget, the OpenDINRail system is a valid alternative.