# Investigación

El desarrollo de RF utilizará el transceptor de RF SI4463 ó SI4464, ambos tienen la capacidad de transmitir y recibir en 144.930 MHz para usarlos como transmisores de APRS y receptores de comandos en formato **PACKET**. Esta elección se basa en el diseño de los módulos lightaprs que lo usan, por lo que ya tiene herencia de vuelo.

Cada micro tiene distintas topologías de diseño de los componentes pasivos que completan el circuito de transmisión y recepción. 

Las topologías se encuentran en el documento: ***AN629*** (ver carpeta adjunta).

En la nota de aplicación: ***AN648*** se explica en mayor detalle el diseño de TX.

Por otro lado, cada topología presentada tiene un diseño de referencia de PCB que se encuentra en la página:  [Technical Resource Search - Silicon Labs](https://www.silabs.com/support/resources.ct-schematic-and-layout-files.p-wireless_proprietary_ezradiopro-sub-ghz-wireless-ics_si4463.p-wireless_proprietary_ezradiopro-sub-ghz-wireless-ics_si4464)

Por como funciona internamente el CHIP, la topología del circuito depende de la frecuencia central a transmitir y/o recibir. En caso de que las frecuencias de TX y RX sean muy distintas, se deberá usar un **switch** que selecione el circuito resonante correspondiente para TX o RX. O, en su defecto, usar antenas distintas.

Hay una relación inversamente proporcional en cuanto a la facilidad de cálculo del circuito y su selecctividad de componentes. Por ejemplo, hay circuitos de TRX que no requieren el switch pero las redes resonantes de TX y RX terminan acopladas entre si, lo que provoca que la disperción de componentes en una red afecte el rendimiento de la otra. 

Por otro lado, las redes separadas tienen más tolerancia de componentes pero requieren más elementos pasivos y hasta un elemento activo (el switch) que incrementan el costo y espacio requerido en la placa. 

## Selección de topología

En la nota de aplicación AN648 TABLA 1, se mencionan los distintos circuitos, y sus bandas de frecuencias aplicables. En el caso nuestro, elegimos el circuito de la fila 4: **SQW DT: 169M 20 dBm 70mA**  para ver el diseño y cálculos se referencian ambas notas de aplicación: ***AN648 y AN629***

Ya que nosotros queremos recibir y transmitir, con una sóla antena y reduciendo la cantidad de componentes, seleccionamos la topología de la ***AN629*** denominada: 

**Square-Wave Direct Tie Type Matching Network Layout Based on the
4463-PSQ20D169 (4463CPSQ20D169) Pico Board (Single Antenna without RF
Switch)**

Su diseño de referencia se encuentra descargado en el repo. Para abrirlo es necesario importarlo en Altium. También está convertido a un diseño maquetado en Kicad. 



# Problemática

Tenemos el problema de que luego de realizar un cálculo de BOM, sólo de comunicaciones, tenemos un costo de materiales de 25 USD. Si consideramos el resto de componentes y costo de manufactura el precio total de venta terminará rondando entre los 100 y 130 USD, muy similar a la solución propuesta por lightaprs. 

El plan de acción debería ser: 

1. Realizar un análisis de mercado para interpretar qué tanto estarían dispuestos a gastar los posibles interesados en nuestra propuesta vs qué tanto están dispuestos a gastar en un lanzamiento completo. Que incluya helio, globos o piniatas, etc. 

2. Ver si sería posible usar soluciones ya existentes de mercado como módulos transceptores:
   
   1. [RFM26W - HOPERF - Reliable original manufacturer of IoT key components](https://www.hoperf.com/modules/rf_transceiver/RFM26W.html)
   
   2. https://es.aliexpress.com/item/1005004147829291.html?spm=a2g0o.productlist.main.23.6bf04f5cAJ2ldw&algo_pvid=86daa3b1-d12e-4d14-922c-cec85e176e00&algo_exp_id=86daa3b1-d12e-4d14-922c-cec85e176e00-11&pdp_npi=4%40dis%21ARS%212001.17%212001.17%21%21%215.50%21%21%402101eab017022213155401827e2d3f%2112000028192810473%21sea%21AR%210%21AB&curPageLogUid=xC1TEUfY4IjR
   
   3. CC1120 con disenio propio
   
   4. [LR62XE, the +30 dBm SX1262 LoRa Module &mdash; Fanstel](https://www.fanstel.com/lr62xe)

3. La solución por la que decantemos deberá ser TX y RX.

4. Ver si realmente los interesados quieren poder enviarle comandos al cansat.

> Antes de seguir con este desarrollo, deberíamos ponernos en contacto con colegios que hayan participado del concurso CANSAT para preguntar si les interesa la propuesta. 
> 
> Podríamos hacer un encuesta por mail que permita responder dudas mencionadas anteriormente.




