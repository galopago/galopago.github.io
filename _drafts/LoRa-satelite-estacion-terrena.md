---
title: "Estacion terrena para recepcion de satelites LoRa"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN005
  - LoRa
  - ESP32
header:
     teaser: "/assets/images/LORA_GROUND_STATION_TEASER.jpg"
---

Los [pequeños satelites](https://es.wikipedia.org/wiki/Sat%C3%A9lite_peque%C3%B1o) que en la actualidad usan tecnologia [LoRa](https://en.wikipedia.org/wiki/LoRa) han logrado que personas con pocos conocimientos tecnicos y con un bajo presupuesto puedan recibir sus señales, algo que era imposible hace algunos años. Gracias a la iniciativa [TinyGS](https://tinygs.com) se ha construido una red abierta de estaciones terrenas distribuidas por todo el mundo y que pueden ser construidas facilmente para ampliar dicha cobertura. El proyecto aqui presentado es una implementacion razonalmente robusta, a prueba de polvo y agua, basada en componentes comerciales listos para usar. Ideal para montajes en exteriores.

<figure>
	<a href="/assets/images/LORA_GROUND_STATION.jpg"> <img src="/assets/images/LORA_GROUND_STATION_MEDIUM.jpg"> </a>
	<figcaption>Estacion de tierra lista para ser montada en exteriores</figcaption>
</figure>

Componente clave: [Heltec WiFi LoRa kit 32 v2 433mhz](https://s.click.aliexpress.com/e/_A0wUdR)
{: .notice--danger}


##### ¿Por que?:

La idea de usar LoRa para comunicacion satelital fue evidente para muchas personas por estas razones:

* Uso de bandas sin licensia (ISM)
* Modulos listos para usar, faciles de conseguir y a relativamente bajo costo.
* Comunicacion a muy larga distancia, con bajo consumo de potencia.
* Se puede establecer comunicacion con un nivel de señal tan bajo como -120dBm.

Este ultimo punto es de vital importancia, pues permite usar una gran cantidad de antenas comerciales, e incluso de construccion casera, que aunque
no muy eficientes, estas pueden llegar a cumplir la funcion de recibir dichas señales. Este en general habia sido uno de los grandes talones de aquiles en
las comunicaciones satelitales hasta entonces.


#### ¿De que trata este proyecto?

Este proyecto es un Gateway o Pasarela entre internet (WiFI) y LoRa @ 433Mhz, usando la mayor cantidad posible de elementos comerciales listos para usar (off the shelf) de forma tal que no se requiera mucha experticia para su construccion. El toque final sera agregar el [firmware de TinyGS](https://github.com/G4lile0/tinyGS) el cual permitira entre otras cosas:

* Recibir actualizaciones de firmware inalambricamente (OTA) automaticamente.
* El receptor se sintonizara automagicamente para recibir las señales del satelite que este mas cerca "a la vista".
* Configuracion de parametros via interfaz web (local).

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_TINYGS.png"> <img src="/assets/images/LORA_GROUND_STATION_TINYGS.png"> </a>
	<figcaption>Arquitectura de la red TinyGS (tomado del sitio de TinyGS)</figcaption>
</figure>

#### Listado de materiales

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_PARTS.jpg"> <img src="/assets/images/LORA_GROUND_STATION_PARTS_MEDIUM.jpg"> </a>
	<figcaption>Un poquito de knolling. No es mucho, pero es trabajo honesto!</figcaption>
</figure>

| Componente        | Enlace de compra | Hoja de datos                                   |
| -------- | ------ | ------------------------------------------------------------ |
| kit LoRa Heltec WiFi 32 v2 433mhz | [compralo aqui](https://s.click.aliexpress.com/e/_A0wUdR) | [WiFi-LoRa-32-V2-433-470-510.pdf](/assets/pdf/WiFi-LoRa-32-V2-433-470-510.pdf) |
| RP-SMA flange to U.FL pigtail | [compralo aqui](https://s.click.aliexpress.com/e/_9vbEjm) | [Catalog_SMA.pdf](/assets/pdf/Catalog_SMA.pdf) |
| Antena SMA 433 Mhz  | [compralo aqui](https://s.click.aliexpress.com/e/_AYvZau) | [433_MHZ_SMA_ANTENNA.pdf](/assets/pdf/433_MHZ_SMA_ANTENNA.pdf) |
| Caja generica a prueba de agua "Sonoff" 100x68x50mm | [compralo aqui](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf) |
| Tornillo phillips M2.5 avellanado | [compralo aqui](https://s.click.aliexpress.com/e/_AEYxys) | [M2-5_COUNTERSUNK_SCREW.pdf](/assets/pdf/M2-5_COUNTERSUNK_SCREW.pdf) |
| Tuerca de seguridad M2.5 | [compralo aqui](https://s.click.aliexpress.com/e/_9RIfcu) | [M2-5_NYLON_LOCK_NUT.pdf](/assets/pdf/M2-5_NYLON_LOCK_NUT.pdf) |
| Tornillo tipo B M2.6 autorroscante | [compralo aqui](https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Terminal de tornillo para PCB kf350 3.5mm 3 pines | [compralo aqui](https://s.click.aliexpress.com/e/_eLjzKB) | [KF350.pdf](/assets/pdf/KF350.pdf) |
| Conector tipo header hembra 2.54mm | [compralo aqui](https://s.click.aliexpress.com/e/_eNYVzN) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Cable calibre 30 AWG tipo UL1423 PVDF | [compralo aqui](https://s.click.aliexpress.com/e/_eL2EYB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| Modulo PoE Splitter D1398 5V 2A  | [compralo aqui](https://s.click.aliexpress.com/e/_Al2dql) | [WC-PD13C050I.pdf](/assets/pdf/WC-PD13C050I.pdf)|
| Adaptador SMA hembra a RP-SMA Macho | [compralo aqui](https://s.click.aliexpress.com/e/_9JKRaz) | [SMA-Female-To-RP-SMA-Male-adapter.pdf](/assets/pdf/SMA-Female-To-RP-SMA-Male-adapter.pdf) |
| Sellante de silicona Neutro | [compralo aqui](https://s.click.aliexpress.com/e/_ANKQnb) | [Neutral-cure-silicone.pdf](/assets/pdf/Neutral-cure-silicone.pdf) |


##### Ensamblaje:

Si bien el articulo no pretende ser una guia de ensamblaje paso a paso, si tratara de explicar lo mas posible algunos pasos claves. Dependiendo
de los materiales obtenidos algunas instrucciones y el orden de ejecucion de ellas podrian cambiar un poco!

###### Perforaciones para el conector de antena:

* Realizar 4 perforaciones con una broca de diametro ligeramente superior a 2.5 mm por donde pasaran los tornillos de fijacion. 
* Realizar otra perforacion en la mitad por donde pasara el cable del conector de antena con una broca de aproximadamente 4mm de diametro. La plantilla para la perforacion de dichos agujeros puede hallarse [aqui](https://github.com/galopago/panel-mount-drill-layouts/tree/main/sma-flange-4-holes).

<figure class="third">
	<a href="/assets/images/SMA_FLANGE_TEMPLATE.jpg"> <img src="/assets/images/SMA_FLANGE_TEMPLATE_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANGE_FRONT.jpg"> <img src="/assets/images/SMA_FLANGE_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/SMA_FLANTE_DIAG.jpg"> <img src="/assets/images/SMA_FLANTE_DIAG_MEDIUM.jpg"> </a>
	<figcaption>Perforaciones para el conector de antena</figcaption>
</figure>

###### Soldar conectores y cables a la tarjeta de circuito impreso:

Existen dos posibilidades para alimentar la estacion, mediante una fuente simple de 5V y mediante un adaptador PoE. La que usa fuente de 5v es la que menos hardware requiere, pero esta limitada a un cable de unos cuantos metros, en cambio la version con PoE, requiere una fuente PoE y un splitter poe dentro de la caja, pero pueden usarse cables de hasta 100 metros de longitud!.

<figure>
	<a href="/assets/images/tinygs_power_wires_blockdiag.png"> <img src="/assets/images/tinygs_power_wires_blockdiag.png"> </a>
	<figcaption>Diagrama simplificado de las conexiones electricas</figcaption>
</figure>

* Soldar conectores header para el modulo LoRa. Esto no es 100% necesario, pues el modulo podria soldarse directamente a la tarjeta de circuito impreso, sinembargo usar los headers permite que el modulo pueda ser retirado en cualquier momento. 
* Soldar conectores header al modulo splitter PoE (en caso que se use uno!).
* Soldar terminales de tornillo a PCB para permitir una conexion/desconexion de forma facil. 
* Realizar las conexiones electricas por debajo de la tarjeta, en lo posible usando cable con recubrimiento PVDF, entre las terminales de tornillo y los pines de de poder del modulo PoE y el modulo LoRa.

<figure class="third">
	<a href="/assets/images/PCB_BARE.jpg"> <img src="/assets/images/PCB_BARE_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_CONNECTORS.jpg"> <img src="/assets/images/PCB_CONNECTORS_MEDIUM.jpg"> </a>
	<a href="/assets/images/PCB_POWER_WIRES.jpg"> <img src="/assets/images/PCB_POWER_WIRES_MEDIUM.jpg"> </a>
	<figcaption>Soldaduras realizadas</figcaption>
</figure>

###### Fijar conector de antena, tarjeta de circuito impreso y cables de poder.

* Fijar el conector de antena mediante las 4 tuercas de seguridad. 
* Introducir los cables de alimentacion por dentro de los conectores pasacables y dejar un poco flojas las tuercas plasticas de ajuste.
* Introducir la tarjeta de circuito impreso, ajustarla a la caja mediante los tornillos autorroscantes.
* Conectar los cables de alimentacion a las bornera tornillo, el cable de la antena al modulo LoRa y ajustar los conectores pasacables. Es probable que se tenga que experimentar un poco con los pasos anteriormente mencionados para buscar la forma mas comoda de ensamblar!

<figure class="third">
	<a href="/assets/images/TINYGS_ANT_CONNECTOR_FRONT.jpg"> <img src="/assets/images/TINYGS_ANT_CONNECTOR_FRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_POWER_CABLES.jpg"> <img src="/assets/images/TINYGS_POWER_CABLES_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PCB_FIXED.jpg"> <img src="/assets/images/TINYGS_PCB_FIXED_MEDIUM.jpg"> </a>
	<figcaption>todos los componentes fijos dentro de la caja</figcaption>
</figure>

###### Descargar firmware.

Una vez verifida la correcta conexion electrica al modulo LoRa, (generalmente estos modulos vienen con un fimrware de prueba y deberia mostrarse algun tipo de logo/imagen/datos en la pantalla LCD), conectar el modulo LoRa mediante un cable Micro USB a un computador personal. Seguir las instrucciones que se encuentran en la [Wiki de TinyGS](https://github.com/G4lile0/tinyGS/wiki).

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_FW.jpg"> <img src="/assets/images/LORA_GROUND_STATION_FW_MEDIUM.jpg"> </a>
	<figcaption>Firmware de TinyGS instalado!</figcaption>
</figure>

###### Ubicacion de la antena.

La antena debera ubicarse donde tenga una mayor vista del cielo (en el techo o mediante un poste muy largo) y en lo posible alejada de paredes y de estructuras metalicas. Esto siempre no es posible dependiendo dependiendo de nuestra vivienda, asi que se debera hacer varias pruebas para ver cual nos da mejor resultado. Si se quiere poner la caja a la intemperie, se debera sellar el segundo agujero de la caja con un trozo de caucho, igualmente se debera usar cinta de caucho autofundente para cubrir las partes metalicas y usar un poco de silicona neutra en los tornillos. Evitar usar silicona acida (la que tiene un olor a vinagre) pues esta tiende a oxidar los tornillos y partes metalicas

###### Resultados obtenidos.

Dadas las condiciones logisticas especificas de esta prueba, no era posible acceder al techo de la edificacion, ni instalar estructuras permanentes por fuera de las ventanas, se decidio probar el siguiente configuracion: La caja con el receptor estaria dentro de la edificacion y la antena, la cual tiene un iman y puede ser montada/desmontada con facilidad, estaria afuera de la ventana sobre la reja. Dicha antena fue comprada en un comercio electronico local, no tiene ningun tipo de ajuste ni optimizacion. La prueba fue realizada en Cali, Colombia y el registro de mayor distancia recibida hasta la fecha fue desde el satelite NORBY cuando volaba sobre Arequipa, Peru, aproximadamente 2265 Kilometros en linea recta hacia el satelite!, nada mal para un receptor satelital cuyo costo es ~40 EUR, ensamblado en casa y que no requirio ningun tipo de ajuste!


<figure class="third">
	<a href="/assets/images/TINYGS_WINDOW_SETUP.jpg"> <img src="/assets/images/TINYGS_WINDOW_SETUP.jpg"> </a>
	<a href="/assets/images/TINYGS_WINDOW_ANTENNA.jpg"> <img src="/assets/images/TINYGS_WINDOW_ANTENNA_MEDIUM.jpg"> </a>
	<a href="/assets/images/TYNYGS_ANTENNA_RECEPTION.jpg"> <img src="/assets/images/TYNYGS_ANTENNA_RECEPTION_MEDIUM.jpg"> </a>
	<figcaption>Setup de la estacion terrena en funcionamiento</figcaption>
</figure>




#### Componentes MISISTEMOTE

| PCB    |  Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Placa trasera para montaje A02 para caja de 200x120x75mm | [A02](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)           |
| Placa adaptadora A05 con agujeros espaciados 10.16mm para fuente 5V 3.8A   | [A05](https://github.com/galopago/TUSISTEMITA/tree/master/A_BACKPLATES)        |
| Tarjeta B01 para conexiones mediante terminales de tornillos 2x4 3.5mm | [B01](https://github.com/galopago/TUSISTEMITA/tree/master/B_SCREW_TERMINAL_WIRE_CONNECTORS)        |
| Tarjeta breakout C08 con salida a terminales de tornillos para NODEMCU V3  | [C08](https://github.com/galopago/TUSISTEMITA/tree/master/C_BREAKOUTS)        |
| Tarjeta D06 de conversion de niveles logicos  | [D06](https://github.com/galopago/TUSISTEMITA/tree/master/D_ELECTRONICS)        |


#### Software

| Software    | Archivos fuente                                          | 
| -------- | ------------------------------------------------------------ |
| Firmware    | [MOS_IOT_ADDRESSABLE_LEDS](https://github.com/galopago/MOS_IOT_ADDRESSABLE_LEDS)           |

 

## Componentes opcionales:

| Componente         | Consigue el tuyo! | Hoja de caracteristicas                                          | 
| -------- | ------ | ------------------------------------------------------------ |
| Juego de 3 brocas escalonadas 3-20 mm + centropunto  | [💸](https://s.click.aliexpress.com/e/_AalUrz)     | [3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf](/assets/pdf/3_pc_set_3-20mm_drill_bit_incremental_center_punch.pdf)           |
| Broca escalonada de 8 pasos 10-45 mm    | [💸](https://s.click.aliexpress.com/e/_ATtnjt)     | [8_steps_10-45mm_incremental_drill_bit.pdf](/assets/pdf/8_steps_10-45mm_incremental_drill_bit.pdf)           |
