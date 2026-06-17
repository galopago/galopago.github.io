---
title: 'Panel-mount 0.96" bare OLED with screw terminals'
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN009
  - Prototyping
header:
  teaser: "/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_TEASER.jpg"
---

Small OLED modules look interchangeable at first glance, but mounting holes and the panel cutout needed for the display to show through rarely match between vendors. A clean panel installation usually means a precise display window plus four accurately placed screw holes. Those dimensions change from one module to the next.

<figure>
  <a href="/assets/images/AN009/FIG_P0001_1.jpg">
    <img src="/assets/images/AN009/FIG_P0001_1_MEDIUM.jpg">
  </a>
  <figcaption>Subtle distance differences between displays from different manufacturers</figcaption>
</figure>

This project packages a raw 0.96" I2C OLED with no intermediate processing module inside a 48×29 mm panel-mount enclosure with [screw terminals](https://www.designworldonline.com/basics-of-terminal-blocks-and-their-various-subtypes/). Build it only once across prototypes without resoldering or crimping custom cables.

##### Why?
Panel instruments in the 48×29 mm form factor share a practical semi-standard: one rectangular cutout, internal clips and a front bezel that hides imperfect edges. That idea was borrowed from low-cost DC panel meters, including the popular “9-in-1” voltage/current/power modules, which already use a two-board internal layout.

<figure>
  <a href="/assets/images/AN009/FIG_P0003_1.jpg">
    <img src="/assets/images/AN009/FIG_P0003_1_MEDIUM.jpg">
  </a>
  <figcaption>Panel-mount digital voltmeter</figcaption>
</figure>

After searching for an off-the-shelf product that combined panel mounting, a dumb I2C display and robust screw terminals, nothing turned up at hobby quantities. The reference starting point was the popular “9-in-1” DC voltage/current/power panel meter in a 48×29 mm enclosure.

<figure class="third">
  <a href="/assets/images/AN009/FIG_P0004_1.jpg">
    <img src="/assets/images/AN009/FIG_P0004_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0004_2.jpg">
    <img src="/assets/images/AN009/FIG_P0004_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0004_3.jpg">
    <img src="/assets/images/AN009/FIG_P0004_3_MEDIUM.jpg">
  </a>
  <figcaption>Inside the 9-in-1 meter enclosure</figcaption>
</figure>

Core component: [0.96" OLED 128x64 bare screen I2C.](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen)
{: .notice--danger}

<figure>
  <a href="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY.jpg">
    <img src="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_MEDIUM.jpg">
  </a>
  <figcaption>Panel-mount OLED module assembled in 48x29 mm enclosure</figcaption>
</figure>

#### Key features:
* Open source hardware: [KiCad sources and Gerbers on GitHub](https://github.com/galopago/panel-mount-oled-display)
* Raw I2C OLED interface (no on-board MCU)
* 48×29 mm panel-mount bezel tolerates a rough cutout
* Six independent 0805 indicator LEDs with separate anode/cathode terminals
* Double-level 3.5 mm screw terminals for solid wire, stranded wire or Dupont leads
* Two-board stack: solder once, rewire many times across projects

#### Bill Of Materials

| Component | Buy link | Datasheet |
| --------- | -------- | --------- |
| SMD capacitor kit (0805) | [Buy link](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=smd%200805%20capacitor%20kit) | [smd-capacitors.pdf](/assets/pdf/smd-capacitors.pdf) |
| SMD LED (0805) | [Buy link](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=led%20smd%200805) | [smd-led-0805.pdf](/assets/pdf/smd-led-0805.pdf) |
| SMD diode 1N4148 | [Buy link](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%20led%201n4148%20melf) | [smd-diode-1n4148-melf.pdf](/assets/pdf/smd-diode-1n4148-melf.pdf) |
| SMD resistor kit (0805) | [Buy link](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%200805%20resistor%20kit) | [smd-resistors.pdf](/assets/pdf/smd-resistors.pdf) |
| Pin header 1x8 2.54 mm (male) | [Buy link](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=single%20row%20pin%20header%202.54) | [single-row-male-header-2-54-pitch.pdf](/assets/pdf/single-row-male-header-2-54-pitch.pdf) |
| PCB screw terminal double level 3.5 mm (2x8) | [Buy link](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=KF128A-3.5) | [pcb-screw-terminal-double-level-3-5.pdf](/assets/pdf/pcb-screw-terminal-double-level-3-5.pdf) |
| 0.96″ OLED 128x64 bare screen I2C | [Buy link](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen) | [oled-0-96-i2c-128x64-bare-screen.pdf](/assets/pdf/oled-0-96-i2c-128x64-bare-screen.pdf) |
| XC6206 3.3 V LDO regulator (SOT-23) | [Buy link](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=XC6206P332%20sot%2023) | [xc6206.pdf](/assets/pdf/xc6206.pdf) |

#### Printed Circuit Boards

| PCB | Source files |
| --- | ------------ |
| Display board (OLED, regulator, LEDs) | [panel-mount-oled-display/display-board](https://github.com/galopago/panel-mount-oled-display/tree/main/display-board) |
| Connector board (screw terminals) | [panel-mount-oled-display/connector-board](https://github.com/galopago/panel-mount-oled-display/tree/main/connector-board) |

#### Electronic design
The design splits functionality across two boards joined by a 1×8 header. The display board carries the XC6206 3.3 V regulator, the OLED auto-reset network, I2C coupling, some capacitors used by the display's internal DC/DC converter and six indicator LEDs with independent terminals. The connector board only routes to the double-level screw terminals. Full schematics and design notes are in the [GitHub repository](https://github.com/galopago/panel-mount-oled-display).

<figure>
  <a href="/assets/images/AN009/SCHEMATIC.png">
    <img src="/assets/images/AN009/SCHEMATIC.png">
  </a>
  <figcaption>Schematic (display and connector boards)</figcaption>
</figure>

#### Assembly
Manual build follows the two-board layout seen in cheap “9-in-1” panel meters. Solder the SMD parts on both PCBs first. The display board gets the flex OLED (0.7 mm pitch, 30 pins), the XC6206, the auto-reset network and six indicator LEDs. The connector board gets the double-level screw terminals. The flex display needs a T-tip iron; everything else is routine SMD work.

<figure class="third">
  <a href="/assets/images/AN009/ASSEMBLY_1.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0006_2.jpg">
    <img src="/assets/images/AN009/FIG_P0006_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/FIG_P0006_3.jpg">
    <img src="/assets/images/AN009/FIG_P0006_3_MEDIUM.jpg">
  </a>
  <figcaption>Component assembly on the two boards</figcaption>
</figure>

Stack the boards with 1×8 pin headers and a spacer between them so the terminals stay reachable from the side.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_2.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_2_MEDIUM.jpg">
  </a>
  <figcaption>Stacked display and connector boards with pin headers and standoffs</figcaption>
</figure>

The case comes from a donor 48×29 mm panel meter (whichever is cheapest): strip the original electronics and reuse the front bezel and acrylic window, or cut a new dark translucent lens up to 1 mm thick. Slide the board stack into the case; internal clips hold the module without extra panel screws.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_3.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_3_MEDIUM.jpg">
  </a>
  <figcaption>Board stack installed inside the enclosure</figcaption>
</figure>

#### Software
This module has no firmware of its own. Any host with I2C (Arduino, RPi Pico, ESP32, etc.) can drive the SSD1306-compatible display and the six LED outputs through the screw terminals.

### Customization
The design can be adapted around power input and how the indicator LEDs are used. A resistor can also be moved between two solder positions to choose between two possible I2C bus orientations.

##### Power source
The on-board XC6206 provides 3.3 V for the OLED from the VCC/GND screw terminals. Feed within the regulator and display ratings (typically 3.3-5 V at the input, depending on the exact XC6206 variant populated).

##### Expansion
Six 0805 LEDs are broken out with independent anode and cathode terminals, so each indicator can belong to a different circuit or ground domain. The bottom terminal row is tighter for Dupont plugs but holds firmly once inserted.

<figure>
  <a href="/assets/images/AN009/FIG_P0012_1.jpg">
    <img src="/assets/images/AN009/FIG_P0012_1_MEDIUM.jpg">
  </a>
  <figcaption>Two LEDs lit: left center position and right lower position</figcaption>
</figure>

##### Sample application
Mount the module in a panel or bench enclosure and wire I2C (SCL, SDA, VCC, GND) from the microcontroller to the screw terminals. Route one or more of the six LED pairs to status signals (power OK, alarm, mode, etc.) on independent returns if needed. When the project ends, unscrew the leads and move the same assembly to the next prototype.

<figure class="third">
  <a href="/assets/images/AN009/SAMPLE_1.jpg">
    <img src="/assets/images/AN009/SAMPLE_1_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/SAMPLE_2.jpg">
    <img src="/assets/images/AN009/SAMPLE_2_MEDIUM.jpg">
  </a>
  <a href="/assets/images/AN009/SAMPLE_3.jpg">
    <img src="/assets/images/AN009/SAMPLE_3_MEDIUM.jpg">
  </a>
  <figcaption>Square cutout detail for display mounting</figcaption>
</figure>

## Optional components:

| Component | Buy link | Datasheet |
| --------- | -------- | --------- |
| 48x29 mm panel meter (donor enclosure) | [Buy link](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=panel%20digital%20voltmeter) | [48x29mm-digital-voltmeter.pdf](/assets/pdf/48x29mm-digital-voltmeter.pdf) |
| T-type soldering tip (flex cable) | [Buy link](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=Soldering%20Iron%20T%20Tip%20T-head%20Copper%20T-Tips%20%2B%20Rubber) | [t-type-soldering-tip-60w.pdf](/assets/pdf/t-type-soldering-tip-60w.pdf) |
| Translucent acrylic sheet 1 mm | [Buy link](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=Translucent%20%20Acrylic%20Plexiglass%201mm) | [translucent-acrylic-plexiglass-1mm.pdf](/assets/pdf/translucent-acrylic-plexiglass-1mm.pdf) |

## Practical notes:
At heart, the goal was simple: solder the display once, then move the module from one prototype to the next without touching the iron or crimper again. Screw the wires, unscrew them, done. If you rework cabling on the bench or inside an instrument box, that convenience adds up fast.

The electronics are the easy part; the enclosure is where the time goes. Empty 48×29 mm cases barely exist in hobby quantities. The realistic move is to buy the cheapest panel meter you can find and strip it. For the front window, everything was tried: the donor voltmeter’s red sheet dims the OLED too much, and green or blue pieces did no better. The grey translucent lens from the donor multimeter looked best (or dark translucent acrylic up to 1 mm if you cut your own).

One reassuring detail: the panel cutout does not need to be perfect. The bezel hides rough edges and internal clips hold the module without extra screws. Dupont plugs on the bottom terminal row are a snug fit (not the most comfortable row to work with), but once seated they stay put even if you tug the cable.
