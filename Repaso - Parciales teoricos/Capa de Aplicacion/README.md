# Introducción

![A-Introducción-01](img/A-Introduccion-01)

- Una RFC es un documento en el que se detalla la información de cierto protocolo del modelo TCP/IP. Su utilidad recae en que son estándares realizados por las personas donde se detallan (por ejemplo) las restricciones, usos y diferentes servicios que ofrece el protocolo documentado.

![A-Introducción-02](img/A-Introduccion-02)

- Capa de Aplicación.
- Capa de Transporte.
- Capa de Internet (de Red).
- Capa Física.

![A-Introducción-03](img/A-Introduccion-03)

- Las redes pueden interconectarse entre sí, formando redes de redes.
- Es un grupo de dispositivos interconectados.

![A-Introducción-04](img/A-Introduccion-04)

- Navegador/Browser Web
- SMTP
- Protocolo bittorrent
- WhatsApp

![A-Introducción-05](img/A-Introduccion-05)

- Modelo abierto
- Funcionalidad de transporte provista por TCP y/o UDP
- Funcionalidad de red provista por IP

![A-Introducción-06](img/A-Introduccion-06)

- Modelo en capas o pila de capas.

![A-Introducción-07](img/A-Introduccion-07)

- FTP
- HTTP
- DNS

![A-Introducción-08](img/A-Introduccion-08)

- Protocolo


# HTTP

![](img/B-HTTP-01)

- El método GET me permite obtener recursos que se le solicitan al servidor. El método PUT sirve para subir recursos al servidor.

![](img/B-HTTP-02)

- Pipelining
- Conexiones persistentes
- Compresión de headers

![](img/B-HTTP-03)

- Falso

![](img/B-HTTP-04)

- Verdadero

![](img/B-HTTP-05)

- Verdadero

![](img/B-HTTP-06)

- Verdadero

# DNS

![](img/C-DNS-01)

- gTLDs -> Contienen dominios con propósitos particulares, de acuerdo a diferentes actividades.
- .ARPA TLD -> Dominio especial usado internamente para resolución de reversos.
- ccTLD -> Contienen dominios delefados a los diferentes paises del mundo.

![](img/C-DNS-02)

- Los servidores autoritativos no pueden ser servidores locales o resolvers.
- Una consulta se podría llegar a obtener resupeusta de diferentes servidores, por ejemplo si toma más tiempo de lo previsto.
- DNS es un sistema distribuido y jerárquico.
- La mayoría de los servidores DNS de la raíz funciona con anycast para dar un mejor servicio.
- Los servidores de DNS autoritativos mayormente atienden consultas iterativas.

![](img/C-DNS-03)

[Link video](https://www.youtube.com/watch?v=Ih9Jalbw4yM&list=PLWRFVCdbvpAnKn9Cuw4XtAvxScF5HGZOA&index=7&ab_channel=AndresBarbieri)

- www.unlp.edu.ar es un alias de cms-nodes.desarrollo.unlp.edu.ar
- 163.10.255.167 es una de las IPs asociadas al nombre de host por el cual se está consultando.
- Los flags indican que la consulta es hecha y respondida en forma recursiva.

![](img/C-DNS-04)

- Procedimiento de búsqueda y resolución
- Espacio de nombres
- Base de datos distribuida y servidores

![](img/C-DNS-05)

- Mapear nombres de hosts/dominio a direcciones IP.

![](img/C-DNS-06)

- Falso

# FTP

![](img/D-FTP-01)

- Usa 2 conexiones, una para control y otra apra datos.
- Es soportado por los navegadores usando la URI ftp://

![](img/D-FTP-02)

- FTPS
- SCP
- NFS
- TFTP

![](img/D-FTP-03)

- En FTP activo el servidor es quién inicia la conexión de datos desde el puerto 20.
- FTP activo usa el puerto 21 para control y el 20 para datos.

![](img/D-FTP-04)

- xd

![](img/D-FTP-05)

- Verdadero

![](img/D-FTP-06)

- Falso


# Correo

![](img/E-Correo-01)

- SMTP -> 25
- POP -> 110
- IMAP -> 143

![](img/E-Correo-02)

- Para enviar un mail el cliente de correo usa el protocolo SMTP.
- Los MTAs se comunican entre sí usando el protocolo SMTP.
- Un cliente de correo electŕonico puede recuperar los mensajes del buzón de un usuario usando POP o IMAP.

![](img/E-Correo-03)

- HELLO
- QUIT

![](img/E-Correo-04)

- Se trata de un mensaje de tipo MIME.
- En el mensaje se transfiere una imagen codificada en base64.
- text/plain es el tipo de contenido de la primer parte del mensaje.

![](img/E-Correo-05)

- Verdadero