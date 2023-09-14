# Practica 4 - Correo electrónico
## Correo electrónico
### 1. ¿Qué protocolos se utilizan para el envío de mails entre el cliente y su servidor de correo? ¿Y entre servidores de correo?
- El protocolo que se usa para el envío de mail tanto entre cliente-servidores y los servidores, es SMTP.
### 2. ¿Qué protocolos se utilizan para la recepción de mails? Enumere y explique características y diferencias entre las alternativas posibles?
- Los protocolos que se usan para la recepción de mail son POP3 y IMAP.
  - POP3 es un protocolo más sencillo, el usuario cuando quiere acceder a sus mails, los descarga y se borran del servidor. Con esto, no podría volver a ver los mails desde otro dispositivo.
  - IMAP es un protocolo más complejo, el servidor permite que el usuario lea, borre y organice los mails como si fuera un systemfile.

### 8. Indique sí es posible que el MSA escuche en un puerto TCP diferente a los convencionales y qué implicancias tendría.
- Si es posible, en ese caso habría que avisarle al resto de los MUA del dominio.
### 9. Indique sí es posible que el MTA escuche en un puerto TCP diferente a los convencionales y qué implicancias tendría.
- En ese caso, no es posible. Ya que debería avisarle a los MSA del cambio y a los otros MTA (muy costoso).

### 10.
#### a.
- Debería registrar los nameservers y las direcciones IP (NS y A) de los servidores DNS de redes2022.com.ar en el dominio "padre" (com.ar).
#### b.
- A
- A
- A
- A
- SOA
- MX
- web-mail no es un servidor de correo por lo tanto no necesita un MX.
#### c.
- No sería necesario, porque es autoritario para el dominio redes2022.com.ar, por tanto no necesitaría resolver la petición consultando a otros servidores.