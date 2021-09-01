---
description: Gestión de los servicios de correo y de cola de impresión.
---

# 10- CORREO Y COLA DE IMPRESIÓN

## **CORREO ELECTRÓNICO**

### **INFORMACION GENERAL CORREO ELECTRONICO**

Cuando enviamos un correo, este se envia al **MTA** \(mail transport agent\) que tiene la mision de enviarlo hacia el **MTA** del destinatario. Se comunican entre si utilizando **protocolo SMTP**.  
Despues, el **MTA** entrega el correo al **MDA** \(mail delivery agent\) que almacena ese correo electronico mientras espera que el usuario lo acepte. Aquí es donde se diferencian dos protocolos de correo:

* **POP3** --&gt; Se usa para recuperar los correos y a veces dejar una copia en el servidor.
* **IMAP** --&gt; Permite gestionar el estado de los correos \(leido, eliminado, movido\). Se guarda en el servidor. 

### **FICHEROS DE UTILIDAD**

**/var/spool/mail** --&gt; directorio con las colas de mail de los usuarios.

**/etc/aliases** --&gt; fichero en el que aparecen las direcciones por defecto de los actores de una red.

**/etc/mail/alias** --&gt; archivo de configuracion de sendmail

### **COMANDOS**

**MAIL** --&gt; mandar correos electronicos desde el sistema  
 `-s` --&gt; Asunto

**MAILQ** --&gt; query de mail

## COLA DE IMPRESIÓN

### **INFORMACION GENERAL IMPRESION**

`apt-get install cups` --&gt; paquete de drivers relacionados con la impresion y las impresoras.

### **FICHEROS DE UTILIDAD**

**/etc/cups/cupsd.conf** --&gt; archivo de configuracion del cups.

**/etc/cups/ppd** --&gt; directorio donde se instalan los drivers de las impresoras.

**/etc/cups/cups-browsed.conf** --&gt; archivo de configuracion de las politicas de impresion

**/etc/cups/printers.conf** --&gt; archivo de confriguracion de impresoras. No se crea por defecto \(parece\)

### **COMANDOS**

**LPR** --&gt; para mandar un fichero a la cola de impresion. P.E: `lpr 111.txt`

**LPRM** --&gt; elimina un fichero de la cola de impresión. `lprm 1 #por numero de trabajo o job`

**LPQ** --&gt; query de la cola de impresion. De aquí sacamos los números de trabajo.

