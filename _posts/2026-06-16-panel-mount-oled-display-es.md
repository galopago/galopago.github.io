---
title: 'Pantalla OLED 0,96" para montaje en panel con terminales de tornillo'
excerpt_separator: "<!--more-->"
classes: wide
categories:
  - espanol
tags:
  - AN009
  - Prototipado
header:
  teaser: "/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_TEASER.jpg"
---

Los módulos OLED pequeños parecen intercambiables, pero los huecos de montaje y el recorte del panel necesario para que salga la pantalla rara vez coinciden entre fabricantes. Un montaje limpio suele exigir una ventana cuadrada muy precisa más cuatro agujeros para tornillos. Esas medidas cambian de un módulo a otro.

<figure>
  <a href="/assets/images/AN009/FIG_P0001_1.jpg">
    <img src="/assets/images/AN009/FIG_P0001_1_MEDIUM.jpg">
  </a>
  <figcaption>Diferencias sutiles en las distancias entre pantallas de distintos fabricantes</figcaption>
</figure>

Este proyecto integra una pantalla OLED I2C de 0,96" sin módulo de procesamiento intermedio dentro de una carcasa de montaje en panel de 48×29 mm con [terminales de tornillo](https://ilardia.com/blog/que-son-los-bornes-de-conexion-electrica). Se construye una única vez entre prototipos sin volver a soldar ni crimpar cables específicos.

##### Concepto
Los instrumentos de panel de 48×29 mm comparten un semi-estándar práctico: un único recorte rectangular, pestañas internas y un bisel frontal que disimula bordes imperfectos. La inspiración vino de medidores DC económicos, incluido el conocido “9 en 1” de voltaje/corriente/potencia, que ya usan dos tarjetas internas.

<figure>
  <a href="/assets/images/AN009/FIG_P0003_1.jpg">
    <img src="/assets/images/AN009/FIG_P0003_1_MEDIUM.jpg">
  </a>
  <figcaption>Voltímetro digital de montaje en panel</figcaption>
</figure>

Tras buscar un producto listo que combinara montaje en panel, pantalla I2C «sin inteligencia» y terminales de tornillo robustos, no apareció nada viable en cantidades de hobby. Como referencia se tomó el medidor múltiple «9 en 1» de voltaje, corriente y potencia en DC, en carcasa de panel 48×29 mm.

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
  <figcaption>Cómo está hecho por dentro el medidor 9 en 1</figcaption>
</figure>

Componente clave: [0,96″ OLED 128x64 bare screen I2C.](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen)
{: .notice--danger}

<figure>
  <a href="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY.jpg">
    <img src="/assets/images/AN009/PANEL_MOUNT_OLED_DISPLAY_MEDIUM.jpg">
  </a>
  <figcaption>Módulo OLED para montaje en panel ensamblado en carcasa 48x29 mm</figcaption>
</figure>

#### Características clave:
* Hardware de código abierto: [fuentes KiCad y Gerbers en GitHub](https://github.com/galopago/panel-mount-oled-display)
* Interfaz I2C directa (sin MCU en la placa)
* Bisel 48×29 mm tolerante a un recorte poco preciso
* Seis LEDs indicadores 0805 con terminales de ánodo y cátodo independientes
* Terminales de tornillo 3,5 mm de doble nivel para cable sólido, multifilar o Dupont
* Dos tarjetas apiladas: soldar una vez, cablear muchas veces

#### Lista de materiales

| Componente | Comprar | Datasheet |
| ---------- | ------- | --------- |
| SMD capacitor kit (0805) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=smd%200805%20capacitor%20kit) | [smd-capacitors.pdf](/assets/pdf/smd-capacitors.pdf) |
| SMD LED (0805) | [Comprar](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=led%20smd%200805) | [smd-led-0805.pdf](/assets/pdf/smd-led-0805.pdf) |
| SMD diode 1N4148 | [Comprar](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%20led%201n4148%20melf) | [smd-diode-1n4148-melf.pdf](/assets/pdf/smd-diode-1n4148-melf.pdf) |
| SMD resistor kit (0805) | [Comprar](https://s.click.aliexpress.com/e/_c4T1PYI9?SearchText=smd%200805%20resistor%20kit) | [smd-resistors.pdf](/assets/pdf/smd-resistors.pdf) |
| Pin header 1x8 2.54 mm (male) | [Comprar](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=single%20row%20pin%20header%202.54) | [single-row-male-header-2-54-pitch.pdf](/assets/pdf/single-row-male-header-2-54-pitch.pdf) |
| PCB screw terminal double level 3.5 mm (2x8) | [Comprar](https://s.click.aliexpress.com/e/_c2vg3QZ7?SearchText=KF128A-3.5) | [pcb-screw-terminal-double-level-3-5.pdf](/assets/pdf/pcb-screw-terminal-double-level-3-5.pdf) |
| 0,96″ OLED 128x64 bare screen I2C | [Comprar](https://s.click.aliexpress.com/e/_c4oPdlbb?SearchText=0.96%20i2c%20128x64%20oled%20display%20bare%20screen) | [oled-0-96-i2c-128x64-bare-screen.pdf](/assets/pdf/oled-0-96-i2c-128x64-bare-screen.pdf) |
| XC6206 3.3 V LDO regulator (SOT-23) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=XC6206P332%20sot%2023) | [xc6206.pdf](/assets/pdf/xc6206.pdf) |

#### Circuitos impresos

| PCB | Archivos fuente |
| --- | --------------- |
| Tarjeta display (OLED, regulador, LEDs) | [panel-mount-oled-display/display-board](https://github.com/galopago/panel-mount-oled-display/tree/main/display-board) |
| Tarjeta conector (terminales de tornillo) | [panel-mount-oled-display/connector-board](https://github.com/galopago/panel-mount-oled-display/tree/main/connector-board) |

#### Diseño electrónico
El diseño reparte la función entre dos tarjetas unidas por un header 1×8. En la tarjeta display van el regulador XC6206 a 3,3 V, la red de auto-reset de la OLED, el acoplamiento I2C, algunos condensadores usados por el conversor interno DC/DC de la pantalla y seis LEDs con terminales independientes. La tarjeta conector solo enruta hacia los terminales de tornillo de doble nivel. Los esquemáticos completos y las notas de diseño están en el [repositorio de GitHub](https://github.com/galopago/panel-mount-oled-display).

<figure>
  <a href="/assets/images/AN009/SCHEMATIC.png">
    <img src="/assets/images/AN009/SCHEMATIC.png">
  </a>
  <figcaption>Esquemático (tarjetas display y conector)</figcaption>
</figure>

#### Ensamblaje
El montaje manual sigue el esquema de dos tarjetas del medidor “9 en 1”: primero se soldan los componentes SMD en ambas PCBs. En la tarjeta display va la OLED de cable flex (0,7 mm, 30 pines), el XC6206, el auto-reset y los seis LEDs; en la tarjeta conector, los terminales de tornillo de doble nivel. El paso que más cuidado pide es soldar el flex de la pantalla con punta de cautín en T; el resto es soldadura SMD habitual.

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
  <figcaption>Montaje de componentes en las dos tarjetas</figcaption>
</figure>

Las dos tarjetas se unen con headers 1×8 y un espaciador entre ellas, de modo que los terminales queden accesibles por un lateral.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_2.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_2_MEDIUM.jpg">
  </a>
  <figcaption>Tarjetas display y conector apiladas con conectores header y separadores</figcaption>
</figure>

La carcasa procede de un medidor de panel 48×29 mm (el más barato que encuentres): se retira la electrónica original y se reutiliza el frontal, incluida la lámina de acrílico si sirve, o una pieza nueva oscura y translúcida de hasta 1 mm. El conjunto de tarjetas se introduce en la carcasa; las pestañas internas sujetan el módulo sin tornillos adicionales en el panel.

<figure>
  <a href="/assets/images/AN009/ASSEMBLY_3.jpg">
    <img src="/assets/images/AN009/ASSEMBLY_3_MEDIUM.jpg">
  </a>
  <figcaption>Conjunto de tarjetas instalado dentro de la carcasa</figcaption>
</figure>

#### Software
El módulo no incluye firmware. Cualquier host con I2C (Arduino, RPi Pico, ESP32, etc.) puede manejar la pantalla compatible con SSD1306 y los seis LEDs mediante los terminales de tornillo.

### Personalización
El diseño admite variaciones en alimentación y en el uso de los LEDs indicadores. También hay una resistencia que se puede cambiar de sitio para escoger entre dos posibles direcciones del bus I2C.

##### Fuente de alimentación
El XC6206 de la placa genera 3,3 V para la OLED desde los terminales VCC/GND. Alimentar dentro de las especificaciones del regulador y del display (típicamente 3,3-5 V en entrada, según la variante de XC6206 montada).

##### Expansión
Seis LEDs 0805 disponen de terminales de ánodo y cátodo independientes, de modo que cada indicador puede pertenecer a un circuito o tierra distinta. La fila inferior de terminales es algo incómoda con conectores Dupont, pero una vez insertados quedan firmes.

<figure>
  <a href="/assets/images/AN009/FIG_P0012_1.jpg">
    <img src="/assets/images/AN009/FIG_P0012_1_MEDIUM.jpg">
  </a>
  <figcaption>Dos LEDs iluminándose: izquierda en posición media y derecha en posición inferior</figcaption>
</figure>

##### Aplicación de ejemplo
Montar el módulo en un panel o caja de instrumentación y cablear I2C (SCL, SDA, VCC, GND) del microcontrolador a los terminales de tornillo. Conectar uno o más pares de LEDs a señales de estado (alimentación, alarma, modo, etc.) con retornos independientes si hace falta. Al terminar el proyecto, desatornillar los cables y reutilizar el mismo conjunto en el siguiente prototipo.

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
  <figcaption>Detalle del hueco cuadrado para montaje de la pantalla</figcaption>
</figure>

## Componentes opcionales:

| Componente | Comprar | Datasheet |
| -------- | -------- | -------- |
| 48x29 mm panel meter (donor enclosure) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=panel%20digital%20voltmeter) | [48x29mm-digital-voltmeter.pdf](/assets/pdf/48x29mm-digital-voltmeter.pdf) |
| T-type soldering tip (flex cable) | [Comprar](https://s.click.aliexpress.com/e/_c3bMZUIN?SearchText=Soldering%20Iron%20T%20Tip%20T-head%20Copper%20T-Tips%20%2B%20Rubber) | [t-type-soldering-tip-60w.pdf](/assets/pdf/t-type-soldering-tip-60w.pdf) |
| Translucent acrylic sheet 1 mm | [Comprar](https://s.click.aliexpress.com/e/_c3fLPpqv?SearchText=Translucent%20%20Acrylic%20Plexiglass%201mm) | [translucent-acrylic-plexiglass-1mm.pdf](/assets/pdf/translucent-acrylic-plexiglass-1mm.pdf) |

## Notas prácticas:
Al final, lo que buscábamos era sencillo: soldar la pantalla una vez y poder mover el módulo de un prototipo a otro sin volver al crimper ni al soldador. Atornillas, desatornillas, y listo. Si cambias mucho el cableado en la mesa de trabajo o en una caja de instrumentación, ese gesto vale la pena.

Lo que más tiempo lleva no es la electrónica, sino la carcasa. Encontrar una carcasa vacía de 48×29 mm en cantidades de hobby es casi misión imposible. Lo habitual es comprar el medidor más barato que encuentres y vaciarlo. Para la ventana delantera se probó de todo: la lámina roja del voltímetro original apaga demasiado la OLED; verdes y azules tampoco ayudaron. Nos quedamos con la lámina gris translúcida del multímetro donante (o un acrílico oscuro de hasta 1 mm si la cortas tú).

Un detalle que tranquiliza: el agujero del panel no tiene que quedar impecable. El bisel tapa cantos irregulares y las pestañas internas sujetan el módulo sin tornillos extra. En la fila inferior de terminales los Dupont entran justos (no es la fila más cómoda), pero una vez dentro aguantan si tiras del cable.
