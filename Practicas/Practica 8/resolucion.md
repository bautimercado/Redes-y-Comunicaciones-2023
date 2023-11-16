# Práctica 8 - Capa de Red - Ruteo

# Recomendación

## 1. Al final de la práctica se encuentra un ejercicio para ser realizado en la herramienta CORE. Si bien el ejercicio no agrega conceptos nuevos a los vistos previamente recomendamos su resolución para que puedan configurar, probar y analizar todo lo aprendido en una simulación de una red

# Fragmentación

## 2. Se tiene la siguiente red con los MTUs indicados en la misma. Si desde pc1 se envía un paquete IP a pc2 con un tamaño total de 1500 bytes (cabecera IP más payload) con el campo Identification = 20543, responder:

![gráfico-ejercicio-2](img/Clipboard01.png)

- Indicar IPs origen y destino y campos correspondientes a la fragmentación cuando el paquete sale de pc1

  - IP Origen: 10.0.0.20/24
  - IP Destino: 10.0.2.20/24
  - Header: 20
  - Length: 1500
  - Identificación: 20543
  - DF Flag: 0
  - MF Flag: 0
  - Fragment offset: 0
  
- ¿Qué sucede cuando el paquete debe ser reenviado por el router R1?

  - El enlace entre el router R1 y R2 tiene un MTU de 600, por lo tanto, el paquete se fragmentará.

- Indicar cómo quedarían las paquetes fragmentados para ser enviados por el enlace entre R1 y R2.

  - Para fragmentar debemos tomar el MTU y restarle el valor del header (20B)
    - 600B - 20B = 580B
  - Después debemos encontrar el múltiplo de 8 más cercano a ese número y sumarle el header (que sería el tamaño total).
    - En este caso hay dos múltiplos cercanos, 584 y 576, pero usamos 576 ya que si le sumamos el header no se pasa de los 600B, por lo tanto, el Length sería de 596B
    - Entonces, en este caso vamos a tener dos fragmentos de 596B. Para el último fragmento vamos a tener 348 pero a ese último fragmento no se le suma 20 del header (por qué?).
    - El tamaño del payload debe ser múltiplo de 8.
  - Para el caso del offset, lo que tenemos que hacer es agarrar el Length obtenido, restarle el header (20) y dividirlo por 3, eso nos da 72.
  - El primer fragmento tendría offset 0
  - El último segmento tendría MF Flag en 0
  - La suma de los length de los fragmentos es igual al length del paquete original (1500B) + 20 * (#fragmentos - 1)

| Fragmento 1 | Fragmento 2 | Fragmento 3 |
|-------------|-------------|-------------|
| Header: 20  |  Header: 20 |  Header: 20 |
| Length: 596 | Length: 596 | Length: 348 |
|  ID: 20543  |  ID: 20543  |  ID: 20543  |
|  DF Flag: 0 |  DF Flag: 0 |  DF Flag: 0 |
|  MF Flag: 1 |  MF Flag: 1 |  MF Flag: 0 |
| Frag. offset: 0 | Frag. offset: 72 | Frag. offset: 144 |   

- ¿Dónde se unen nuevamente los fragmentos? ¿Qué sucede si un fragmento no llega?

  - Los fragmentos se vuelven a unir en los sistemas terminales. Si un fragmento se pierde, se tienen que retransmitir todos los fragmentos del paquete original.
  - Esto depende de los protocolos de las capas superiores, recordar que IP es Best-Effort. 

- Si un fragmento tiene que ser reenviado por un enlace con un MTU menor al tamaño del fragmento, ¿qué hará el router con ese fragmento?

  - En este caso, se vuelve a fragmentar en función del nuevo MTU.

# Ruteo

## 3. ¿Qué es el ruteo? ¿Por qué es necesario?

- El ruteo es la acción de seleccionar la interfaz de salida y el próximo salto a partir de la tabla de ruteo de un dispositivo (router o host).
- Es necesario para que el paquete viaje desde un origen hasta un destino.

## 4. En las redes IP el ruteo puede configurarse en forma estática o en forma dinámica. Indique ventajas y desventajas de cada método.

| Forma | Ventajas | Desventajas |
| ----- | -------- | ----------- |
| Estática | Fácil de configurar en redes pequeñas. Se tiene un control total sobre las rutas. Genera menos tráfico. | No se adapta a cambios. No es escalable. Menos eficiente en cuanto a tiempo en redes grandes. |
| Dinámica | Es más adaptable a cambios. Es más escalable y usa más eficientemente los recursos. | Es muy compleja y difícil de mantener. El tráfico de red tiende a ser mayor, lo cuál además genera inestabilidad si no se la configura correctamente. |

## 5. Una máquina conectada a una red pero no a Internet, ¿tiene tabla de ruteo?

- Si, esa tabla de ruteo sirve para que la máquina pueda comunicarse en dicha red.

## 6. Observando el siguiente gráfico y la tabla de ruteo del router D, responder:

![gráfico-ejercicio-6](img/Clipboard02.png)

### a. ¿Está correcta esa tabla de ruteo? En caso de no estarlo, indicar el o los errores encontrados. Escribir la tabla correctamente (no es necesario agregar las redes que conectan contra los ISPs)

- La entrada a la red 205.10.280.0 está mal escrita, en realidad la red (A) es 205.10.0.280 y el next hop sería 10.0.0.1 no 10.0.0.2 (que esa es una IP del router).
- Falta la red 10.0.0.8 (las redes directamente conectadas SIEMPRE tienen que estar).
- La red 205.20.0.193 no existe.
- La entrada a la red 10.0.0.12, el next hop no debe tener prefijo.
- La conexión con la red B en realidad sería con la IP 205.20.0.192, por el Rtr-B sería un camino más óptimo (no es un error lo último).

escribir tabla.

- Si el enunciado no aclara, el router debe alcanzar todas las redes (+ el Default Gateway)

### b. Con la tabla de ruteo del punto anterior, Red D, ¿tiene salida a Internet? ¿Por qué? ¿Cómo lo solucionaría? Suponga que los demás routers están correctamente configurados, con salida a Internet y que Rtr-D debe salir a Internet por Rtr-C.

- No, con la configuración dada la Red D no tiene sálida a Internet ya que el router no tiene ninguna configuración hacía algunos de los routers ISP.
- Una forma de solucionarlo es agregar un default gateway que mande el tráfico que va hacía internet a través del router C por ejemplo (suponiendo que Rtr-C también tendrá un Default Gateway a su ISP).

| Red Destino | Mask | Next-Hop | Interface |
| ----------- | ---- | -------- | --------- |
|   0.0.0.0   |  /0  | 10.0.0.10 |   eth3   |

### c. Teniendo en cuenta lo aplicado en el punto anterior, si en Rtr-C estuviese la siguiente entrada en su tabla de ruteo qué sucedería si desde una PC en Red D se quiere acceder un servidor con IP 163.10.5.15.

| Red Destino | Mask | Next-Hop | Interface |
|-------------|------|----------|-----------|
| 163.10.5.0  | /24  | 10.0.0.9 |   eth1    |

- El Rtr-D recibe el paquete y lo reenvía por el Default Gateway, ya que la IP 163.10.5.15 no coincide con ninguna otra entrada al aplicarle el AND lógico con las máscaras.
- El Rtr-C recibe el paquete, ve que la IP destino es 163.10.5.15 y calcula la entrada correspondiente aplicando el AND lógico con las máscaras.
- En este caso, el router vuelve a mandar el paquete al Rtr-D y se produce un bucle hasta que el TTL expire.
- Siempre se rutea en función de la IP destino. Se va aplicando el AND lógico con las máscaras más especificas a las menos específicas.

### d. ¿Es posible aplicar sumarización en esa tabla, la del router Rtr-D? ¿Por qué? ¿Qué debería suceder para poder aplicarla?

- No es posible (con la tabla por defecto), si bien algunas de las redes son continuas, no podemos sumarizar porque además de ser continuas deben tener el mismo Next-Hop y la misma Interface, sino perdemos información.

### e. La sumarización aplicada en el punto anterior, ¿se podría aplicar en Rtr-B? ¿Por qué?

- Se podría aplicar siempre y cuando tenga redes que son continuas y que compartan Next-Hop y Interface.

### f. Escriba la tabla de ruteo de Rtr-B teniendo en cuenta lo siguiente:

- Debe llegarse a todas las redes del gráfico
- Debe salir a Internet por Rtr-A
- Debe pasar por Rtr-D para llegar a Red D
- Sumarizar si es posible

| Red Destino | Mask | Next-Hop | Iface |
| ----------- | ---- | -------- | ----- |
| 205.20.0.192 | /26 |  0.0.0.0 | eth0  |
| 205.20.0.128 | /26 |  0.0.0.0 | eth2  |
|   10.0.0.4   | /30 |  0.0.0.0 | eth1  |
|   10.0.0.12  | /30 |  0.0.0.0 | eth3  |
| 153.10.20.128 | /27 | 10.0.0.6 | eth1 |
| 163.10.5.64  | /27 | 10.0.0.6 | eth1 |
| 205.10.0.128 | /25 | 10.0.0.13 | eth3 |
| 10.0.0.0 | /30 | 10.0.0.6 | eth1 |
| 10.0.0.8 | /30 | 10.0.0.6 | eth1 |
| 10.0.0.16 | /30 | 10.0.0.13 | eth3 |
| 120.0.0.0 | /30 | 10.0.0.13 | eth3 |
| 130.0.10.0 | /30 | 10.0.0.6 | eth1 |
| 0.0.0.0 | /0 | 10.0.0.13 | eth3 |

- Sumarizando me queda:

| Red Destino | Mask | Next-Hop | Iface |
| ----------- | ---- | -------- | ----- |
| 205.20.0.192 | /26 |  0.0.0.0 | eth0  |
| 205.20.0.128 | /26 |  0.0.0.0 | eth2  |
|   10.0.0.4   | /30 |  0.0.0.0 | eth1  |
|   10.0.0.12  | /30 |  0.0.0.0 | eth3  |
| 153.10.20.128 | /27 | 10.0.0.6 | eth1 |
| 163.10.5.64  | /27 | 10.0.0.6 | eth1 |
| 205.10.0.128 | /25 | 10.0.0.13 | eth3 |
| 10.0.0.0 | /28 | 10.0.0.6 | eth1 |
| 10.0.0.16 | /30 | 10.0.0.13 | eth3 |
| 120.0.0.0 | /30 | 10.0.0.13 | eth3 |
| 130.0.10.0 | /30 | 10.0.0.6 | eth1 |
| 0.0.0.0 | /0 | 10.0.0.13 | eth3 |

### g. Si Rtr-C pierde conectividad contra ISP-2, ¿es posible restablecer el acceso a Internet sin esperar a que vuelva la conectividad entre esos dispositivos?

- Es posible pero tenemos que configurar las tablas de ruteo. Podríamos hacer que Rtr-C redirija el tráfico que iba a ISP-2 hacia ISP-1 pasando por el Rtr-A (10.0.0.17). 

## 7. Evalúe para cada caso si el mensaje llegará a destino, saltos que tomará y tipo de respuesta recibida el emisor

![gráfico-ejercicio-7](img/Clipboard03.png)

### Un mensaje ICMP enviado por PC-B a PC-C.

- PC-B -> 10.0.5.20
- PC-C -> 10.0.7.20
- PC-B le envía el paquete al router2.
- El router2 no tiene configurada la red de PC-C (10.0.7.0) pero tiene un Default Gateway que dirige el tráfico hacía el router1. Entonces el router2 le envía el paquete al router1.
- El router1 parece que no tiene configurada la red 10.0.7.0 pero en realidad si la tiene, ya que su tabla tiene la entrada 10.0.0.0 cuya máscara es /16 y abarca a la red 10.0.7.0, además si aplicamos esa máscara al destino 10.0.7.20, nos da 10.0.0.0 (red destino), entonces el router1 le envía el paquete al router3 (10.0.3.1).
- El router3 tiene la red 10.0.7.0, entonces la envía a dicha red para que PC-C obtenga el paquete.
- Entonces el mensaje llega a su destino, la respuesta recibida por PC-B sería ICMP Echo Reply.
- Los saltos fueron:
  - PC-B - 10.0.5.20/24
  - Router2 - 10.0.5.1/24
  - Router1 - 10.0.0.1/24
  - Router3 - 10.0.3.1/24
  - PC-C - 10.0.7.20

### Un mensaje ICMP enviado por PC-C a PC-B.

- PC-C -> 10.0.7.20/24
- PC-B -> 10.0.5.20/24
- PC-C le envía el paquete al router3
- El router3 no conoce a 10.0.5.20, entonces envía el paquete a su Default Gateway que sería al router4 (10.0.2.1)
- El router4 tiene la entrada 10.0.0.0 con máscara /8, si le aplicamos esa máscara a la IP destino obtenemos 10.0.0.0, por lo tanto usamos esa entrada para rutear el paquete y lo recibe el router2 (10.0.1.1)
- El router2 conoce la red 10.0.5.0 ya que es una red directamente conectada, entonces lo envía por la interface eth2 para que PC-B lo reciba.
- La respuesta es un ICMP Echo Reply.
- Los saltos fueron:
  - PC-C - 10.0.7.20/24
  - Router3 - 10.0.7.1/24
  - Router4 - 10.0.2.1/24
  - Router2 - 10.0.1.1/24
  - PC-B - 10.0.5.20/24

### Un mensaje ICMP enviado por PC-C a 8.8.8.8.

- El router3 recibe el paquete de PC-C y no conoce 8.8.8.8, por lo tanto se lo envía al router4 por su Default Gateway.
- El router4 no conoce la red 8.8.8.8 y como no tiene Default Gateway, el paquete se queda ahí.
- La respuesta es un ICMP Network Unreacheable.

### Un mensaje ICMP enviado por PC-B a 8.8.8.8.

- El router2 recibe el paquete de PC-B, no conoce a 8.8.8.8, por lo tanto envía el paquete a su Default Gateway que es Router1.
- El router1 recibe el paquete, tampoco conoce a 8.8.8.8, entonces envía el paquete a su Default Gateway que es el router2 de nuevo.
- Esto causa un loop, por lo tanto PC-B recibiría un ICMP TTL Expired o un ICMP Network Unreachable.

# DHCP y NAT

## 8. Con la máquina virtual con acceso a Internet realice las siguientes observaciones respecto de la auto-configuración IP vía DHCP:

### a. Inicie una captura de tráfico Wireshark utilizando el filtro bootp para visualizar únicamente tráfico de DHCP.

### b. En una terminal de root, ejecute el comando sudo /sbin/dhclient eth0 y analice el intercambio de paquetes capturado.

### c. Analice la información registrada en el archivo /var/lib/dhcp/dhclient.leases, ¿cuál parece su función?

### d. Ejecute el siguiente comando para eliminar información temporal asignada por el servidor DHCP. rm /var/lib/dhcp/dhclient.leases

### e. En una terminal de root, vuelva a ejecutar el comando sudo /sbin/dhclient eth0 y analice el intercambio de paquetes capturado nuevamente ¿a que se debió la diferencia con lo observado en el punto “b”?

### f. Tanto en “b” como en “e”, ¿qué información es brindada al host que realiza la petición DHCP, además de la dirección IP que tiene que utilizar?

## 9. ¿Qué es NAT y para qué sirve? De un ejemplo de su uso y analice cómo funcionaría en ese entorno. Ayuda: analizar el servicio de Internet hogareño en el cual varios dispositivos usan Internet simultáneamente.

## 10. ¿Qué especifica la RFC 1918 y cómo se relaciona con NAT?

## 11. En la red de su casa o trabajo verifique la dirección IP de su computadora y luego acceda a www.cualesmiip.com. ¿Qué observa? ¿Puede explicar qué sucede?

## 12. Resuelva las consignas que se dan a continuación.

### a. En base a la siguiente topología y a las tablas que se muestran, complete los datos que faltan.

![gráfico-ejercicio-12](img/Clipboard04.png)

PC-A (ss)

|Local Address:Port|Peer Address:Port|
|------------------|-----------------|
|192.168.1.2:49273 |...|
|... |190.50.10.63:25|
|192.168.1.2:...| 190.50.10.81:8080 |

PC-B (ss)

|Local Address:Port|Peer Address:Port|
|------------------|-----------------|
|192.168.1.3:52734|...|
|192.168.1.3:39275|...|

RTR-1 (Tabla de NAT)

|Lado LAN |Lado WAN|
|---------|--------|
|192.168.1.2:49273 |205.20.0.29:25192|
|192.168.1.2:51238 |...|
|192.168.1.3:52734 |205.20.0.29:51091|
|192.168.1.2:37484 |205.20.0.29:41823|
|192.168.1.3:39275 |205.20.0.29:9123|

SRV-A (ss)

|Local Address:Port |Peer Address:Port|
|-------------------|----------------|
|190.50.10.63:80 |205.20.0.29:25192|
|190.50.10.63:25 |205.20.0.29:41823|

SRV-B (ss)

|Local Address:Port |Peer Address:Port|
|------------------|------------------|
|190.50.10.81:8080 |205.20.0.29:16345|
|190.50.10.81:8081 |205.20.0.29:51091|
|190.50.10.81:8080 |205.20.0.29:9123|

### b. En base a lo anterior, responda:

#### i. ¿Cuántas conexiones establecidas hay y entre qué dispositivos?

#### ii. ¿Quién inició cada una de las conexiones? ¿Podrían haberse iniciado en sentido inverso? ¿Por qué? Investigue qué es port forwarding y si serviría como solución en este caso.