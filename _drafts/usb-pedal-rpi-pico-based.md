---
title: "USB Pedal based on Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - english
tags:
  - AN002
  - RPI PICO
  - CIRCUITPYTHON
header:
     teaser: "/assets/images/USB_PEDAL_RPI_PICO_TEASER.jpg"
---
USB pedals (or any other momentary switches) who emulates keyboard keypress or combination of keys. Handy to use with video edition software to pause/play without moving the hands away from the keyboard or mouse, it can also be used by videoconferencing software to mute quickly. There's no need for special application to download initial firmware nor for keys setup (only a simple text editor needed). Works with almost any operating system, even with android devices using an OTG USB adapter.

<figure>
	<a href="/assets/images/USB_PEDAL_RPI_PICO.jpg"> <img src="/assets/images/USB_PEDAL_RPI_PICO_MEDIUM.jpg"> </a>
	<figcaption>USB Pedal circuit installed in a robust enclosure</figcaption>
</figure>

Key component: [Rpi Pico.](https://s.click.aliexpress.com/e/_AXStdl)
{: .notice--danger}


##### Concept:

A lot of USB programmable pedals on the market need to install an application for configuration. Usually this app is only for Windows and came poorly translated (if translated at all). This is a pitfall for Linux or Mac users, who have only two options: To install a Windows virtual machine or ask a favor to a Windows user for pedal setup.

Here come to the rescue [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/), for two big reasons: USB native interface, so no programmer or additional hardware needed for firmware download and the most important: CircuitPython support. Programming could be "on the fly" without compiling-and-download during the debug phase. So Rpi Pico is the best candidate for a DIY pedal.

Another additional advantage over commercial USB pedals, the pedal itself can be replaced for a more robust one, without touching the circuit. Another kind of switches could be used, so operation with different parts of the body is possible. The amount of switches to be installed is only limited by Rpi Pico GPIO pins and the space available on the enclosure.

The circuit is built using [TUSISTEMITA](https://github.com/galopago/TUSISTEMITA) hardware prototyping system, which provides different kinds of prebuilt modules which allows to build an electronic project without soldering, but making it very robust and expandable. All the parts are enclosed in a dustproof and waterproof IP65 box. This enclosure gives an “industrial look” to the project and also adds mechanical strength to withstand abuses. The external electrical connections (pedals, and USB) were fitted with IP accessories to provide a good seal.


#### Key features:

* Developed using CircuitPython, friendly and easy to learn
* Compatible with the most common operating systems
* No need to install apps for initial firmware download
* Key configuration done in a text file
* Splash resistant and shockproof
* Detachable and replaceable pedals
* Built using hardware prototyping system
* Powered by USB, no additional power source needed

The hardware is pretty simple, only requires a Rpi Pico and switches connected between GPIO and ground. Internal pull-up resistors used. Power and data via USB cable


<figure>
	<a href="/assets/images/rpi_pico_usb_keyboard.png"> <img src="/assets/images/rpi_pico_usb_keyboard.png"> </a>
	<figcaption>Simplified block diagram</figcaption>
</figure>


##### What is CircuitPython?:
In [Adafruit Industres](https://learn.adafruit.com/bienvenido-a-circuitpython-2/que-es-circuitpython) words, makers of CircuitPython: 
> CircuitPython is a programming language designed to simplify experimenting and learning to program on low-cost microcontroller boards. It makes getting started easier than ever with no upfront desktop downloads needed. Once you get your board set up, open any text editor, and get started editing code. It's that simple.

Other reasons to use CircuitPython include:


* You want to get up and running quickly. Create a file, edit your code, save the file, and it runs immediately. There is no compiling, no downloading and no uploading needed.
* You're new to programming. CircuitPython is designed with education in mind. It's easy to start learning how to program and you get immediate feedback from the board.
* Easily update your code. Since your code lives on the disk drive, you can edit it whenever you like, you can also keep multiple files around for easy experimentation.
* The serial console and REPL. These allow for live feedback from your code and interactive programming.
* File storage. The internal storage for CircuitPython makes it great for data-logging, playing audio clips, and otherwise interacting with files.
* Strong hardware support. There are many libraries and drivers for sensors, breakout boards and other external components.
* It's Python! Python is the fastest-growing programming language. It's taught in schools and universities. CircuitPython is almost-completely compatible with Python. It simply adds hardware support.

##### Software:

Sample application presented here is composed of two tasks: Initialize GPIO according to the configuration file and then runs an endless loop verifying for switch closing to send its respective keycode. Software debouncing function was used to avoid false key press. Rpi Pico onboard LED lights when whatever configured switch closes.

The configuration file structure is very simple. First line GPIOS to use, second line keycode to send, and third line modifier keycode (I.E SHIFT, CONTROL, ALT). If during initialization the config file isn't found, the program will assume some default values. More GPIOS can be added to the config file, so 3, 4 or mode pedals could be plugged.

##### Ensamblaje:

El prototipo del sistema fue montado usando varios componentes de TUSISTEMITA, como la placa trasera para montaje, y la tarjeta de salida a terminales de tornillo para el Rpi Pico

Una vez descargada la aplicacion por primera vez y comprobado que las conexiones electricas funcionan bien,
se puede pasar a la caja para montaje definitivo sin ningun traumatismo. Solamente hay que desconectar el puerto USB y las terminales de tornillo donde estan conectados los interruptores de prueba, fijar la placa a la caja y reconectar nuevamente. 

<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_DEBUG.jpg"> <img src="/assets/images/USB_PEDAL_PICO_DEBUG_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PARTS.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_WIRED.jpg"> <img src="/assets/images/USB_PEDAL_PICO_WIRED_MEDIUM.jpg"> </a>
	<figcaption>Pruebas, ensamblaje y cableado.</figcaption>
</figure>

Se escogio un conector USB tipo impresora, por ser uno de los mas robustos e intuitivos. El conector usado es del tipo para montaje en panel y
tiene 4 pines para soldar los cables (VCC,USB+,USB-,GND). Este conector se soldo a una extension Micro USB que conectara al Rpi Pico. Los pedales usan conectores tipo aviacion

<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_AVIATION.jpg"> <img src="/assets/images/USB_PEDAL_PICO_AVIATION_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PANEL.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PANEL_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PRINTER.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PRINTER_MEDIUM.jpg"> </a>
	<figcaption>Conectores para pedales y computador</figcaption>
</figure>

Una vez cerrada la caja, las actualizaciones al programa pueden hacerse modificando el archivo de CircuitPython, o usando la interfaz interactiva. Si se requiere hacer una reinstalacion de CircuitPython o "formatear" el Rpi Pico, debera abrirse la caja para tener acceso al boton bootsel.

#### Listado de materiales

| Component         | Get yours! | Datasheet                                          |
| -------- | ------ | ------------------------------------------------------------ |
| M2.6 self-tapping B-type screw | [💸](https://s.click.aliexpress.com/e/_eOJ3Kd) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| 2:1 Heatshrink tube multiple colors | [💸](https://s.click.aliexpress.com/e/_9ikkU7) | [2_1_heatshrink_tube_colors.pdf](/assets/pdf/2_1_heatshrink_tube_colors.pdf) |
| 115x90x55 mm enclosure box | [💸](https://s.click.aliexpress.com/e/_AFnqxL) | [KH-F3.pdf](/assets/pdf/KH-F3.pdf) |
| Raspberry Pi Pico | [💸](https://s.click.aliexpress.com/e/_AXStdl) | [pico-datasheet.pdf](/assets/pdf/pico-datasheet.pdf) |
| USB Type B IP68 panel connector | [💸](https://s.click.aliexpress.com/e/_AbHdB8) | [USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf](/assets/pdf/USB_TYPE_B_PANEL_MOUNT_CONNECTOR.pdf) |
| 4 pin aviation connector | [💸](https://s.click.aliexpress.com/e/_9yPVWE) | [CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf](/assets/pdf/CIRCULAR_AVIATION_PANEL_CONNECTOR.pdf) |
| Metal electric foot switch | [💸](https://s.click.aliexpress.com/e/_97Yt4m) | [METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf](/assets/pdf/METAL_MOMENTARY_ELECTRIC_FOOT_SWITCH.pdf) |
| USB printer cable A type | [💸](https://s.click.aliexpress.com/e/_A1mCwQ) | [USB_PRINTER_CABLE.pdf](/assets/pdf/USB_PRINTER_CABLE.pdf) |
| Micro USB cable | [💸](https://s.click.aliexpress.com/e/_97vmPY) | [MICRO_USB_CABLE.pdf](/assets/pdf/MICRO_USB_CABLE.pdf) |


#### Componentes TUSISTEMITA

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Placa trasera para montaje A01 para caja de 158x90x60mm | [A01](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| Tarjeta breakout C11 con salida a terminales de tornillos para Rpi Pico  | [C11](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |



#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [PEDAL_USB_RPI_PICO](https://github.com/galopago/RPI_PICO_USB_FOOT_SWITCH)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_9vxJV5)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_9Ior51)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
