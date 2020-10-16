---
title: "Nodo LoRa basado en RAK811 y alimentado por baterias AA"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN000
  - LoRaWAN
header:
     teaser: "/assets/images/RAK811_NODE_OPEN_TEASER.jpg"
---

Nodo LoRa concebido para la experimentacion. Se conecta facilmente con casi cualquier tipo de sensor. Diseñado para instalarse dentro
de una caja generica resistente al agua, solo hay que agregar un par de pilas AA alcalinas, y listo para usarse!

Componente clave: [Modulo LoRa RAK811.](https://s.click.aliexpress.com/e/_eOuZFX)
{: .notice--danger}

<figure>
	<a href="/assets/images/RAK811_NODE_OPEN.jpg"> <img src="/assets/images/RAK811_NODE_OPEN_MEDIUM.jpg"> </a>
	<figcaption>Nodo Lora dentro de la caja resistente agua.</figcaption>
</figure>


#### Principales caracteristicas:
* Hardware & Software de Codigo Libre
* Se alimenta con 2 pilas AA (1.5v) .
* Resistente al agua y montable en pared.
* RAK811=SX1276+STM32L151. No se necesita microcontrolador adicional.
* Programacion mediante [RAK RUI API](https://docs.rakwireless.com/RUI/), o STM32 CUBE LoRa stack.
* Area para expansion y/o Prototipado.
* Pads para soldar antena de resorte interna o conector U.FL para externa.


#### Listado de materiales

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Modulo LoRa RAK811    | [💸](https://s.click.aliexpress.com/e/_eOuZFX)     | [RAK811.pdf](/assets/pdf/RAK811.pdf)           |
| Caja generica resistente al agua de 83x58x33mm  (varias opciones: tapa transparente, salientes para montaje en pared)    | [💸](https://s.click.aliexpress.com/e/_eNGM5X )  | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf)                               |
| Tornillo autorroscante M2.6  tipo B    | [💸](https://s.click.aliexpress.com/e/_eOJ3Kd)     | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf)           |
| Soporte para bateria AA para montaje en PCB  | [💸](https://s.click.aliexpress.com/e/_eLS8qh)  | [BH311.pdf](/assets/pdf/BH311.pdf) | 
| Bornera de tornillo kf350 3.5mm 3 pines | [💸](https://s.click.aliexpress.com/e/_eKkaWv)  | [KF350.pdf](/assets/pdf/KF350.pdf)                           |
| Antena de resorte para 433,868,915 MHz| [💸](https://s.click.aliexpress.com/e/_eNNciZ)  | [SW433-TH32.pdf](/assets/pdf/SW433-TH32.pdf) [SW868-TH06.pdf](/assets/pdf/SW868-TH06.pdf) [SW915-TH12.pdf](/assets/pdf/SW915-TH12.pdf)
| Conector de hilera de pines hembra 2.54mm  | [💸](https://s.click.aliexpress.com/e/_eN8wK1)  | [FHA3-SXX.pdf](/assets/pdf/FHA3-S1XX.pdf)                           |
| Conector de hilera de pines macho 2.54mm  | [💸](https://s.click.aliexpress.com/e/_eMCUJv )  | [PHA1-S3XX.pdf](/assets/pdf/PHA1-S3XX.pdf)                           |

#### Tarjetas de Circuito Impreso

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Tarjeta principal     | [RAK811 LORA ADAPTABLE NODE](https://github.com/galopago/RAK811_LORA_ADAPTABLE_NODE)           |
| Tarjeta de expansion  | [RAK LORA ADAPTABLE NODE BREAKOUT 2AA](https://github.com/galopago/RAK_LORA_ADAPTABLE_NODE_BREAKOUT_2AA)        |

#### Software

| Software    | Archivos fuentes                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [RAK811 RUI SWITCH SENSOR](https://github.com/galopago/RAK811_RUI_SWITCH_SENSOR)           |

### Personalizacion
El proyecto ha sido dividido en 4 principales aspectos: fuente de alimentacion, caja, antena y expansion. Cada uno de los cuales puede ser modificado segun los requerimientos propios. Finalmente se presentara una aplicacion de ejemplo para mostrar como implementar su propio sensor.

##### Fuente de alimentacion
El dispositivo puede operar desde 1.8v hasta 3.7v. Hay varias alternativas para hacerlo:
* 2 Pilas alcalinas AA. Se deberan cortocircuitar las posiciones 1-2 del jumper JP1.
* 1 Pila de litio 14500. Se deberan cortocircuitar las posiciones 2-3 del jumper JP1. El soporte para la bateria BT2 puede ser removido, liberando un poco de espacio en el PCB.
* Fuente de alimentacion externa en la bornera J1. Los soportes para baterias BT1 y BT2 pueden ser removidos, liberando aun mas espacio en el PCB.

##### Caja
El PCB tiene las dimensiones correctas para ser instalado dentro de una caja plastica "generica" a prueba de agua de **83x58x33mm** . Estas cajas vienen en multiples variantes: gris, negro, blanco, tapa transparente, salientes para montaje en pared, etc. La tarjeta se fija a la caja mediante 2 tornillos autorroscantes.

##### Expansion

<figure class="half">
	<a href="/assets/images/RAK811_NODE_EXPANSION.jpg"> <img src="/assets/images/RAK811_NODE_EXPANSION_MEDIUM.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_PINOUT.png"> <img src="/assets/images/RAK811_NODE_PINOUT.png"> </a>
	<figcaption>Area para expansion y/o prototipado.</figcaption>
</figure>

El area de prototipado contiene pads para soldadura que estan conectados a todos los pines del modulo RAK811, adicionalmente hay algunos pads libres para realizar algo de prototipado mediante cable y soldadura. Las conexiones a sensores externos se realizan mediante las borneras W, X, Y, Z. En caso que la inmensa area para prototipado no sea suficiente, se pueden soldar [regletas de conectores hembra](https://rimstar.org/science_electronics_projects/pin_headers_soldering_cutting_male_female.htm) para agregar una tarjeta de expansion desmontable.
Notese que el RAK811-LF y RAK811-HF tienen algunas diferencias en unos cuantos pines de i/o.


##### Opciones de antena
Antena interna de resorte soldada en el pad J6, se deberan cortocircuitar las posiciones 1-2 del jumper JP2.


Antena externa usando conector U.FL, se deberan cortocircuitar las posiciones 2-3 del jumper JP2. 

##### Aplicacion de ejemplo

<figure class="third">
	<a href="/assets/images/RAK811_NODE_RESISTORS.jpg"> <img src="/assets/images/RAK811_NODE_RESISTORS_MEDIUM.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_REEDSWITCH.jpg"> <img src="/assets/images/RAK811_NODE_REEDSWITCH_MEDIUM.jpg"> </a>
	<a href="/assets/images/RAK811_NODE_CLOSED.jpg"> <img src="/assets/images/RAK811_NODE_CLOSED_MEDIUM.jpg"> </a>
	<figcaption>Nodo LoRa interruptor magnetico.</figcaption>
</figure>

La aplicacion de ejemplo consiste en un interruptor magnetico LoRa que transmite un paquete cada vez que se cierra o se abre el contacto debido al efecto de acercar o alejar el iman. Para ello se instalo un reed switch pequeño en una de las paredes al interior de la caja.
La tarjeta de expansion es usada para instalar los componentes suplementarios: Led indicador de transmision, resistencias de pullup, pulsador para  prueba de transmision, y divisor de voltaje para monitoreo de bateria. 

Cualquier otro sensor de tipo interruptor ([sensor de inclinacion por esferas, resorte detector de vibracion](http://blog.vidianindhita.com/2018/02/27/all-about-tilt-switches/), etc.) puede ser agregado!

Para hacer las conexiones se uso cable con recubrimiento PVDF por su alta resistencia al calor, en especial al soldar con cautin!. 
Para mas informacion sobre el [PCB](#tarjetas-de-circuito-impreso) o el  [firmware](#software), recuerde consultar los [repositorios vinculados](#tarjetas-de-circuito-impreso)
 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Alambre 30 AWG con recubrimiento PVDF UL1423     | [💸](https://s.click.aliexpress.com/e/_eMiimB )     | [UL1423.pdf](/assets/pdf/UL1423.pdf)           |
| Conector para antena externa U.FL montaje superficial    | [💸](https://s.click.aliexpress.com/e/_eLJ9zD)     | [6474011114.pdf](/assets/pdf/6474011114.pdf)           |
| Reed switch plastico pequeño     | [💸](https://s.click.aliexpress.com/e/_eOoX6T)  | [GPS-11A.pdf](/assets/pdf/GPS-11A.pdf)                               |
| Iman para fijacion en pared mediante tornillos     | [💸](https://s.click.aliexpress.com/e/_eOmX4J )  | [MC-38.pdf](/assets/pdf/MC-38.pdf)                               |
| Sensor de vibracion tipo resorte | [💸](https://s.click.aliexpress.com/e/_etYDMP)  | [SW-18015p.pdf](/assets/pdf/SW-18015p.pdf)                               |
| Sensor de inclinacion por esferas     | [💸](https://s.click.aliexpress.com/e/_eNI7aF )  | [SW-200D.pdf](/assets/pdf/SW-200D.pdf)                               |
| Resistencias TH 1/4W 1%    | [💸](https://s.click.aliexpress.com/e/_eMCbH1)  | [MGR-SERIES.pdf](/assets/pdf/MGR-SERIES.pdf)                               |
| Led 3mm    | [💸](https://s.click.aliexpress.com/e/_eMDYML)  | [1254-10SYGD.pdf](/assets/pdf/1254-10SYGD.pdf)                               |
| Interruptor momentaneo pulsador  6x6mm  | [💸](https://s.click.aliexpress.com/e/_eKd4YV)  | [TS-1301.pdf](/assets/pdf/TS-1301.pdf)                               |
                     