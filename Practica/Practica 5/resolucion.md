## 1. ¿Cuál es la función de la capa de transporte?

- La función de la Capa de Transporte es transportar los datos de una aplicación de un host a otro host, pasandole los datos a la capa inferior.
## 2. Describa la estructura del segmento TCP y UDP.

- El datagrama UDP es muy sencillo. Posee el número de puerto origen y número de puerto destino, el tamaño del datagrama, el checksum y el payload.
- El segmento TCP ya es más complejo (al ofrecer más funcionalidades), tiene casi los mismos campos que el detagrama UDP, cuenta con flags para el estado de la conexión, tiene un apartado de opciones, campos para saber el número de bit que se envía del stream TCP, número de ACK, campos de opciones, tamaño de ventana de recepción, etc.
## 3. ¿Cuál es el objetivo del uso de puertos en el modelo TCP/IP?

- En particular, un mismo host (que tiene una dirección IP), puede estar manteniendo más de una aplicación con la cuál se puede comunicar con otros (por ejemplo, un servidor puede ser un servidor HTTP y un servidor de correo a la vez). El uso de los puertos permite distinguir con qué aplicación de un host nos estamos comunicando.
## 4. Compare TCP y UDP en cuanto a:

### a. Confiabilidad.

- UDP es un protocolo no confiable best-effort. Esto significa que UDP no asegura de que el paquete llegue a su destino. Lo único que posee es el checksum para control de errores.
- TCP es un protocolo confiable. Asegura que el paquete llegue a destino, además ofrece control de errores, control de flujo y control de congestión.

### b. Multiplexación.

- Tanto TCP como UDP permiten multiplexación, pero cada uno lo hace a su manera:
  - En el datagrama UDP viene incluido la dirección ip y el puerto del emisor, y la dirección ip y el puerto del destino. Se puede lograr la multiplexación cambiando de lugar estos valores (es decir, si el receptor desea contestar el mensaje, podría decir que ahora los valores de emisor son los suyos y los valores de receptor son del que envió el mensaje).
  - En TCP se establece una conexión entre los dos extremos. Esto me permite que ambos extremos puedan enviarse mensajes mutuamente.

### c. Orientado a la conexión.

- UDP no es orientado a conexión, simplemente se envía el paquete al host destino.
- TCP si es orientado a conexión, antes de enviar los datos, se establece la conexión entre ambos extremos donde se negocian ciertos parámetros.

### d. Controles de congestión.

- UDP no ofrece controles de congestión, es decir, no se fija en cuál es el estado de la red.
- TCP si cuenta con controles de congestión.

### e. Utilización de puertos.

//CONSULTAR
- Tanto UDP como TCP hacen uso de los puertos. La diferncia está en que TCP no necesita tener que invertir los valores de puertos para hacer MUX/DEMUX.

## 5. La PDU de la capa de transporte es el segmento. Sin embargo, en algunos contextos suele utilizarse el término datagrama. Indique cuando.

//CONSULTAR
- La PDU de la Capa de Red es el _datagrama_, ese término es utilizado en Capa de Transporte para referirse a la PDU de UDP. Es llamado así, ya que la información que agrega a la PDU de transporte es poca.