# Capa de Transporte - Parte II

## 1. ¿Cual es el puerto por defecto que se utiliza en los siguientes servicios?

Web / SSH / DNS / Web Seguro / POP3 / IMAP / SMTP

- Web -> 80
- SSH -> 22
- DNS -> 43
- Web Seguro -> 443
- POP3 -> 110
- IMAP -> 143
- SMTP -> 25

Investigue en qué lugar en Linux y en Windows está descripta la asociación utilizada por defecto para cada servicio.

- Linux -> /etc/services
- Windows -> HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services


## 2. Investigue qué es multicast. ¿Sobre cuál de los protocolos de capa de transporte funciona? ¿Se podría adaptar para que funcione sobre el otro protocolo de capa de transporte? ¿Por qué?

- Multicast es un tipo de envío, en el cuál desde un emisor se envía un mensaje a múltiples receptores.
- Multicast puede funcionar junto con UDP pero no con TCP, ya que este es end-to-end (de host a host), se establece una conexión entre ellos.

## 3. Investigue cómo funciona el protocolo de aplicación FTP teniendo en cuenta las diferencias en su funcionamiento cuando se utiliza el modo activo de cuando se utiliza el modo pasivo ¿En qué se diferencian estos tipos de comunicaciones del resto de los protocolos de aplicación vistos?

- FTP es un protocolo de la capa de aplicación que permite el intercambio de información (cliente-servidor). Lo que lo distingue de los otros protocolos es que este utiliza dos conexiones, una para control (puerto 21) y otra para datos. FTP tiene dos modos, FTP activo y FTP pasivo.
  - En el modo activo, el servidor inicia la conexión de datos con el cliente al puerto 20.
  - En el modo pasivo, el cliente le dice al servidor a cuál de sus puertos debe conectarse para la conexión de datos.

## 4. Suponiendo Selective Repeat; tamaño de ventana 4 y sabiendo que E indica que el mensaje llegó con errores. Indique en el siguiente gráfico, la numeración de los ACK que el host B envía al Host A.

![](img/clipboard01.png)

- ACK = 0
- ACK = 1
- ACK = 3
- ACK = 4
- ACK = 5
- ACK = 2

## 5. ¿Qué restricción existe sobre el tamaño de ventanas en el protocolo Selective Repeat?

- El tamaño de la ventana debe ser menos que (M-1)/2
  - Siendo M la enumeración de los segmentos de una ráfaga.

## 6. De acuerdo a la captura TCP de la siguiente figura, indique los valores de los campos borroneados.

![](img/clipboard02.png)

1. 172.20.1.1 - 172.20.1.100 [__SYN__] Seq=__3933822138__, ...
2. 172.20.1.100 - 172.20.1.1 [__SYN, ACK__] Seq=1047471501, Ack=3933822138
3. __172.20.1.1__ - __172.10.1.100__ [__ACK__] Seq=__3933822138__, Ack=__1047471501__

## 7. Dada la sesión TCP de la figura, completar los valores marcados con un signo de interrogación.

![](img/clipboard3.png)

- Seq=1, Ack=1
- Seq=1, Ack=8
- Seq=1, Ack=17
- Seq=1, Ack=22
- Seq=22, Ack=1
- Ack=1, Seq=23
- Seq=23, Ack=2 

## 8. ¿Qué es el RTT y cómo se calcula? Investigue la opción TCP timestamp y los campos TSval y TSecr.

- El RTT (Round-Trip Time) es el tiempo de un segmento en ir y volver. Se calcula restando el tiempo de recepción al emisor y el tiempo en el que se envió.
- La opción TCP timestamp es un mecanismo que nos permite medir y sincronizar el tiempo entre los extremos. Es un campo del header TCP que tiene una marca de tiempo escrita por el emisor, después también la escribe el receptor y en función de eso se puede obtener el RTT
  - __TSVal (TimeStamp Value):__ Valor de la marca de tiempo generada por el emisor.
  - __TSecr (TimeStamp Echo Reply):__ Valor de la marca de tiempo que recibe el emisor. Es retornada al emisor. 