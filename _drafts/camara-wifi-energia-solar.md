---
title: "Camara WiFi alimentada por energia solar"
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN006
  - Solar
  - ESP32
header:
     teaser: "/assets/images/ENERGY_HARVESTING_CAMERA_TEASER.jpg"
---

El modulo ESP32 CAM es un dispositivo economico basado en el modulo ESP32-S,un sensor de imagen OV2640 y un conector para tarjeta MicroSD. Si bien este dispositivo no viene diseñado para un bajo consumo de energia, tras una serie de modificaciones se puede llegar a un nivel aceptable para que funcione de modo intermitente alimentado por energia solar. El proyecto aqui presentado es una plataforma para experimentacion razonablemente robusta, a prueba de polvo y agua, basada en componentes comerciales listos para usar. Ideal para montajes en exteriores.

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_MEDIUM.jpg"> </a>
	<figcaption>Camara WiFi alimentada por energia solar lista para ser ubicada en exteriores</figcaption>
</figure>

Componente clave: [ESP 32 CAM](https://s.click.aliexpress.com/e/_Dde4rkL)
{: .notice--danger}


##### Reduciendo el consumo energetico

EL ESP 32 CAM no esta diseñado para ser un dispositivo de bajo consumo, sin modificacion alguna, al poner el ESP32 en deep sleep, el consumo electrico medido es de 2.8 mA lo cual deja mucho que desear. 

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_POWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_POWER_MEDIUM.jpg"> </a>
	<figcaption>Medicion de consumo en deep sleep del modulo sin modificar</figcaption>
</figure>

Algunas personas en internet ya se han aventurado a hacer este tipo de modificaciones las cuales son las siguientes:

* Remover el regulador de voltaje de 5V a 3.3 V, la camara se alimentara directamente mediante bateria LiFePO4
* Cortar la pista que alimenta la camara a 3.3 V y conectarla al MOSFET que conmuta los reguladores de 2.8V y 1.2V
* Retirar el led y conectar el GPIO33 al pin de alimentacion de 5V para poder utilizar este GPIO de forma externa.

Estas modificaciones bajan el consumo en deep sleep hasta los 0.8 mA que es escandaloso para ser llamado bajo consumo, sinembargo es un avance sustancial sobre los 2.8 mA sin modificacion alguna.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_SWTICH_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_NOREGULATORLED_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_LOWPOWER_MEDIUM.jpg"> </a>
	<figcaption>Modificaciones y resultado final</figcaption>
</figure>

##### Construccion de la plataforma

La plataforma consta de una carcasa a prueba de agua para una camara deportiva y una tarjeta de circuito impreso con las dimensiones adecuadas para ser ubicada adentro. 

<figure>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_PLATFORM_MEDIUM.jpg"> </a>
	<figcaption>Componentes de la plataforma basica</figcaption>
</figure>

La carcasa usada es bastante comun, facil de conseguir y economica. Se abre y cierra sin necesidad de tornillos y posee un punto donde se le pueden agregar diferentes tipos de accesorios para ser montada. 

La tarjeta de circuito impreso fue diseñada para ubicar el modulo ESP 32 CAM en la ventana que la carcasa dispone para la ubicacion del lente. El modulo puede ser montado en dos posiciones diferentes para maximizar el area dependiendo de los componentes a usar.

Se agrego un soporte para bateria AAA, conectores hembra para conectar/desconectar facilmente el modulo y pines en donde conectar el programador, pues esta tarjeta no cuenta con dicho circuito. Tambien se agrego un led a la tarjeta para depuracion.

<figure class="third">
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDFRONT_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_BOARDBACK_MEDIUM.jpg"> </a>
	<a href="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE.jpg"> <img src="/assets/images/ENERGY_HARVESTING_CAMERA_WITHMODULE_MEDIUM.jpg"> </a>
	<figcaption>Tarjeta con sus componentes</figcaption>
</figure>

##### Resistencias
Valores de resistencias:

HISTERESIS 3.0 V

ROV2 = 4.7 M
ROV1 = 5.1M + 240 K

VOLT OK 2.7 V

RUV1 5.1 M
RUV2 5.1 M 

UNDERV VOLT 2.5 V

ROK1 = 3.9 M + 200 K
ROK2 = 4.7 M
ROK3 = 1 M

MPPT 78%

ROC1 5.6 M + 10 M
ROC2 4.42 M

OVERTEMPERATURE
(GROUND) 60 C 

La idea de usar LoRa para comunicacion satelital fue evidente para muchas personas por estas razones:

* Uso de bandas sin licencia ([ISM](https://es.wikipedia.org/wiki/Banda_ISM))
* Modulos listos para usar, faciles de conseguir y a relativamente bajo costo.
* Comunicacion a muy larga distancia, con bajo consumo de potencia.
* Se puede establecer enlaces con un nivel de señal tan bajo como -120dBm.

Este ultimo punto es de vital importancia, pues permite usar una gran cantidad de antenas comerciales, incluso de construccion casera, que aunque
no muy eficientes, pueden cumplir la funcion de recibir dichas señales. Esto habia sido uno de los grandes talones de aquiles en
las comunicaciones satelitales hasta entonces.


#### ¿De que trata este proyecto?

Este proyecto es un Gateway o Pasarela entre internet (WiFI) y LoRa @ 433Mhz, usando la mayor cantidad posible de elementos comerciales listos para usar ([Commercial-Off-The-Shelf](https://es.wikipedia.org/wiki/Componente_salido_del_estante)) de forma tal que no se requiera mucha experticia para su construccion. El toque final sera agregar el [firmware de TinyGS](https://github.com/G4lile0/tinyGS), el cual permitira entre otras cosas:

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
	<figcaption>Un poquito de knolling. ¡No es mucho, pero es trabajo honesto!</figcaption>
</figure>

| Componente        | Enlace de compra | Hoja de datos                                   |
| -------- | ------ | ------------------------------------------------------------ |
| Kit LoRa Heltec WiFi 32 v2 433mhz | [compralo aqui](https://s.click.aliexpress.com/e/_A0wUdR) | [WiFi-LoRa-32-V2-433-470-510.pdf](/assets/pdf/WiFi-LoRa-32-V2-433-470-510.pdf) |
| Brida RP-SMA con extension de cable a conector U.FL | [compralo aqui](https://s.click.aliexpress.com/e/_9vbEjm) | [Catalog_SMA.pdf](/assets/pdf/Catalog_SMA.pdf) |
| Antena SMA 433 Mhz  | [compralo aqui](https://s.click.aliexpress.com/e/_AYvZau) | [433_MHZ_SMA_ANTENNA.pdf](/assets/pdf/433_MHZ_SMA_ANTENNA.pdf) |
| Caja generica a prueba de agua "Sonoff" 100x68x50mm | [compralo aqui](https://s.click.aliexpress.com/e/_AtukwZ) | [SONOFF-IP66-waterproof-case.pdf](/assets/pdf/SONOFF-IP66-waterproof-case.pdf) |
| Tornillo Phillips M2.5 avellanado | [compralo aqui](https://s.click.aliexpress.com/e/_AEYxys) | [M2-5_COUNTERSUNK_SCREW.pdf](/assets/pdf/M2-5_COUNTERSUNK_SCREW.pdf) |
| Tuerca de seguridad M2.5 | [compralo aqui](https://s.click.aliexpress.com/e/_9RIfcu) | [M2-5_NYLON_LOCK_NUT.pdf](/assets/pdf/M2-5_NYLON_LOCK_NUT.pdf) |
| Tornillo con punta tipo B M2.6 autorroscante | [compralo aqui](https://s.click.aliexpress.com/e/_esHHyb) | [M2.6x5-6-8-12mm.pdf](/assets/pdf/M2.6x5-6-8-12mm.pdf) |
| Terminal de tornillo para PCB kf350 3.5mm 3 pines | [compralo aqui](https://s.click.aliexpress.com/e/_eLjzKB) | [KF350.pdf](/assets/pdf/KF350.pdf) |
| Conector tipo header hembra 2.54mm | [compralo aqui](https://s.click.aliexpress.com/e/_eNYVzN) | [FHA3-S1XX.pdf](/assets/pdf/FHA3-S1XX.pdf) |
| Cable calibre 30 AWG tipo UL1423 PVDF | [compralo aqui](https://s.click.aliexpress.com/e/_eL2EYB) | [UL1423.pdf](/assets/pdf/UL1423.pdf) |
| Inyector Poe 48V 0.5A  | [compralo aqui](https://s.click.aliexpress.com/e/_Dl1hpWX) | [PoE-injector-48V-05A.pdf](/assets/pdf/PoE-injector-48V-05A.pdf)|
| Modulo PoE Splitter D1398 5V 2A  | [compralo aqui](https://s.click.aliexpress.com/e/_Al2dql) | [WC-PD13C050I.pdf](/assets/pdf/WC-PD13C050I.pdf)|
| Adaptador SMA hembra a RP-SMA Macho | [compralo aqui](https://s.click.aliexpress.com/e/_9JKRaz) | [SMA-Female-To-RP-SMA-Male-adapter.pdf](/assets/pdf/SMA-Female-To-RP-SMA-Male-adapter.pdf) |
| Sellante de silicona Neutro | [compralo aqui](https://s.click.aliexpress.com/e/_ANKQnb) | [Neutral-cure-silicone.pdf](/assets/pdf/Neutral-cure-silicone.pdf) |
| Cinta autofundente | [compralo aqui](https://s.click.aliexpress.com/e/_DlbGSST) | [Waterproof-silicone-self-fusing-vulcanizing-tape.pdf](/assets/pdf/Waterproof-silicone-self-fusing-vulcanizing-tape.pdf) |


| Tarjeta de circuito impreso (PCB) | Enlace de compra | Repositorio con archivos fuente  |
| --------------------------------- | ---------------- | ------------------------------- |
| Tarjeta prototipo para caja de 100x68mm | [compralo aqui](https://www.pcbway.com/project/shareproject/mcu_proto_100x68mm_6ae31333.html) | [mcu-proto-100x68mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-100x68mm) |

| Software | repositorio |
| ----------------------- | ---------------- |
| Firmware para estacion terrena TingyGS | [descargalo aqui](https://github.com/G4lile0/tinyGS) |

| Herramientas opcionales | Enlace de compra | Hoja de datos |
| ----------------------- | ---------------- | ------------------------------- |
| Taladro manual y juego de brocas de multiples diametros 0.5-3mm | [compralo aqui](https://s.click.aliexpress.com/e/_DBPw6on) | [Hand-drill-set-mini.pdf](/assets/pdf/Hand-drill-set-mini.pdf) |


##### Ensamblaje:

Este articulo no pretende ser una guia de ensamblaje paso a paso, sino que tratara de explicar de forma general las acciones a realizar. Dependiendo de los materiales obtenidos algunas instrucciones y el orden de ejecucion de ellas podrian cambiar un poco!

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

Existen dos posibilidades para alimentar la estacion, mediante una fuente simple de 5V y mediante un adaptador PoE. La opcion que usa fuente de 5v es la que menos hardware requiere, pero esta limitada a un cable de unos cuantos metros, en cambio la version con PoE, requiere una fuente PoE y un splitter PoE dentro de la caja, pero pueden usarse cables de hasta 100 metros de longitud!.

<figure>
	<a href="/assets/images/tinygs_power_wires_blockdiag.png"> <img src="/assets/images/tinygs_power_wires_blockdiag.png"> </a>
	<figcaption>Diagrama simplificado de las conexiones electricas</figcaption>
</figure>

* Soldar conectores header para el modulo LoRa. Esto no es 100% necesario, pues el modulo podria soldarse directamente a la tarjeta de circuito impreso, sin embargo, usar los headers permite que el modulo pueda ser retirado en cualquier momento. 
* Soldar conectores header para el modulo splitter PoE (¡en caso que se use uno!).
* Soldar terminales de tornillo a la PCB para permitir una conexion/desconexion del cable electrico de forma facil. 
* Realizar las conexiones electricas por debajo de la tarjeta, en lo posible usando cable con recubrimiento PVDF, entre las terminales de tornillo y los pines de poder del modulo PoE y el modulo LoRa.

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
	<figcaption>Todos los componentes fijos dentro de la caja</figcaption>
</figure>

###### Descargar el firmware.

Una vez verificada la correcta conexion electrica al modulo LoRa, (generalmente estos modulos vienen con un firmware de prueba y deberian mostrar algun tipo de logo/imagen/datos en la pantalla LCD al enchufar la alimentacion), conectar el modulo LoRa mediante un cable Micro USB a un computador personal y seguir las instrucciones que se encuentran en la [Wiki de TinyGS](https://github.com/G4lile0/tinyGS/wiki).

<figure>
	<a href="/assets/images/LORA_GROUND_STATION_FW.jpg"> <img src="/assets/images/LORA_GROUND_STATION_FW_MEDIUM.jpg"> </a>
	<figcaption>¡Firmware de TinyGS instalado!</figcaption>
</figure>

###### Ubicacion de la antena.

La antena debera ubicarse donde tenga una mayor vista del cielo (en el techo o mediante un poste muy largo) y en lo posible alejada de paredes y de estructuras metalicas. Dependiendo de nuestra vivienda esto podria no ser posible, asi que se debera hacer varias pruebas en ventanas para ver cual nos da mejor resultado. 

Si se quiere poner la caja a la intemperie, se debera sellar el segundo agujero de la caja con un trozo de caucho, igualmente se debera usar cinta de caucho autofundente para cubrir las partes metalicas de la antena y usar un poco de silicona neutra en los tornillos. Evitar usar silicona acida (la que tiene un olor a vinagre) pues esta tiende a oxidar los tornillos y partes metalicas

###### Resultados obtenidos.

Dadas las condiciones logisticas especificas de esta prueba, no era posible acceder al techo de la edificacion, ni instalar estructuras permanentes por fuera de las ventanas, por lo tanto, se decidio probar el siguiente configuracion: La caja con el receptor estaria dentro de la edificacion y la antena, la cual tiene un iman y puede ser montada/desmontada con facilidad, estaria afuera de la ventana sobre la reja. 

La antena fue comprada en un comercio electronico local, no tiene ningun tipo de ajuste ni optimizacion. La prueba fue realizada en Cali, Colombia y el registro de mayor distancia recibida hasta la fecha fue desde el satelite [NORBY](https://tinygs.com/satellite/Norbi) cuando volaba sobre Arequipa, Peru, aproximadamente 2265 Kilometros en linea recta hacia el satelite, ¡nada mal para un receptor satelital cuyo costo ronda los 40 EUR, fue ensamblado en casa y que no requirio ningun tipo de ajuste!

<figure class="third">
	<a href="/assets/images/TINYGS_WINDOW_SETUP.jpg"> <img src="/assets/images/TINYGS_WINDOW_SETUP_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_WINDOW_ANTENNA.jpg"> <img src="/assets/images/TINYGS_WINDOW_ANTENNA_MEDIUM.jpg"> </a>
	<a href="/assets/images/TYNYGS_ANTENNA_RECEPTION.jpg"> <img src="/assets/images/TYNYGS_ANTENNA_RECEPTION_MEDIUM.jpg"> </a>
	<figcaption>Setup de la estacion terrena en funcionamiento</figcaption>
</figure>

###### Variantes.

Se desarrollo una version portatil de la estacion terrena, que usa una caja un poco mas pequeña y se alimenta mediante una bateria. Esta pensada para ser una estacion movil-temporal que se conecte a un WiFi de un telefono celular. Utiliza una bateria [LiFePo4](https://es.wikipedia.org/wiki/Bater%C3%ADa_de_litio-ferrofosfato) de 3.2 voltios, por lo tanto, no se requiere un regulador, la bateria va directamente conectada al pin de 3.3v del modulo LoRa. 

Este mismo hardware (tanto el fijo, como el portatil) pueden ser usados para otro tipo de proyectos, por ejemplo para el proyecto [aprs.fi](https://aprs.fi/), el cual es de especial interes para radioaficionados. El hardware es 100% compatible y solo requiere cambiar el firmware por [este](https://github.com/lora-aprs/LoRa_APRS_iGate).

<figure class="third">
	<a href="/assets/images/TINYGS_PORTABLE_PCB.jpg"> <img src="/assets/images/TINYGS_PORTABLE_PCB_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_WIRED.jpg"> <img src="/assets/images/TINYGS_PORTABLE_WIRED_MEDIUM.jpg"> </a>
	<a href="/assets/images/TINYGS_PORTABLE_FW.jpg"> <img src="/assets/images/TINYGS_PORTABLE_FW_MEDIUM.jpg"> </a>
	<figcaption>Detalle de la estacion terrena portatil</figcaption>
</figure>

| Componentes adicionales para version movil| Enlace de compra | Hoja de datos           |
| ------------ | ------ | ------------------------------------------------------------ |
| Caja generica a prueba de agua 83x58x33mm  | [compralo aqui](https://s.click.aliexpress.com/e/_Ad6Gxn) | [AK10019-A1.pdf](/assets/pdf/AK10019-A1.pdf) |
| Conector para bateria AA para PCB | [compralo aqui](https://s.click.aliexpress.com/e/_A0wUdR) | [BH311.pdf](/assets/pdf/BH311.pdf) |
| Bateria recargable Lifepo4 3.2V 14500 AA | [compralo aqui](https://s.click.aliexpress.com/e/_Asl8pn) | [Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf](/assets/pdf/Lifepo4-3.2V-14500-Rechargeable-battery-AA.pdf) |


| Tarjeta de circuito impreso (PCB) | Enlace de compra | Repositorio con archivos fuente  |
| --------------------------------- | ---------------- | ------------------------------- |
| Tarjeta prototipo para caja de 83x58mm | [compralo aqui](https://www.pcbway.com/project/shareproject/mcu_proto_83x58mm_16815998.html) | [mcu-proto-100x68mm](https://github.com/galopago/misistemote/tree/main/mcu-proto-83x58mm) |


