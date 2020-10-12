---
title: "RAK811 based LoRa Node powered by AA batteries"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN000
  - LoRaWAN
---

En un inicio este post ll children, except one, grow up. They soon know that they will grow up, and the way Wendy knew was this.
experimental but strong but usefull

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
* RAK811=SX1276+STM32L151. no additional uC needed.
* Build environment: RAK RUI API, or STM32 CUBE LoRa stack.
* Prototyping/expansion area.
* Pad for a spring antenna or U.FL connector for external ant.


#### Bill Of Materials

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| RAK811 LoRa Module    | [💸](#)     | [RAK811.pdf](/assets/pdf/RAK811.pdf)           |
| Generic 83x58x33mm waterproof enclosure box (wall mounting tabs, clear cover options available)    | [💸](#)  | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf)                               |
| M2.6 self-tapping B-type screw    | [💸](#)     | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)           |
| Single AA battery holder for pcb mounting | [💸](#)  | [BH311.pdf](/assets/pdf/BH311.pdf) | 
| Screw terminal kf350 3.5mm 3 pin | [💸](#)  | [KF350.pdf](/assets/pdf/KF350.pdf)                           |
| Spring antenna for 433,868,915 mhz| [💸](#)  | [SW433-TH32.pdf](/assets/pdf/SW433-TH32.pdf) [SW868-TH06.pdf](/assets/pdf/SW868-TH06.pdf) [SW915-TH12.pdf](/assets/pdf/SW915-TH12.pdf)
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


#### Power source
The device can work from 3.7v down to 1.8v. There are many alternatives to power it:
* 2 x AA alkaline batteries. JP1 jumper positions 1-2 shorted
* 1 x 14500 lithium battery. JP1 jumper positions 2-3 shorted. BT2 battery holder could be removed freeing up some pcb space.
* External power applied to J1 screw terminal. BT1 and BT2 battery holders could be removes freeing up even more pcb space.
battery connected to module pins

#### Enclosure
The PCB fits inside a "generic" unbranded 83x58x33mm waterproof plastic enclosure. Theese enclosures came in multiple flavors: gray, white, black, clear lid, wall mount tabs. The board is fixed to the enclosure by two self tapping screws.

#### Expansion

<figure class="half">
	<a href="/assets/images/RAK811_NODE_EXPANSION.jpg"> <img src="/assets/images/RAK811_NODE_EXPANSION.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_PINOUT.png"> <img src="/assets/images/RAK811_NODE_PINOUT.png"> </a>
	<figcaption>PCB expansion area</figcaption>
</figure>

The prototyping area contains TH pads connected to all pins of RAK811 module, plus  some small amount of free connected pads for prototping. Conections for outside sensors are provided via W,X,Y,Z screw terminals. If the vast prototyping area isn't enough, female pin headers cold be soldered and an expansion board could be plugged in.
note that RAK811-LF and RAK811-HF have sligter differences in some i/o pins


#### Antenna options
Internal spring antena soldered on J6, JP2 1-2 pins must be shored.  
External antenna using U.FL. connector, JP2 2-3 pins must be shorted. 

#### Sample application

<figure class="third">
	<a href="/assets/images/RAK811_NODE_RESISTORS.jpg"> <img src="/assets/images/RAK811_NODE_RESISTORS.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_REEDSWITCH.jpg"> <img src="/assets/images/RAK811_NODE_REEDSWITCH.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_CLOSED.jpg"> <img src="/assets/images/RAK811_NODE_CLOSED.jpg"> </a>
	<figcaption>Magnetic Switch LoRa sensor node</figcaption>
</figure>

switch based sensor , vibrating sensors, ball sensors, fw descpription
cut headers (link) PVDF cable dont melt soldering ( link)
generic magnetic switch too big inside, so small reed switch used
led lights on transmission can be turned off by downkink
pushbutton test tx in case external sensor inaccesible

## Additional components:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 30 AWG wirewrap UL1423 PVDF cable    | [💸](#)     | [UL1423.pdf](/assets/pdf/UL1423.pdf)           |
| U.FL smd external antenna conector    | [💸](#)     | [6474011114.pdf](/assets/pdf/6474011114.pdf)           |
| plastic small red switch     | [💸](#)  | [GPS-11A.pdf](/assets/pdf/GPS-11A.pdf)                               |
| magnet with screw tabs for wall mounting     | [💸](#)  | [MC-38.pdf](/assets/pdf/MC-38.pdf)                               |
| vibration sensor (wall mounting tabs, clear cover options available)    | [💸](#)  | [SW-18015p.pdf](/assets/pdf/SW-18015p.pdf)                               |
| ball sensor inclination sensor    | [💸](#)  | [SW-200D.pdf](/assets/pdf/SW-200D.pdf)                               |

                     

Occasionally in her travels through her children's minds Mrs. Darling found things she could not understand, and of these quite the most perplexing was the word Peter. She knew of no Peter, and yet he was here and there in John and Michael's minds, while Wendy's began to be scrawled all over with him. The name stood out in bolder letters than any of the other words, and as Mrs. Darling gaze