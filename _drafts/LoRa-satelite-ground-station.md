---
title: "LoRa satellite ground station"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN005
  - LoRa
  - ESP32
header:
     teaser: "/assets/images/LORA_GROUND_STATION_TEASER.jpg"
---
The arrival of [small satellites](https://en.wikipedia.org/wiki/Small_satellite) that used [LoRa](https://en.wikipedia.org/wiki/LoRa) for telemetry data has meant that less technically qualified persons, with a very low budget, can receive their signals.Thanks to TinyGS, there is now an open network of distributed ground stations, and more stations can be built to increase their coverage.The project presented here is a reasonably robust, dust-resistant and waterproof implementation of TinyGS ground station, using commercial off-the-shelf components. Ideal for outdoor usage


<figure>
	<a href="/assets/images/LORA_GROUND_STATION.jpg"> <img src="/assets/images/LORA_GROUND_STATION_MEDIUM.jpg"> </a>
	<figcaption>Ground station ready to be placed outside</figcaption>
</figure>

Key component: [Heltec WiFi LoRa kit 32 v2 433mhz](https://s.click.aliexpress.com/e/_A0wUdR)
{: .notice--danger}


##### Why?


The idea of using LoRa for satellite communications became obvious to many people for the following reasons:

* Uses unlicensed [ISM](https://en.wikipedia.org/wiki/ISM_radio_band) band
* Availability of ready to use, low cost, easy to find electronic modules.
* Very long range, and low power communications
* Reception possible with very low level signals -120dBm

The last point is very important, since many commercial antennas can be used (homemade too!), even if they aren't very efficient, are enough to receive signals. This was the Achiles' heel of satellite communications until now


#### What is the project about?

This project is about a gateway between the Internet (WiFi) and LoRa @433Mhz using as much as possible of [commercial off-the-shelf components](https://en.wikipedia.org/wiki/Commercial_off-the-shelf), so not much expertise needed for assembly. The final key consists in downloading [TinyGS firmware](https://github.com/G4lile0/tinyGS) which allows something like:

* Download automatic firmware updates (OTA)
* The receiver will tune automagically to the nearest satellite in the sky
* Configuration of parameters using the local web interface


<figure>
	<a href="/assets/images/LORA_GROUND_STATION_TINYGS.png"> <img src="/assets/images/LORA_GROUND_STATION_TINYGS.png"> </a>
	<figcaption>TinyGS network architecture (taken from TinyGS site)</figcaption>
</figure>

#### Bill of materials

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_PARTS.jpg"> <img src="/assets/images/LORA_GROUND_STATION_PARTS_MEDIUM.jpg"> </a>
	<figcaption>A little bit of knolling.</figcaption>
</figure>

| Component        | Buy link | Datasheet                                 |
| -------- | ------ | ------------------------------------------------------------ |
| Heltec Lora Kit 32 V2 433MHZ ESP32| [buy it](https://s.click.aliexpress.com/e/_A0wUdR) | [WiFi-LoRa-32-V2-433-470-510.pdf](/assets/pdf/WiFi-LoRa-32-V2-433-470-510.pdf) |
| RP-SMA flange to U.FL pigtail | [buy it](https://s.click.aliexpress.com/e/_9vbEjm) | [Catalog_SMA.pdf](/assets/pdf/Catalog_SMA.pdf) |
| 433 Mhz antenna SMA  | [buy it](https://s.click.aliexpress.com/e/_AYvZau) | [433_MHZ_SMA_ANTENNA.pdf](/assets/pdf/433_MHZ_SMA_ANTENNA.pdf) |
| Generic 100x68x50mm waterproof enclosure box "Sonoff" | [buy it](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf) |
| M2.5 countersunk screw phillips | [buy it](https://s.click.aliexpress.com/e/_AEYxys) | [M2-5_COUNTERSUNK_SCREW.pdf](/assets/pdf/M2-5_COUNTERSUNK_SCREW.pdf) |
| M2.5 nylon lock nut | [buy it](https://s.click.aliexpress.com/e/_9RIfcu) | [M2-5_NYLON_LOCK_NUT.pdf](/assets/pdf/M2-5_NYLON_LOCK_NUT.pdf) |
| M2.6 self-tapping B-type screw | [buy it](https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Screw terminal kf350 3.5mm 3 pin | [buy it](https://s.click.aliexpress.com/e/_eLjzKB) | [KF350.pdf](/assets/pdf/KF350.pdf) |
| Female header 2.54mm | [buy it](https://s.click.aliexpress.com/e/_eNYVzN) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| 30 AWG wire wrap UL1423 PVDF | [buy it](https://s.click.aliexpress.com/e/_eL2EYB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| PoE injector 48V 0.5A  | [buy it](https://s.click.aliexpress.com/e/_Dl1hpWX) | [PoE-injector-48V-05A.pdf](/assets/pdf/PoE-injector-48V-05A.pdf)|
| PoE Splitter D1398 module 5V 2A output  | [buy it](https://s.click.aliexpress.com/e/_Al2dql) | [WC-PD13C050I.pdf](/assets/pdf/WC-PD13C050I.pdf)|
| SMA Female To RP SMA Male adapter | [buy it](https://s.click.aliexpress.com/e/_9JKRaz) | [SMA-Female-To-RP-SMA-Male-adapter.pdf](/assets/pdf/SMA-Female-To-RP-SMA-Male-adapter.pdf) |
| Silicone Sealant Neutral RTV | [buy it](https://s.click.aliexpress.com/e/_ANKQnb) | [Neutral-cure-silicone.pdf](/assets/pdf/Neutral-cure-silicone.pdf) |
| Waterproof silicone self fusing vulcanizing tape | [buy it](https://s.click.aliexpress.com/e/_DlbGSST) | [Waterproof-silicone-self-fusing-vulcanizing-tape.pdf](/assets/pdf/Waterproof-silicone-self-fusing-vulcanizing-tape.pdf) |


| Printed Circuit Board | Buy link | Source files repository  |
| --------------------------------- | ---------------- | ------------------------------- |
| Prototype circuit board for 100x68mm enclosure | [buy it](https://www.pcbway.com/project/shareproject/mcu_proto_100x68mm_6ae31333.html) | [mcu-proto-100x68mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-100x68mm) |

| Software | repository |
| ----------------------- | ---------------- |
| TingyGS Firmware | [download it](https://github.com/G4lile0/tinyGS) |

|  Optional component  | Buy link | Datasheet  |
| ----------------------- | ---------------- | ------------------------------- |
| Hand drill set mini 0.5-3mm | [buy it](https://s.click.aliexpress.com/e/_DBPw6on) | [Hand-drill-set-mini.pdf](/assets/pdf/Hand-drill-set-mini.pdf) |


##### Assembly:

This article is not intended to be a step-by-step assembly guide, it will attempt to explain briefly what to do next. Depending on the components obtained, some instructions and their sequence may change slightly.


###### Antenna connector drillings:

* Make 4 drillings with a bit slightly wider than 2.5 mm, that's where the fixing screws will go.

* Make another drilling in the middle with a bit slightly wider than 4 mm, that's where the pigtail wire will go. The drill assistant template can be found [here](https://github.com/galopago/panel-mount-drill-layouts/tree/main/sma-flange-4-holes).


<figure class="third">
	<a href="/assets/images/SMA_FLANGE_TEMPLATE.jpg"> <img src="/assets/images/SMA_FLANGE_TEMPLATE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANGE_FRONT.jpg"> <img src="/assets/images/SMA_FLANGE_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANTE_DIAG.jpg"> <img src="/assets/images/SMA_FLANTE_DIAG_MEDIUM.jpg"> </a>
	<figcaption>Antenna connector drillings</figcaption>
</figure>


###### Connectors and wire soldering

There are two options to power the station: using a simple 5V power supply or using a PoE adapter. The 5V power option requires less hardware, but is limited to a few meters of cable, however the PoE version requires a PoE injector, a PoE splitter inside the case, but it can be placed up to 100 meters away


<figure>
	<a href="/assets/images/tinygs_power_wires_blockdiag.png"> <img src="/assets/images/tinygs_power_wires_blockdiag.png"> </a>
	<figcaption>Simplified diagram of electrical wiring</figcaption>
</figure>

* Solder LoRa module headers. This is not 100% necessary, because the module could be soldered directly to the board, however, using headers make it possible to disconnect the module at any time.

* Solder PoE splitter module header (if used!)

* Solder PCB screw terminals for ease of connection/disconnection of the power cable.

* Solder the power wires under the board, using PVDF coated wire when possible, between the screw terminal pads and the PoE power pads and then to the LoRa power pads


<figure class="third">
	<a href="/assets/images/PCB_BARE.jpg"> <img src="/assets/images/PCB_BARE_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_CONNECTORS.jpg"> <img src="/assets/images/PCB_CONNECTORS_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_POWER_WIRES.jpg"> <img src="/assets/images/PCB_POWER_WIRES_MEDIUM.jpg"> </a>
	<figcaption>Connectors and wires soldered</figcaption>
</figure>

###### Fix antenna connector, circuit board and power cable.

* Fix antenna connector to the enclosure with the screws and nylon nuts

* Pass power cable through cable gland, let the adjusting nuts a little bit unscrewed

* Place PCB inside enclosure and fix it using the self tapping screws

* Connect power cable to screw terminals, antenna cable to LoRa module, and tight cable gland nut. Some experimentation with the order of the aforementioned steps will be required to find the easiest way to assembly.

<figure class="third">
	<a href="/assets/images/TINYGS_ANT_CONNECTOR_FRONT.jpg"> <img src="/assets/images/TINYGS_ANT_CONNECTOR_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_POWER_CABLES.jpg"> <img src="/assets/images/TINYGS_POWER_CABLES_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PCB_FIXED.jpg"> <img src="/assets/images/TINYGS_PCB_FIXED_MEDIUM.jpg"> </a>
	<figcaption>All components fixed inside the enclosure</figcaption>
</figure>

###### Firmware download.

Once the power connection was verified (usually the modules came with some sort of test firmware, so when the power is plugged some data will appear on the screen), connect the LoRa module to a computer using a USB cable, and follow the steps of the [TinyGS wiki](https://github.com/G4lile0/tinyGS/wiki)


<figure>
	<a href="/assets/images/LORA_GROUND_STATION_FW.jpg"> <img src="/assets/images/LORA_GROUND_STATION_FW_MEDIUM.jpg"> </a>
	<figcaption>TinyGS firmware installed!</figcaption>
</figure>

###### Antenna placement.

The antenna must be placed where there is the clearest view of the sky (on the roof or on a long pole) and away from walls or metal structures. In some houses it is not possible so, many tests on the windows must be carried out to obtain the best result

For outdoor installation, seal the second cable gland with a piece of rubber, wrap some self fusing tape around antenna metallic parts, and put a bit of neutral cure silicone sealant over the screws. Avoid using an acidic silicone sealant (those that smell like vinegar) as it oxidizes screws and metallic parts


###### Results

Due to the specific logistic conditions of this test, access to the roof was not possible and permanent structures could not be installed outside the windows, so the following configuration was tested: the receiver box would be placed inside, and a temporary magnetic mounted antenna on the outside.

The antenna was purchased at a local store without any optimization or adjustment. The test was carried out in Cali, Colombia, the longest range transmission was received from [NORBY](https://tinygs.com/satellite/Norbi) satellite over Arequipa, Peru. The distance is about 2265 Km in line of sight, nothing bad for a home-assembled satellite receiver, with a budget of approximately 40 EUR and no adjustment required

<figure class="third">
	<a href="/assets/images/TINYGS_WINDOW_SETUP.jpg"> <img src="/assets/images/TINYGS_WINDOW_SETUP_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_WINDOW_ANTENNA.jpg"> <img src="/assets/images/TINYGS_WINDOW_ANTENNA_MEDIUM.jpg"> </a>
	<a href="/assets/images/TYNYGS_ANTENNA_RECEPTION.jpg"> <img src="/assets/images/TYNYGS_ANTENNA_RECEPTION_MEDIUM.jpg"> </a>
	<figcaption>Ground station setup working</figcaption>
</figure>

###### Variants.

A portable version of the ground station has been developed, it uses a smaller enclosure and is powered by a battery. It was designed to be a temporary-mobile station which connects to a mobile phone via WiFi. It uses a 3.2v [LiFePo4](https://es.wikipedia.org/wiki/Bater%C3%ADa_de_litio-ferrofosfato) battery, therefore no voltage regulator was required, the battery is connected directly to the 3.3v power pin of the LoRa module

The same hardware (fixed or mobile versions) could be used for another type of projects, such as [aprs.fi](https://aprs.fi/), which is of particular interest to amateur radio operators. The hardware is 100% compatible and only requires a [firmware change](https://github.com/lora-aprs/LoRa_APRS_iGate)


<figure class="third">
	<a href="/assets/images/TINYGS_PORTABLE_PCB.jpg"> <img src="/assets/images/TINYGS_PORTABLE_PCB_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_WIRED.jpg"> <img src="/assets/images/TINYGS_PORTABLE_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_FW.jpg"> <img src="/assets/images/TINYGS_PORTABLE_FW_MEDIUM.jpg"> </a>
	<figcaption>Detail of portable ground station</figcaption>
</figure>

| Optional components for mobile version| Buy link | Datasheet           |
| ------------ | ------ | ------------------------------------------------------------ |
| Generic 83x58x33mm waterproof enclosure box | [buy it](https://s.click.aliexpress.com/e/_Ad6Gxn) | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf) |
| AA Battery holder for PCB | [buy it](https://s.click.aliexpress.com/e/_A0wUdR) | [BH311.pdf](/assets/pdf/BH311.pdf) |
| LiFePo4 3.2V 14500 AA Rechargeable battery| [buy it](https://s.click.aliexpress.com/e/_Asl8pn) | [Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf](/assets/pdf/Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf) |


| Printed Circuit Board | Buy link | Source files repository  |
| --------------------------------- | ---------------- | ------------------------------- |
| Prototype circuit board for 83x58mm enclosure | [buy it](https://www.pcbway.com/project/shareproject/mcu_proto_83x58mm_16815998.html) | [mcu-proto-83x58mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-83x58mm) |


