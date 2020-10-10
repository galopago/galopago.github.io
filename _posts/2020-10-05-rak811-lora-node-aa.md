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

<figure>
	<a href="/assets/images/RAK811_NODE_OPEN.JPG"> <img src="/assets/images/RAK811_NODE_OPEN.JPG"> </a>
	<figcaption>Lora Node inside waterproof case</figcaption>
</figure>

#### Key features:
* Open source Hardware & Software
* Powered by 2xAA (1.5v) batteries or a single (3.0v) battery.**
* Waterproof if installed in an "easy to find worldwide" 83x58x33mm waterproof plastic enclosure (multiple choices: clear cover, wall mounting tabs, etc.).
* Class A battery powered or Class C external powered via screw terminal.
* RAK811 = SX1276+STM32L151. So no additional cpu/microcontroller needed for a complete solution.
* Can be programmed using RAK Unified Interface (RUI) API, for rapid development or STM32 CUBE LoRa stack.
* TH pad for a spring antenna or U.FL connector for external antenna.
* Prototyping/expansion area.

#### Bill Of Materials

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| RAK811 LoRa Module    | [💸](#)     | [RAK811.pdf](/assets/pdf/RAK811.pdf)           |
| Generic 83x58x33mm waterproof enclosure box (wall mounting tabs, clear cover options available)    | [☢](#)  | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf)                               |
| M2.6 self-tapping B-type screw    | [💸](#)     | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)           |
| Single AA battery holder for pcb mounting | $100M  | [BH311.pdf](/assets/pdf/BH311.pdf) | 
| Screw terminal kf350 3.5mm 3 pin | $100B  | [KF350.pdf](/assets/pdf/KF350.pdf)                           |
| Spring antenna for 433,868,915 mhz| $100B  | [SW433-TH32.pdf](/assets/pdf/SW433-TH32.pdf) [SW868-TH06.pdf](/assets/pdf/SW868-TH06.pdf) [SW915-TH12.pdf](/assets/pdf/SW915-TH12.pdf)
| Female header 2.54mm  | $100B  | [FHA3-SXX.pdf](/assets/pdf/FHA3-S1XX.pdf)                           |
| Male pin header 2.54mm  | $100B  | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf)                           |

| PCB    | Get yours! | Source files                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Main circuit board    | [💸](#)     | [RAK811 LORA ADAPTABLE NODE](https://github.com/galopago/RAK811_LORA_ADAPTABLE_NODE)           |
| Female header 2.54mm  | $100B  | [RAK LORA ADAPTABLE NODE BREAKOUT 2AA](https://github.com/galopago/RAK_LORA_ADAPTABLE_NODE_BREAKOUT_2AA)        |

| Software    | Get yours! | Source files                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Main circuit board    | [💸](#)     | [RAK811 RUI SWITCH SENSOR](https://github.com/galopago/RAK811_RUI_SWITCH_SENSOR)           |


Of course the Neverlands vary a good deal. John's, for instance, had a lagoon with flamingoes flying over it at which John was shooting, while Michael, who was very small, had a flamingo with lagoons flying over it. John lived in a boat turned upside down on the sands, Michael in a wigwam, Wendy in a house of leaves deftly sewn together. John had no friends, Michael had friends at night, Wendy had a pet wolf forsaken by its parents, but on the whole the Neverlands have a family resemblance, and if they stood still in a row you could say of them that they have each other's nose, and so forth. On these magic shores children at play are for ever beaching their coracles [simple boat]. We too have been there; we can still hear the sound of the surf, though we shall land no more.

Of all delectable islands the Neverland is the snuggest and most compact, not large and sprawly, you know, with tedious distances between one adventure and another, but nicely crammed. When you play at it by day with the chairs and table-cloth, it is not in the least alarming, but in the two minutes before you go to sleep it becomes very real. That is why there are night-lights.

Occasionally in her travels through her children's minds Mrs. Darling found things she could not understand, and of these quite the most perplexing was the word Peter. She knew of no Peter, and yet he was here and there in John and Michael's minds, while Wendy's began to be scrawled all over with him. The name stood out in bolder letters than any of the other words, and as Mrs. Darling gaze