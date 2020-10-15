---
title: "RAK811 based LoRa Node powered by AA batteries"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN000
  - LoRaWAN
header:
     teaser: "/assets/images/RAK811_NODE_OPEN_TEASER.jpg"
---

LoRa node conceived for experimentation. Easy to interface to multiple kind of sensors. Designed to fit
inside a generic waterproof enclosure, just add a pair of AA alkaline batteries and deploy!

Core component: [RAK811 LoRa module.](#)
{: .notice--danger}

<figure>
	<a href="/assets/images/RAK811_NODE_OPEN.jpg"> <img src="/assets/images/RAK811_NODE_OPEN.jpg"> </a>
	<figcaption>Lora Node inside waterproof case</figcaption>
</figure>


#### Key features:
* Open source Hardware & Software
* Powered by 2xAA (1.5v) batteries.
* Waterproof & wall mountable.
* RAK811=SX1276+STM32L151. No additional μC needed.
* Build environment: RAK RUI API, or STM32 CUBE LoRa stack.
* Prototyping/expansion area.
* Pad for a spring antenna or U.FL connector for external ant.


#### Bill Of Materials

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| RAK811 LoRa Module    | [💸](#)     | [RAK811.pdf](/assets/pdf/RAK811.pdf)           |
| Generic 83x58x33mm waterproof enclosure box (wall mounting tabs, clear cover options available)    | [💸](#)  | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf)                               |
| M2.6 self-tapping B-type screw    | [💸](#)     | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)           |
| Single AA battery holder for PCB mounting | [💸](#)  | [BH311.pdf](/assets/pdf/BH311.pdf) | 
| Screw terminal kf350 3.5mm 3 pin | [💸](#)  | [KF350.pdf](/assets/pdf/KF350.pdf)                           |
| Spring antenna for 433,868,915 MHz| [💸](#)  | [SW433-TH32.pdf](/assets/pdf/SW433-TH32.pdf) [SW868-TH06.pdf](/assets/pdf/SW868-TH06.pdf) [SW915-TH12.pdf](/assets/pdf/SW915-TH12.pdf)
| Female header 2.54mm  | [💸](#)  | [FHA3-SXX.pdf](/assets/pdf/FHA3-S1XX.pdf)                           |
| Male pin header 2.54mm  | [💸](#)  | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf)                           |

#### Printed Circuit Boards

| PCB    |  Source files                                          | 
| -------- | ------------------------------------------------------------ |
| Main circuit board     | [RAK811 LORA ADAPTABLE NODE](https://github.com/galopago/RAK811_LORA_ADAPTABLE_NODE)           |
| Breakout/expansion  | [RAK LORA ADAPTABLE NODE BREAKOUT 2AA](https://github.com/galopago/RAK_LORA_ADAPTABLE_NODE_BREAKOUT_2AA)        |

#### Software

| Software    | Source files                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [RAK811 RUI SWITCH SENSOR](https://github.com/galopago/RAK811_RUI_SWITCH_SENSOR)           |

### Customization
The project is divided in four main aspects: power source, enclosure, antenna and expansion which can be modified for the exact requirements. Finally a sample application is given as a way to show how to implement your own sensor solution.

##### Power source
The device can work from 1.8v up to 3.7v. There are many alternatives to power it:
* 2 x AA alkaline batteries. JP1 jumper positions 1-2 shorted.
* 1 x 14500 lithium battery. JP1 jumper positions 2-3 shorted. The BT2 battery holder could be removed, freeing up some PCB space.
* External power applied to J1 screw terminal. BT1 and BT2 battery holders could be removed, freeing up even more PCB space.

##### Enclosure
The PCB fits inside a "generic" unbranded **83x58x33mm** waterproof plastic enclosure. These enclosures came in multiple flavors: gray, white, black, clear lid, wall mounting tabs. The board is fixed to the enclosure by two self tapping screws.

##### Expansion

<figure class="half">
	<a href="/assets/images/RAK811_NODE_EXPANSION.jpg"> <img src="/assets/images/RAK811_NODE_EXPANSION.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_PINOUT.png"> <img src="/assets/images/RAK811_NODE_PINOUT.png"> </a>
	<figcaption>PCB expansion area</figcaption>
</figure>

The prototyping area contains through hole soldering pads routed to all pins of RAK811 module, plus  some small amount of free connected pads for prototyping. Connections for outside detachable sensors are provided via W,X,Y,Z screw terminals. If the vast prototyping area isn't enough, female pin headers could be soldered and an expansion board could be plugged in.
Notice that RAK811-LF and RAK811-HF have slighter differences in some i/o pins


##### Antenna options
Internal spring antena soldered on J6, JP2  jumper positions 1-2 shorted.  
External antenna using U.FL. connector, JP2 jumper positions 2-3 shorted. 

##### Sample application

<figure class="third">
	<a href="/assets/images/RAK811_NODE_RESISTORS.jpg"> <img src="/assets/images/RAK811_NODE_RESISTORS.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_REEDSWITCH.jpg"> <img src="/assets/images/RAK811_NODE_REEDSWITCH.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_CLOSED.jpg"> <img src="/assets/images/RAK811_NODE_CLOSED.jpg"> </a>
	<figcaption>Magnetic Switch LoRa sensor node</figcaption>
</figure>

The sample applications consist in a LoRa magnetic switch sensor which transmits a packet when the switch opens or closes. A very small reed switch is installed in one of the walls inside enclosure.
Breakout board  was used to install the supplementary electronic components: Led indicator, pullup resistors, test button, and voltage divider for battery monitoring. 

Any other kind of switch sensor (ball inclination sensor, spring vibration sensor, etc.) could be added!

PVDF wire was used to make connections because the insulation resists pretty well soldering iron abuse!. 
For more information about the PCB or the firmware, don't forget to read the [linked repositories.](/#printed-circuit-boards)
 

## Additional components:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 30 AWG wire wrap UL1423 PVDF cable    | [💸](#)     | [UL1423.pdf](/assets/pdf/UL1423.pdf)           |
| U.FL smd external antenna conector    | [💸](#)     | [6474011114.pdf](/assets/pdf/6474011114.pdf)           |
| Plastic small red switch     | [💸](#)  | [GPS-11A.pdf](/assets/pdf/GPS-11A.pdf)                               |
| Magnet with screw tabs for wall mounting     | [💸](#)  | [MC-38.pdf](/assets/pdf/MC-38.pdf)                               |
| Vibration spring sensor | [💸](#)  | [SW-18015p.pdf](/assets/pdf/SW-18015p.pdf)                               |
| Tilt ball sensor     | [💸](#)  | [SW-200D.pdf](/assets/pdf/SW-200D.pdf)                               |
| 1/4W 1%  TH Resistors    | [💸](#)  | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf)                               |
| 3mm led    | [💸](#)  | [1254-10SYGD.pdf](/assets/pdf/1254-10SYGD.pdf)                               |
| push button    | [💸](#)  | [TS-1301.pdf](/assets/pdf/TS-1301.pdf)                               |
                     