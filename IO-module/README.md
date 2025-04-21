# IO module

The IO module is a DIN rail mountable input output module which can be connected to the [controller](https://github.com/Feudal-Project/OpenDINRail/tree/main/Controller-module) module. It is intended as a DIY project for anyone who is already familiar with ESPHome and has a basic to advanced level of soldering skills.

## Features

- 16 24V inputs
- 16 24V low side switching outputs functioning as relay drivers (integrated flyback diode).
- Side connector for daisy chaining up to 4 IO modules.
- Galvanic isolated input and output rows to prevent cascading damage throughout daisy chained devices.
- 3D printable housing with engraved port descriptions and DIN Rail compatibility with 3D printed locking keys.
- Highly versatile in its use due to the vast possibilities of ESPHome.

<p align="center">
  <img src="/images/IO-module.jpg" width="50%">
</p>

## FAQs
### What is the idea behind the IO module?
The main idea is to connect any appliance controllable by a switch, and any type of sensor providing a binary output to this module. The ESPHome configuration on the [controller](https://github.com/Feudal-Project/OpenDINRail/tree/main/Controller-module) module will awaken the system and let the magic happen!

### What exactly can be connected to the IO module?
The following appliances can (usually) be controlled via relays and therefore get connected to the IO module:
- Basic lights.
- Blinds/covers with separate control wires for up/down (most of them do). If you are unsure, ask a question in the [Q&A discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a), or consult your local electrician.
- Garage doors which are capable of being wired to a wall switch.
- Any type of binary valve, like in floor heating valves.
- Many more ESPHome components which use a binary output at the core.

The following devices can be sensed by the IO module:
- Static and momentary wall switches.
- Any type of binary window sensor (switch-based, reed contact).
- Basic motion sensors (PIRs) outputting a binary value.
- Floating switches for water level measurement.
- Many more ESPHome components which use a binary input at the core.

You found another use for the IO module? Awesome! Share it in the [ideas discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/ideas) so others can benefit from your discovery!

## Wiring
In the light installation schematic below, the typical wiring of a normal wall switch, and the light itself is shown. Commercial systems you typically get on the market do not split the system into distinct parts, as I did for the feudal project. A shelly device for example usually concludes powersupply, controller, relay driver and the relay itself into one device. The all in one approach will result in a smaller footprint inside the cabinet, but will be less repairable.

Most of the setup uses 24V as a supply voltage, which makes it safer for humans. Most countries recognize this safety advantage and therefore do not regulate this type of wiring as much as typical household voltage (230V/110V). Therefore, it most likely is allowed for you to work with this voltage at home while not breaking any code or insurance terms (Disclaimer: I do not know your specific situation and I also won’t defend you in any way, if you break your local rules. Do your own research or consult a local electrician!).

The benefit this will give you is to be able to set up the whole system yourself and repair it yourself. The only parts which need to be worked by an electrician is wiring the 230V/110V devices towards the respective relay.

You may ask yourself what benefit this really provides you. Simple answer: Your typical electrician will most likely not be willing to install your favorite smart home system (like shellies or so on). Most often, you need to get in contact with an electrician which has also some sort of IT knowledge and knows your system of choice while also being willing to take the accountability of the installation. With the feudal project, the work for the electrician is simplified to a degree any electrician can handle, and you yourself are able to setup everything the way you want it to.

<p align="center">
  <img src="/images/OpenDINRail-simple-schematic.png" width="80%">
  <img src="/images/OpenDINRail-simple-schematic-cover.png" width="80%">
</p>

## Component selection

### Relay
Most simple appliances can be controlled via a relay. In order to find the best relay for your usecase, a few things need to be considered.

First of all (and most importantly), the relay needs to work with your low voltage level. At the moment the only voltage level for the IO module is 24V DC, so make sure, your relay works with this voltage level at the input ports. 

Another important metric is the current rating of the relay. If you power a simple light fixture, a relay capable of 4 or 8A might be enough. If you wish to control an electric heater, you will most likely need a relay able to supply 16A. All in all, you need to make sure to use a correctly rated relay for your usecase. If you are unsure, ask a question in [Q&A discussion section] (https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a) or consult a local electrician for help.

To minimize your own electric bill, you might want to take a look at the electric consumption of the relay itself. Most of the time, the wattage needed by the relay is stated in the datasheet, but more often than not, this value is a bit higher then what it actually needs. If you want to minimize your consumption, you have to order the relay and measure it yourself with a multimeter. You can also take a look at the comparison table in the 
section. Another option to minimize the relays power consumption can be to use impulse controlled relays. These can be more expensive money wise as well as memory wise. But then ESPHome has to keep track of the current state of the relays, because there is no way for the IO module to know, if the relay is on, or off.

### Power supply
Your power supply selection is mainly influenced by the number of relays and the power needed by the relay itself. The voltage needs to be 24V DC, as no other voltage is supported by the IO module at the moment.

I would suggest you choose a power supply from a reputable brand (like Meanwell), because going cheap on this one, will lead to unstable states. In my opinion 20-40€ more on a power supply which most likely will last for 10 years or more are reasonable, compared to a cheap one, which my start to produce coil noises and goes dead in 2-3 years.

**Formular to calculate power supply wattage:**
`Wattage = Number of IO module * 16 * (wattage of relays + 0,084W) + 10W`

With the formular above, you will get a number which should work for your setup in the worst case (all outputs are on, and all switches are closed). This use case is more than unlikely, but you can be sure it’ll work!

If the wattage is above any power supply which you can get a hold of, simply split the power line. Use a power supply for only one or two IO modules and connect their grounds together. This is possible, because the input and output circuitry is galvanically isolated from the driving logic. If you are unsure, just ask a question in [Q&A discussion section](https://github.com/Feudal-Project/OpenDINRail/discussions/categories/q-a).

### Wall switches
You can choose between two types of switches typically. The first option (which is used most often), is the toggle switch. It can get turned on or off, which causes to change the permanent state inside of ESPHome. The momentary switch will flick back into its position as soon as the user releases the switch. As a result, ESPHome will see a short pulse at the input signal.

The answer to which is right for you is simple. If you want to be able to rip out the Smart System and use only the switches and relays later, you should use toggle switches, so that the relays stay on and if the switch is “turned on”. If you want to get the most out of the multiclick feature and hate the fact that a toggle switch might not represent the actual state of the output, you should get momentary switches. Even if you choose momentary switches and want to rip out the feudal project later on, you could just buy toggle switches (to replace the momentary ones), or impuls relays (to replace the normal relays).
