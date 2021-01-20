---
title: "WiFi controlled waterproof LED string"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN001
  - WiFi
  - MONGOOSE OS
header:
     teaser: "/assets/images/MOS_WIFI_IOT_LIGHTS_TEASER.jpg"
---

Decorative lights suitable for Halloween, Christmas, parties, etc. Not only controlled over internet but, also completely reprogrammed 
wirelessly using OTA over WiFi. Waterproof, dustproof and sturdy. Ideal for indoor projects like interactive backgrounds for youtubers/streamers
controlled by their audience and for outdoor projects like advertizing signs in walls or vehicles.


<figure>
	<a href="/assets/images/MOS_WIFI_IOT_LIGHTS.jpg"> <img src="/assets/images/MOS_WIFI_IOT_LIGHTS_MEDIUM.jpg"> </a>
	<figcaption>Open enclosure showing internal components</figcaption>
</figure>

Key component: [WS2811 waterproof LED string.](https://s.click.aliexpress.com/e/_AWaLpZ)
{: .notice--danger}


##### Concept:

With the advent of addressable LED like WS2812, WS2812b, WS2811, etc. is now possible for small microcontrollers to 
handle large amounts of LEDs with only one I/O pin. That advantage popularized this component and a lot of variants appeared: surface mount 
single leds, flexible strips, Christmas-like strings, etc. The last one will be used in this article due to its flexibility and strength and could adapt
easily to different project from Christmas ornaments to led matrix, without soldering or other electrical modifications.

The microcontroller chosen was an ESP8266, more exactly a development board known as "NODEMCU V3" which has all additional components necessary to start work on
programming the MCU with a computer. The onboard WiFi of the ESP8266 is not only possible to to change light sequences, but also download a totally different
firmware wirelessly (OTA), using a powerful combo: [Mongoose OS](https://mongoose-os.com/) and its remote device management dashboard [mDASH](https://mdash.net/).
Mongoose OS uses a scaled down version of JavaScript known as [mJS](https://github.com/cesanta/mjs). This is an attractive language for web developers whom already 
work with JS. Mongoose OS is built on top of Espressif's ESP-iDF, so it is possible to write functions in C, which is also attractive for more "traditional" embedded programmers.

The circuit is built using [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA) hardware prototyping system, which provides different kinds of prebuilt modules which allows
to build an electronic project without soldering, but making it very robust and expandable. All the parts are enclosed in a dustproof and waterproof IP65 box. This enclosure gives an
"industrial look" to the project and also adds mechanical strength to withstand abuses. The external electrical connections (AC, and LEDs) were fitted with IP accessories to provide
a good seal.

#### Key features:
* Mongoose OS embedded operating system running on ESP8266.
* Dustproof, waterproof and wall mountable.
* Wireless remote firmware update, thanks to Mongoose OS management dashboard mDASH.
* Built with TUSISTEMITA hardware prototyping blocks
* 110/220V AC power

The circuit is composed of 4 elements well differentiated: Power source, CPU, logic level shifter and LEDs. Power source is switched type, 20W power, 5V output and 110/220V input, so
it could be used in any country of the world. ESP8266 was used as CPU (NODEMCU V3). This board can be powered by 3.3V directly to processor power pin or by 5V using the
onboard regulator. The high logic level output of ESP8266 is 3.3V, so a logic level shifter is needed for working with 5V sensors. WS2812 works with 5V logic levels so TUSISTEMITA D06
logic level board converter was used. This board is based on BSS138 MOSFET.

<figure>
	<a href="/assets/images/mos_wifi_iot_lights_blockdiag.png"> <img src="/assets/images/mos_wifi_iot_lights_blockdiag.png"> </a>
	<figcaption>Simplified block diagram</figcaption>
</figure>

Power source output current is around 3.8A max, and each WS2811 LED consumes 60 mA max, so at least 63 LED could be powered. To stay below absolute maximum only 50
LED is recommended. Any LED string that works with WS2811 compatible protocol could be used.

##### Mongoose OS:

Mongoose OS is an operating system for the Internet Of Things, it can run on ESP8266, ESP32 and others. Is a blend of easiness and robustness. Ideal for rapid prototyping
of IoT products because of its native built-in cloud connectivity (AWS, Google, Azure).
There are two characteristics that make Mongoose OS so versatile. One of them is the possibility to work "remote/local". Remote is the default option, and compiles
the code in the cloud, this is good for beginners because avoids the problems related to SDK installations. Local option is based on docker containers and is good for automatic builds
without internet connection.

Another important characteristic is the use of a scaled down version of JavaScript called mJS as programming language. Advanced functionalities could be written with
few lines of code compared to other languages (Assembler, C, Processing). However, nothing prevents to call functions written in C, especially for time sensitive device drivers.

##### Software:

Sample application presented here is composed of two tasks: Send color data for every LED in the string and listen to incoming data coming from the cloud.

To send data to each LED, the color code is randomly extracted from a predefined color table. Communication to the LED string is made using NEOPIXEL library bundled 
with Mongoose OS.

An MQTT connection is established to a broker where the app subscribes to a specific topic. A third party client application must connect to the same MQTT broker and publish
data to the same topic to change the color palette used. This is a very simple way to change the light pattern over the internet.

##### Circuit assembly:

The circuit was built using components of TUSISTEMITA, like enclosure backplate, power source backplate, NODEMCU breakboard, logic level shifter board and screw
 terminal board. Once the app is downloaded for the first time, and electrical connections verified, the backplate could be attached to the enclosure hassle free. Just unplug
external cables from terminals, screw backplate to enclosure and reconnect cables again.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_PARTS.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WIRED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_WORKING.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_WORKING_MEDIUM.jpg"> </a>
	<figcaption>Assembly and wiring.</figcaption>
</figure>

It is recommended to change the connectors of the LED strip, for a more robust and waterproof connectors. Heatshrink tube with glue (double wall) should 
be used to protect solder joints from the elements.

<figure class="third">
	<a href="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CABLEGLAND_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_CONNECTOR_MEDIUM.jpg"> </a>
	<a href="/assets/images/MOS_WIFI_LIGHTS_FINISHED.jpg"> <img src="/assets/images/MOS_WIFI_LIGHTS_FINISHED_MEDIUM.jpg"> </a>
	<figcaption>Cable glands and waterproof connectors</figcaption>
</figure>

Once the enclosure is closed, firmware updates could be done via wirelessly via OTA, using Mongoose OS device management dashboard mDASH.

#### Bill of materials

| Component         | Get yours! | Datasheet
| -------- | ------ | ------------------------------------------------------------ |
| ESP8266 NodeMCU V3    | [💸](https://s.click.aliexpress.com/e/_As5zmb)     | [NodeMCUV3.pdf](/assets/pdf/NodeMCUV3.pdf)           |
| WS2811 waterproof LED string | [💸](https://s.click.aliexpress.com/e/_AWaLpZ )  | [WS2811_WATERPROOF_LED_STRING.pdf](/assets/pdf/WS2811_WATERPROOF_LED_STRING.pdf)                               |
| Switched power supply 5V 3.8A 20W   | [💸](https://s.click.aliexpress.com/e/_9gYBnH)     | [5V_4A_switching_power.pdf](/assets/pdf/5V_4A_switching_power.pdf)           |
| Waterproof plastic enclosure 200x120x75mm (multiple options: transparent lid, wall mounting tabs)| [💸](https://s.click.aliexpress.com/e/_ASuE1N)  | [g373_g269.pdf](/assets/pdf/g373_g269.pdf)           |
| M2.6 self-tapping B type screw | [💸](https://s.click.aliexpress.com/e/_98ymAB)  | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)                           |
| M3 countersunk phillips screw | [💸](https://s.click.aliexpress.com/e/_AoOvPz)  | [M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf](/assets/pdf/M2-M10_Stainless_steel_304_countersunk_screw_flat_head_phillips.pdf)                           |
| M3 hex flanged nut DIN6923 | [💸](https://s.click.aliexpress.com/e/_9g89th)  | [FLANGED_NUT_3MM_DIN6923.pdf](/assets/pdf/FLANGED_NUT_3MM_DIN6923.pdf)                           |
| Nylon spacer G228  | [💸](https://s.click.aliexpress.com/e/_A7PPYf)  | [G228.pdf](/assets/pdf/G228.pdf)                           |
| Cable gland PG7 or PG9 | [💸](https://s.click.aliexpress.com/e/_9z6Z4r )  | [pg_7.pdf](/assets/pdf/pg_7.pdf) | 
| 3 pin waterproof cable connector for LED string  | [💸](https://s.click.aliexpress.com/e/_AesJgr )  | [Waterproof_led_string_connector.pdf](/assets/pdf/Waterproof_led_string_connector.pdf)                           |
| 3:1 Heatshrink tube with glue  | [💸](https://s.click.aliexpress.com/e/_AaW9bd)  | [3_1_heatshrink_tube_glue.pdf](/assets/pdf/3_1_heatshrink_tube_glue.pdf)                           |
| 2:1 Heatshrink tube multiple colors  | [💸](https://s.click.aliexpress.com/e/_9ikkU7 )  | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf)                           |

#### TUSISTEMITA blocks

| PCB    |  Source file                                          | 
| -------- | ------------------------------------------------------------ |
| A02 Backplate for 200x120x75mm enclosure | [A02](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| A05 adapterboard 10.16mm pitch for 5V 3.8A PSU  | [A05](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)        |
| B01 2x4 3.5mm screw terminal board | [B01](https://github.com/galopago/TUSISTEMITA/tree/master/B_SCREW_TERMINAL_WIRE_CONNECTORS)        |
| C08 screw terminal breakout board for NODEMCU V3  | [C08](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |
| D06 logic level shifter board  | [D06](https://github.com/galopago/TUSISTEMITA/tree/master/D_ELECTRONICS)        |


#### Software

| Software    | Source file                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [MOS_IOT_ADDRESSABLE_LEDS](https://github.com/galopago/MOS_IOT_ADDRESSABLE_LEDS)           |

 

## Componentes opcionales:

| Component         | Get yours! | Datasheet                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 3 pc step drill bit 3-20 mm + centerpunch | [💸](https://s.click.aliexpress.com/e/_9vxJV5 )     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| 8 Step drill bit 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_9Ior51)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
