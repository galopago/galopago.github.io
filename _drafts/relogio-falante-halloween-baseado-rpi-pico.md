---
title: "Relógio falante de Halloween baseado no Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN003
  - RPI PICO  
  - C/C++ SDK
  - CIRCUITPHYTON
header:
     teaser: "/assets/images/HALLOWEEN_TALKING_CLOCK_TEASER.jpg.jpg"
---
Relógio falante de Halloween que toca sons a cada hora cheia. Apenas alguns componentes externos (fáceis de encontrar e soldar) são necessários. A placa de uma face pode ser fabricada em casa. Projeto altamente personalizável que envolve múltiplas áreas de conhecimento ([STEAM](https://en.wikipedia.org/wiki/STEAM_fields)): Eletrônica, programação, marcenaria, artes, etc.

Halloween talking clock that plays sounds every O'clock hour. Only a few external components (easy to source and solder) needed. The single side board could be manufactured at home. Very customizable project than involves multiple knowledge areas ([STEAM](https://en.wikipedia.org/wiki/STEAM_fields)): Electronics, programming, woodworking, arts, etc.

<figure>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MEDIUM.jpg"> </a>
	<figcaption>Customized clock hanging on a wall</figcaption>
</figure>

Key component: [Quartz clock movement with trigger](https://s.click.aliexpress.com/e/_AfCGIL)
{: .notice--danger}


##### Concept:

A lot of musical wall clocks on the market lacks the possibility of change original sounds. A clock with that capability can be built with an embedded system. But which one to choose? Raspberry Pi Pico was chosen for the 3 following reasons: 

* There's no need to install software for initial firmware download
* Onboard memory 2 MegaBytes of flash can store some amount of sounds without requiring external memory
* Can be powered by 2xAA batteries without additional components

Rpi Pico draws about 1.6 mA in it's lowest power mode (deep sleep). Seems not much, but is too high for a battery powered circuit, because they will exhaust in around two months. For that reason an external power circuit that can shut off the board completely was added. After that, power consumption lowered to 70 uA, so batteries will last for a year.

The Rpi Pico acts as sound storage and player. To show the time and generate an O'clock signal, a quartz clock movement with trigger was used. Combining these 2 elements a talking sound clock was born

#### Key features:

* Two versions of the (almost) same application: One developed in [CircuitPython](https://www.adafruit.com/circuitpython) and the other in the [C/C++ SDK](https://github.com/raspberrypi/pico-sdk).
* Compatible with the most common operating systems.
* No need to install apps for initial firmware download
* There's no need to recompile code (in the app developed in CircuitPython) to change sounds
* Up to 3 years in standby mode using a pair of AA batteries.
* Easy to source, and solder components.

<figure>
	<a href="/assets/images/rpi_pico_sound_clock.png"> <img src="/assets/images/rpi_pico_sound_clock.png"> </a>
	<figcaption>Simplified diagram of the power circuit</figcaption>
</figure>

##### Software:

Right after power on, Rpi Pico puts a low level on the GPIO that is wired to the power circuit to keep it powered, then decides which file should be played, and after the sound finishes, a high level is put on the GPIO powering off the Pico. Additionally a light sensor is read to not play sound when is dark (night).

Sound files are played sequentially, one by one on each power on. A pointer to the next file is stored in nonvolatile memory, be carefully modifying the program to keep writing at a minimum.

###### PECULIARITIES OF THE SDK C/C++ VERSION:

Sounds to be played must be converted first to WAV format 16 bit mono @ 44100 Hz, then converted to C arrays[] before compiling. The application uses a PWM via digital output and interrupts to play sounds.

The program execution starts almost immediately after power on. The main disadvantage of the application for now, it only supports .WAV files which are big, and cannot be changed without recompiling code

###### PECULIARITIES OF THE CIRCUITPYTHON VERSION:

Sounds to be played must be converted to MP3 mono format, The app uses audiomp3 and audiopwmio modules to output audio out of a digital pin (PWM). These files are stored in the filesystem provided by CP, so modifying them is straightforward, just drag and drop.

MP3 files can store about 10 more sound time than WAV for the same file size, however CircuitPython runtime execution takes more than a second after power on, so probably it won't be a good thing for any kind of final application

##### Hardware:
External components are part of one of the three different functionalities:

* __On/Off__ : The circuit is made up by a MOSFET, Drain terminal connected to 3V3_EN and the Source terminal connected to GND. Connected to the gate are 2 elements: A capacitor to ground, and a resistor to V+. The circuit works in the following way:

  * Step 1: Capacitor is fully charged, turning on the MOSFET and tying 3V3_EN to ground totally powering off Rpi Pico board

  * Step 2: Capacitor is quickly discharged by the brief closure of the contacts of the clock movement, turning off the MOSFET, and powering on the Rpi Pico. The first thing to do after power up, is keeping the capacitor discharged with the aid of a GPIO output in low level.
  
  * Step 3: While sound is played, low level on the GPIO is kept. Once sound finishes, GPIO output turned high level, so MOSFET turns on again, powering off the Rpi Pico until the next switch closure

* __Audio amplifier__: Single-stage, single NPN transistor powers a small 8 Ohm speaker. There is also an input RC low pass filter to smooth noise due to the PWM output.

* __Day/night detection__: Visible light sensor to avoid playing sounds at night. Connected to an ADC pin



##### Board assembly:

Rpi Pico, speaker, light sensor, and clock contacts could be soldered directly to the PCB to get a very small height profile, or add pin headers and female sockets for a more flexible option.

The single sided board can be etched at home. There are some free gpio pads for experimentation and also mounting holes near the corners
 

<figure class="third">
	<a href="/assets/images/SINSONTE_BOARD_HOMEMADE.jpg"> <img src="/assets/images/SINSONTE_BOARD_HOMEMADE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_NOCONNECTOR.jpg"> <img src="/assets/images/SINSONTE_BOARD_NOCONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/SINSONTE_BOARD_WITHCONNECTORS.jpg"> <img src="/assets/images/SINSONTE_BOARD_WITHCONNECTORS_MEDIUM.jpg"> </a>
	<figcaption>Home etched board, direct soldering example and finished with connector headers.</figcaption>
</figure>

To build the wall clock, choose a plate or disk made of plastic or wood, with enough diameter to hide the clock movement and the sound board. Fix all electronic components and then decorative accessories like LED lights. Finish it with the paint work

<figure class="third">
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MECHANISM_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_COMPONENTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_BACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_FRONT_MEDIUM.jpg"> </a>
	<figcaption>clock movement with external contacts, decorative elements, finished back and finished front</figcaption>
</figure>

For hour adjustment, remove all batteries and clock hands (hour, minute, second). Slowly turn clock adjustment knob until a "click" sound is heard. Put all clock hands pointing to 12 O'clock. Put the batteries. Sounds can be shifted pressing the momentary push button switch on the board.



#### Bill of materials

| Component         | Get yours! | Datasheet                                          |
| -------- | ------ | ------------------------------------------------------------ |
| Female header 2.54mm | [shop now](https://s.click.aliexpress.com/e/_eNNciZ) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Male pin header 2.54mm | [shop now](https://s.click.aliexpress.com/e/_eMCUJv) | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf) |
| 1/4W 1% TH Resistors | [shop now](https://s.click.aliexpress.com/e/_eMCbH1) | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf) |
| Push button 6x6mm | [shop now](https://s.click.aliexpress.com/e/_eKd4YV) | [TS-1301.pdf](/assets/pdf/TS-1301.pdf) |
| Raspberry Pi Pico | [shop now](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| 2xAA battery holder for PCB | [shop now](https://s.click.aliexpress.com/e/_AoI96B) | [Comfortable_Catalog.pdf](/assets/pdf/Comfortable_Catalog.pdf) |
| 8 Ohm speaker 29 mm 0.25W | [shop now](https://s.click.aliexpress.com/e/_ATihaX) | [DXP29W-A.pdf](/assets/pdf/DXP29W-A.pdf) |
| MOSFET 2N7000 | [shop now](https://s.click.aliexpress.com/e/_9j8Bgx) | [NDS7002A-D.pdf](/assets/pdf/NDS7002A-D.pdf) |
| NPN BIPOLAR TRANSISTOR 2N2222A | [shop now](https://s.click.aliexpress.com/e/_ANvtiX) | [P2N2222A-D.pdf](/assets/pdf/P2N2222A-D.pdf) |
| TH Radial Electrolytic Capacitor | [shop now](https://s.click.aliexpress.com/e/_9gn4vh) | [TS13DE-CD110X.pdf](/assets/pdf/TS13DE-CD110X.pdf) |
| TH Ceramic Disc Capacitor | [shop now](https://s.click.aliexpress.com/e/_Apm6Pd) | [TS15.pdf](/assets/pdf/TS15.pdf) |
| Quartz clock movement with trigger | [shop now](https://s.click.aliexpress.com/e/_AfCGIL) | [12888SE_TRIGGER_CLOCK_MOVEMENT.pdf](/assets/pdf/12888SE_TRIGGER_CLOCK_MOVEMENT.pdf) |
| Wall Clock hooks DIY | [shop now](https://s.click.aliexpress.com/e/_A0tg3V) | [wall_clock_hook.pdf](/assets/pdf/wall_clock_hook.pdf) |
| TEPT5700 visible light photodiode | [shop now](https://s.click.aliexpress.com/e/_AM6wDK) | [tept5700.pdf](/assets/pdf/tept5700.pdf) |
| LED Copper Wire with battery box | [shop now](https://s.click.aliexpress.com/e/_9vylbl) | [LED_Copper_Wire_Battery_Box.pdf](/assets/pdf/LED_Copper_Wire_Battery_Box.pdf) |


#### Circuit board

| PCB    |  Source files                                        | 
| -------- | ------------------------------------------------------------ |
| Sound board (hardware directory) | [SINSONTE](https://github.com/galopago/SINSONTE)           |



#### Software

| Software    | Source files                                         | 
| -------- | ------------------------------------------------------------ |
| Firmware CircuitPython & SDK C/C++ (software folder)   | [SINSONTE](https://github.com/galopago/SINSONTE)           |

 

## Optional components:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 3 pc step drill bit 3-20 mm + centerpunch  | [shop now](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
