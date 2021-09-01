---
description: Gestión de servicios de hora y lenguaje en ambientes Linux
---

# 08- HORA Y LENGUAJE

## **INFORMACIÓN BÁSICA**

El servicio de hora es muy importante para los servicios. Por ejemplo, en un servidor, si la diferencia es de  
5 minutos con respecto al reloj del servidor, no se puede conectar. Por otra parte, si busco el servicio de log y no coinciden las fechas o las horas, no puedo realizar un analisis forense correcto.

Para ello existen los **NTP** \(network time protocol\) que no dejan de ser los servidores del servicio de hora  
en una red. Todos ellos cuelgan de otro **NTP** de mayor nivel colgando el demayor nivel de un reloj atomico.

En el flujo de informacion entre **NTP,s** pueden darse pequeños retrasos que pueden llegar a suponer una ruptura de la red si no se tienen en cuenta.

## **FICHEROS RELEVANTES**

**/usr/share/zoneinfo** --&gt; directorio donde se encuentran las configuraciones de las zonas horarias \(no ASCII\)

**/etc/localtime** --&gt; enlace simbolico a la zona horaria activa \(si cambio este enlace, cambio la zona activa\)

**/etc/ntp.conf** --&gt; fichero donde se almacenan los servidores ntp que vamos a utilizar.

**/etc/locale.gen** --&gt; ver las posibles variables del idioma \(instaladas y no instaladas\)

**/etc/default/locale** --&gt; almacena el idioma \(LANG\) a nivel global.

## **COMANDOS**

**DATE** --&gt; Permite ver la fecha y la hora del dispositivo.  
 `date MMDDhhmmYY #para cambiar la fecha y hora`

**CAL** --&gt; Saca el calendario del mes presente  
 se puede elegir el mes que uno quiere. P.E: `cal 4 2020`

**HWCLOCK** --&gt; Muestra la hora del hardware  
 `--hctosys` --&gt; sincroniza la hora del sistema \(la cambia\) con la de la bios.  
 `--systohc` --&gt; sincroniza la hora de la bios \(la cambia\) con la del sistema.  
 _MUY IMPORTANTE_ _PARA EL NTP_ \(network time protocol\)

**NTPQ** --&gt; Da informacion de los servidores ntp con los que enlaza el sistema. \(llama al contenido de `/etc/ntp.conf`\)  
 `-p` --&gt; Lista los servidores con los que enlaza el daemon de NTP.

**NTPDATE** --&gt; Ajusta el tiempo mediante NTP  
 `-u [nombre del servidor NTP]` --&gt; Ajusta con ese servidor.

**NTPDC** --&gt; Permite enlazar con el servidor NTP y pedirle informacion.  
 `-c loopinfo` --&gt; Da informacion de los estratos hasta el servidor NTP.  
 En virtualizacion no funciona

**NTPTRACE** --&gt; Permite buscar fallos en el enlace con NTP.

**LOCALE** --&gt; permite ver el idioma que se está utilizando \(codeset\)  
 `-a` --&gt; Muestra los que tenemos disponibles en este momento.  
 `locale-gen` --&gt; Genera los locales \(a partir del /etc/locale.gen\)  
 export LC\_ALL=es\_ES.utf8

