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

<figure>
	<a href="/assets/images/HALLOWEEN_TALKING_CLOCK.jpg"> <img src="/assets/images/HALLOWEEN_TALKING_CLOCK_MEDIUM.jpg"> </a>
	<figcaption>Relógio personalizado pendurado na parede.</figcaption>
</figure>

Componente chave: [Movimento de relógio de quartzo com gatilho](https://s.click.aliexpress.com/e/_AfCGIL)
{: .notice--danger}


##### Conceito:

Um grande número de relógios de parede musicais no mercado carecem da possibilidade de mudar os sons originais. Um relógio com essa capacidade pode ser construído com um sistema embarcado. Mas qual escolher? O Raspberry Pi Pico foi escolhido por 3 razões:

Não é necessário instalar software para o download inicial do firmware
A memória onboard de 2 MegaBytes de flash pode armazenar alguma quantidade de sons sem precisar de memória externa
Pode ser alimentado por 2 baterias AA sem componentes adicionais.

A Rpi Pico consome cerca de 1,6 mA no seu modo de consumo mais baixo (sono profundo). Pode parecer pouco, mas é alto demais para um circuito alimentado por bateria, pois elas se esgotarão em cerca de dois meses. Por esse motivo, um circuito de alimentação externo que pode desligar completamente a placa foi adicionado. Depois disso, o consumo de energia caiu para 70 uA, então as baterias durarão por um ano.

O Rpi Pico age como armazenador e tocador de som. Para exibir o tempo e gerar um sinal de "hora", foi usado um movimento de relógio de quartzo com gatilho. Ao combinar esses dois elementos, nasceu um relógio falante de som.


#### Recursos principais:

* Duas versões da mesma aplicação (quase): Uma desenvolvida em [CircuitPython](https://www.adafruit.com/circuitpython) e a outra no [C/C++ SDK](https://github.com/raspberrypi/pico-sdk).
* Compatível com os sistemas operacionais mais comuns.
* Não é necessário instalar aplicativos para o download inicial do firmware.
* Não é necessário recompilar o código (na aplicação desenvolvida em CircuitPython) para mudar os sons.
* Até 3 anos em modo de standby usando uma par de pilhas AA.
* Componentes fáceis de encontrar e soldar.


<figure>
	<a href="/assets/images/rpi_pico_sound_clock.png"> <img src="/assets/images/rpi_pico_sound_clock.png"> </a>
	<figcaption>Diagrama simplificado do circuito de energia</figcaption>
</figure>

##### Software:

Assim que ligado, o Rpi Pico coloca um nível baixo no GPIO que está conectado ao circuito de alimentação para mantê-lo ligado, então decide qual arquivo deve ser tocado e, após o som terminar, é colocado um nível alto no GPIO desligando o Pico. Além disso, é lida uma sensibilidade à luz para não tocar som quando estiver escuro (à noite).

Os arquivos de som são reproduzidos sequencialmente, um por um a cada ligada. Um ponteiro para o próximo arquivo é armazenado na memória não volátil, cuidado ao modificar o programa para manter a escrita mínima.

###### Peculiaridades da versão C/C++ SDK:

Os sons a serem reproduzidos devem ser convertidos primeiro para o formato WAV de 16 bits mono a 44100 Hz, em seguida convertidos para arrays C[] antes da compilação. A aplicação usa uma PWM via saída digital e interrupções para reproduzir sons.

O programa começa a ser executado logo após a ligação. A principal desvantagem do aplicativo por enquanto é que ele só suporta arquivos .WAV, que são grandes e não podem ser alterados sem recompilar o código.


###### Peculiaridades da versão CircuitPython:

Sons a serem tocados devem ser convertidos para o formato MP3 mono, o aplicativo usa módulos audiomp3 e audiopwmio para saída de áudio de um pino digital (PWM). Esses arquivos são armazenados no sistema de arquivos fornecido pelo CP, então a sua modificação é simples, basta arrastar e soltar.

Arquivos MP3 podem armazenar cerca de 10 vezes mais tempo de som do que WAV para o mesmo tamanho de arquivo, no entanto, a execução do tempo de execução do CircuitPython leva mais de um segundo após a ligar, então provavelmente não será uma coisa boa para qualquer tipo de aplicação final.


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
