---
title: "Pedal USB baseado em Rpi Pico"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - portugues
tags:
  - AN002
  - RPI PICO
  - CIRCUITPYTHON
header:
     teaser: "/assets/images/USB_PEDAL_RPI_PICO_TEASER.jpg"
---
Pedais USB (ou qualquer outro interruptor momentâneo) que imitam a pressão de uma tecla no teclado ou combinação de teclas. Prático para usar com software de edição de vídeo para pausar/reproduzir sem afastar as mãos do teclado ou mouse, também pode ser usado por software de videoconferência para silenciar rapidamente. Não é necessário baixar firmware especial ou configurar teclas (apenas um editor de texto simples é necessário). Funciona com quase qualquer sistema operacional, até mesmo com dispositivos Android usando um adaptador USB OTG.

<figure>
	<a href="/assets/images/USB_PEDAL_RPI_PICO.jpg"> <img src="/assets/images/USB_PEDAL_RPI_PICO_MEDIUM.jpg"> </a>
	<figcaption>Circuito do pedal USB instalado em uma caixa robusta.</figcaption>
</figure>

Componente chave: [Rpi Pico.](https://s.click.aliexpress.com/e/_AXStdl)
{: .notice--danger}


##### Conceito:

A grande maioria dos pedais programáveis USB disponíveis no mercado precisam que você instale um aplicativo para configuração. Normalmente, este aplicativo só está disponível para Windows e vem traduzido de maneira precária (se é que vem traduzido). Isso é um obstáculo para usuários de Linux ou Mac, que só têm duas opções: instalar uma máquina virtual Windows ou pedir ajuda a um usuário Windows para configurar o pedal.

Aqui entra em ação o [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/), por duas grandes razões: interface USB nativa, sem necessidade de programador ou hardware adicional para download de firmware, e o mais importante: suporte ao CircuitPython. A programação pode ser feita "ao vivo", sem necessidade de compilação e download durante a fase de depuração. Portanto, o Rpi Pico é o melhor candidato para um pedal DIY.

Outra vantagem adicional sobre os pedais USB comerciais, o próprio pedal pode ser substituído por um mais robusto, sem tocar no circuito. Outro tipo de interruptores pode ser usado, para que a operação com diferentes partes do corpo seja possível. A quantidade de interruptores a serem instalados é limitada apenas pelos pinos GPIO do Rpi Pico e pelo espaço disponível na caixa.

O circuito é construído usando o sistema de prototipagem de hardware [MISISTEMITA](https://github.com/galopago/misistemita), que fornece diferentes tipos de módulos pré-construídos que permitem construir um projeto eletrônico sem solda, mas tornando-o muito robusto e expansível. Todas as peças estão enclausuradas em uma caixa à prova de poeira e água IP65. Essa caixa confere um aspecto "industrial" ao projeto e também adiciona força mecânica para suportar abusos. As conexões elétricas externas (pedais e USB) foram equipadas com acessórios IP para fornecer uma boa vedação.


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

##### Circuit assembly:

The circuit was built using components of TUSISTEMITA, like enclosure backplate, and Rpi Pico screw terminal breakboard.

Once the app is downloaded for the first time, and electrical connections verified, the backplate could be attached to the enclosure hassle free. Just unplug USB cable and debug switches' screw terminals, screw backplate to enclosure and reconnect cables again.

<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_DEBUG.jpg"> <img src="/assets/images/USB_PEDAL_PICO_DEBUG_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PARTS.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PARTS_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_WIRED.jpg"> <img src="/assets/images/USB_PEDAL_PICO_WIRED_MEDIUM.jpg"> </a>
	<figcaption>Debug, wiring and assembly.</figcaption>
</figure>

USB printer connector (Type B) was chosen because is very robust and intuitive. This specific connector is designed for panel mounting and sports 4 metal pins (VCC,USB+,USB-,GND) that must be soldered to a Micro USB extension cable to plug to the Rpi Pico. Pedals use circular aviation connectors.


<figure class="third">
	<a href="/assets/images/USB_PEDAL_PICO_AVIATION.jpg"> <img src="/assets/images/USB_PEDAL_PICO_AVIATION_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PANEL.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PANEL_MEDIUM.jpg"> </a>
	<a href="/assets/images/USB_PEDAL_PICO_PRINTER.jpg"> <img src="/assets/images/USB_PEDAL_PICO_PRINTER_MEDIUM.jpg"> </a>
	<figcaption>Connectors for computer and pedals</figcaption>
</figure>

Once the enclosure is closed, firmware updates could be done modifying the CircuitPython file, or via interactive environment. For a CircuitPython re-installation or Rpi Pico "format", the enclosure must be open to access bootsel button.

#### Bill of materials

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


#### TUSISTEMITA blocks

| PCB    |  Source file                                          | 
| -------- | ------------------------------------------------------------ |
| A01 Backplate for 158x90x60mm enclosure| [A01](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| C11 screw terminal breakout board for Rpi Pico  | [C11](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |



#### Software

| Software    | Source file                                        | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [PEDAL_USB_RPI_PICO](https://github.com/galopago/RPI_PICO_USB_FOOT_SWITCH)           |

 

## Optional components:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| 3 pc step drill bit 3-20 mm + centerpunch  | [💸](https://s.click.aliexpress.com/e/_9vxJV5)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| 8 Step drill bit 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_9Ior51)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
