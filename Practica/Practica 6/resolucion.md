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

## 5. ¿Qué restricción existe sobre el tamaño de ventanas en el protocolo Selective Repeat?

## 6. De acuerdo a la captura TCP de la siguiente figura, indique los valores de los campos borroneados.

## 7. Dada la sesión TCP de la figura, completar los valores marcados con un signo de interrogación.


## 8. ¿Qué es el RTT y cómo se calcula? Investigue la opción TCP timestamp y los campos TSval y TSecr.