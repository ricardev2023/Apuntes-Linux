---
description: Gestión de registros en sistemas Linux.
---

# 09- REGISTROS

## **INFORMACION GENERAL**

Existen dos aplicaciones para almacenar y presentar logs: journalctl y rsyslog. Ambas sirven para lo mismo y se utilizan indistintamente en funcion de las preferencias del programador. En este documento vamos a ver el uso de ambas.

## **FICHEROS DE UTILIDAD**

**/etc/systemd/journald.conf** --&gt; Fichero de configuracion del servicio journal \(por defecto está todo comentado\).

**/etc/rsyslog.conf** --&gt; Fichero de configuracion del servicio rsyslog**.**

**/etc/logrotate.conf** --&gt; Fichero de configuración de la rotación de logs. En el se puede estipular cada cuanto se eliminan los logs, se comprimen, se hace copia de seguridad o se envían por e-mail entre otras cosas.

## RSYSLOG VS SYSTEMD

**SYSLOG** --&gt; Fué el primer sistema de log consolidado, cuyo proyecto comenzó en 1980 y se extendió durante bastantes años. Sólo soporta UDP no garantizando la el almacenamiento de todos los mensajes.

**SYSLOG-NG** --&gt; Se realiza a partir de 1998 y mejora las capacidades de syslog:

* Filtros basados en contenido
* Logging directamente a base de datos
* Ofrece transporte TCP
* Ofrece encreiptación TLS

**RSYSLOG** --&gt; El siseño de syslog-ng se mejoró desde 2004 con rsyslog añadiéndo las siguientes funcionalidades básicas:

* Soporte de protocolo RELP
* Soporte de operaciones en Búfer

**JOURNALD** --&gt; Con el nuevo systema de inicio **SYSTEMD** se implementa el nuevo journald como servicio y recolección de logs.

* No se almacena la información en texto plano, sino el archivos binarios aumentando la seguridad.
* Se almacena al información de manera estructurada.
* Se requiere la herramienta journalctl para interpretar los logs.

## SYSTEMD

**SYSTEMD** es un conjunto de daemons de administración de sistema, bibliotecas y herramientas diseñados como una plataforma de administración y configuración central para interactuar con el núcleo del Sistema operativo GNU/Linux.

**JOURNAL** es la herramienta de Systemd que permite administrar de manera centralizada la informacion  
de los logs del sistema.

**JOURNALD** es el demonio que implementa este servicio.

**JOURNALCTL** --&gt; utilidad que permite acceder y manipular los datos del log:

 `-b` --&gt; mensajes en el arranque del sistema. Si añadimos:  
 `-0` --&gt; mensajes del ultimo arranque del sistema  
 `-1` --&gt; mensajes del anterior arranque \(los arranques tienen un ID de arranque\)

 `-f` --&gt; mensajes del sistema en directo. \(marca ademas el PID del servicio de cada entrada del log\)  
 `_PID=[PID]` --&gt; Muestra los mensajes de log del servicio con PID marcado.

Una característica de journald es que la información se almacena de forma volátil por defecto. Se configura rsyslog para tomar los datos de journald y enviarlos al archivo /var/log para lograr la persistencia. Además permite almacenar enviar los registros a un servidor centralizado para su persistencia.

Para hacer la **información persistente:**

`mkdir –p /var/log/journal`  
`systemd–tmpfiles —create —prefix /var/log/journal`

## **RSYSLOG**

Rsyslog es un daemon encargado de recolectar los mensajes de servicios que provienen de aplicaciones  
y el núcleo para luego distribuirlos en archivos de registros \(normalmente almacenados en el directorio  
/var/log\). Dicho daemon obedece los parámetros de configuración del fichero /etc/rsyslog.conf.

Maneja mensajes de diferentes tipo, ya que cada mensaje de registro se encuentra asociado con una facilidad:

* **AUTH Y AUTHPRIV**: para autenticación en el sistema.
* **CRON**: proviene servicios de programación de tareas, cron y atd.
* **DAEMON**: afecta un demonio sin clasificación especial \(DNS, NTP, etc.\).
* **FTP**: el servidor FTP.
* **KERN**: mensaje que proviene del núcleo.
* **LPR**: proviene del subsistema de impresión.
* **MAIL**: proviene del subsistema de correo electrónico.
* **NEWS**: mensaje del subsistema Usenet \(especialmente de un servidor NNTP — protocolo de transferencia de noticias en red, «Network News Transfer Protocol» — que administra grupos de noticias\).
* **SYSLOG**: mensajes del servidor syslogd en sí.
* **USER**: mensajes de usuario \(genéricos\).
* **UUCP**: mensajes del servidor UUCP \(programa de copia Unix a Unix, «Unix to Unix Copy Program», un  protocolo antiguo utilizado notablemente para distribuir correo electrónico\).
* **LOCAL0** **A LOCAL7**: reservados para uso local.

Cada mensaje tiene asociado un **nivel de prioridad**, dependiendo de la gravedad del mensaje en el log,  
estará etiquetada con un nivel de prioridad u otro. Los niveles de prioridad son los que aparecen a  
continuación y van **ordenado de mayor a menor gravedad**:

* **EMERG**: «¡Ayuda!» Hay una emergencia y el sistema probablemente está inutilizado.
* **ALERT**: apúrese, cualquier demora puede ser peligrosa, debe reaccionar inmediatamente.
* **CRIT**: las condiciones son críticas.
* **ERR**: error.
* **WARN**: advertencia \(error potencial\).
* **NOTICE**: las condiciones son normales pero el mensaje es importante.
* **INFO**: mensaje informativo.
* **DEBUG**: mensaje de depuración.

Por ultimo tenemos la **accion**, que equivale a el fichero donde se almacena el log de cada facilidad.

En el fichero `/etc/rsyslog.conf` hay un apartada llamado RULES que estructura la informacion desarrollada anteriormente:

`auth,authpriv.* /var/log/auth.log #coge los logs relacionados con la autenticacion de cualquier prioridad y los guarda en esa ruta).`

### **COMANDOS**

**LOGGER** --&gt; añade un mensaje al log \(syslog\)  
 `-i` --&gt; añade un PID al mensaje de log añadido.  
 `-p` --&gt; genera el mensaje con Facilidad y prioridad.

## REFERENCIAS

[https://www.mundotelematico.com/syslog-rsyslog-syslog-ng-y-journald/](https://www.mundotelematico.com/syslog-rsyslog-syslog-ng-y-journald/)

