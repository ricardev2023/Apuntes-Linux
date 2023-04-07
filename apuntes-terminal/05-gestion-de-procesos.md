---
description: Comandos para la gestion de procesos y del sistema en ambientes Linux.
---

# 05- GESTIÓN DE PROCESOS

{% hint style="info" %}
Linux trabaja en dos planos de proceso: \
\- Primer plano: utiliza la consola activamente e impide que la pueda seguir utilizando \
\- Segundo plano: permite seguir utilizando la consola de comandos para otras cosas. \
\
Para mandar un comando a segundo plano hay que finalizar el comando con &. \
Para terminar un comando en primer plano ctrl+c \
Para pausar un comando en primer plano ctrl+z \

{% endhint %}

## &#x20;**NIVELES DE ACTIVACION DEL KERNEL**

&#x20;**Nivel 0** --> Sistema detenido. Se paran los servicios al apagar el sistema.

&#x20;**Nivel 1** --> Mantenimiento. Servicios detenidos. Usado por el root.

&#x20;**Nivel 2** --> Tareas de administración. No se suele usar.

&#x20;**Nivel 3** --> Todos los servicios iniciados pero sin entorno gráfico.

&#x20;**Nivel 4** --> Similar al nivel 2.

&#x20;**Nivel 5** --> Similar al 3 pero con entorno gráfico.

&#x20;**Nivel 6** --> Nivel temporal. Nivel de un sistema que está reiniciando.

## &#x20;**FICHEROS RELEVANTES**

&#x20;**/etc/crontab** --> nos permite modificar el system-wide crontab.

&#x20;**/etc/anacrontab** --> permite ejecutar periodicamente los procesos sin estar 24h encendida\
&#x20;por regla general, se ejecutan los cron, no procesos aislados.

&#x20;**/etc/cron.daily** --> directorio donde se encuentran las tareas diarias del cron.

&#x20;**/etc/cron.weekly** --> directorio donde se encuentran las tareas semanales del cron.

&#x20;**/etc/cron.monthly** --> directorio donde se encuentran las tareas mensuales del cron.

&#x20;**/var/spool/anacron/cron.\***--> pequeños ficheros con la ultima fecha que se inicio anacron.\
&#x20;(daily, weekly, monthly)

&#x20;**/etc/rc0.d a rcS.d** --> Se denominan runlevels y determinan que programas se ejecutan al inicio en LINUX.\
&#x20;**rc0** --> apagado del sistema\
&#x20;**rc1** --> modo monousuario (modo de rescate)\
&#x20;**rc2-5** --> modo multiusuario (por defecto)\
&#x20;**rc6** --> Reinicio del sistema\
&#x20;Dentro de cada nivel tenemos enlaces simbolicos a su carpeta en init.d que tienen la forma:\
&#x20;`[K | S] + nn + [string]`\
&#x20;**K** --> El servicio se detiene al llegar al runlevel\
&#x20;**S** --> El servicio se activa al llegar al runlevel\
&#x20;**nn** --> Dos numeros que indican la prioridad al llegar al runlevel\
&#x20;**90** es la prioridad para el inicio\
&#x20;**01** es la prioridad de detencion.

&#x20;Si se añade un comando a un runlevel, hay que utilizar el comando `update-rc.d`\
&#x20;`update-rc.d test.sh start 90 2 3 4 5 stop 01 0 1 6`\
&#x20;`update-rc.d test.sh defaults #pone los valores por defecto.`

## &#x20;**COMANDOS**

&#x20;**RUNLEVEL** --> Muestra el nivel de activación del kernel

&#x20;**TELINIT** --> Cambia el nivel de activacion del kernel

&#x20;**DMESG** --> Muestra el log de inicio del Kernel\
&#x20;`--clear` --> limpia los mensajes y lo deja en blanco\
&#x20;`-u` --> muestra solo los avisos del espacio usuario

&#x20;**PIDOF** --> muestra el PID de un proceso dado.

&#x20;**TOP** --> Muestra los procesos que se estan ejecutando en tiempo real.\
&#x20;**tecla q** para parar el TOP sin quitarlo de la pantalla\
&#x20;**tecla h** para ayuda.\
&#x20;**tecla k** para matar un proceso (necesario PID)\
&#x20;**tecla r** para cambiar las prioridades de un proceso (NI de -20 a 20)\
&#x20;**tecla p** para ordenar por % de uso de la cpu\
&#x20;**tecla ctrl+m** para ordenar por % de uso de memoria\
&#x20;**tecla esc** refresca la informacion

&#x20;**HTOP** --> como el top pero más gráfico. Requiere de instalación.

&#x20;**PS** --> Permite ver los procesos que se estan ejecutando en el Shell.\
&#x20;`-ef` --> Muestra todos los procesos.\
&#x20;`aux` --> Muestra todos los procesos del sistema.\
&#x20;`fax` --> Hace lo mismo que el ps aux pero en otro formato mas visual

&#x20;**SERVICE** --> permite modificar el estado en un servicio (un servicio puede tener varios procesos)\
&#x20;`status` --> info del servicio\
&#x20;`stop` --> mata un servicio\
&#x20;`start` --> inicia un servicio\
&#x20;`restart` --> reinicia un servicio

&#x20;Hace lo mismo que:\
&#x20;`/etc/init.d/[servicio] status/stop/start/restart`

&#x20;**JOBS** --> Permite ver los servicios que se estan ejecutando en segundo plano.\
&#x20;`fg %1` --> trae al primer plano el primer servicio del segundo plano\
&#x20;`bg %1` --> manda al segundo plano el primer servicio y lo reactiva.

&#x20;**NOHUP** --> Permite mantener un proceso activo aunque cierre la ventana

&#x20;**PGREP** --> Es el buscador global de procesos\
&#x20;`-n` --> muestra el PID del porceso activo\
&#x20;`-c [nombre de la aplicacion]`--> cuenta los procesos activos de esa aplicacion.

&#x20;**PSTREE** --> Muestra los procesos en forma de arbol

&#x20;**FUSER** --> muestra todos los procesos que utilizan socket en un directorio dado.\
&#x20;`-v` --> verbose\
&#x20;`-k` --> mata el proceso\
&#x20;`-i` --> modo interactivo (permite interactuar con la salida de fuser)

&#x20;**CRONTAB** --> Permite crear un proceso en segundo plano que se ejecute periodicamente.

&#x20;`-l` --> listar proceso ejecutando\
&#x20;`-r` --> eliminar un proceso de crontab\
&#x20;`-e` --> editar o crear un proceso de crontab

&#x20;Los datos a introducir son:\
&#x20;**minutos** --> 0-59 (si ponemos \* todos los minutos cumpliran la condición)\
&#x20;**horas** --> 0-23\
&#x20;**Día del mes** --> 1-31\
&#x20;**mes** --> 1-12 (o meses en inglés\
&#x20;**día de la semana** --> 0-6 (domingo = 0)\
&#x20;**comando a ejecutar** en el momento que se cumpla todo lo anterior.

&#x20;**AT** --> Programa una tarea para una sola vez\
&#x20;`atq` --> lista las tareas pendientes\
&#x20;`atrm` --> elimina la tarea del ID marcado\
&#x20;`-t` --> se le puede poner fecha a la tarea\
&#x20;P.E: `at -t 2008010700 #07:00 del 01 de Agosto de 2020`

&#x20;**NICE** --> inicia un proceso con la prioridad 10.\
&#x20;un usuario cualquiera puede cambiarla de 20 a 0 (0 es mas prioritario)\
&#x20;el usuario root puede cambiarla de 20 a -20 (siendo esta ultima la mas prioritaria)

&#x20;**RENICE** --> modifica la prioridad de un proceso

&#x20;**KILL** --> finaliza un proceso sabiendo su PID\
&#x20;`-1` --> para y reinicia el proceso\
&#x20;`-2` --> termina el proceso\
&#x20;`-9` --> fuerza el cierre\
&#x20;`-15` --> solicita finalizar (cierra de buenas)\
&#x20;`-18` --> reactivacion (despues de usar -19)\
&#x20;`-19` --> pausa

&#x20;**PKILL** --> finaliza un proceso por su nombre

&#x20;**LSOF** --> muestra los ficheros y librerias que se utilizan en los procesos activos.\
&#x20;Si no pongo nada, me lo muestra de todos los procesos de sistema.\
&#x20;Si solo quiero uno, tengo que poner el proceso concreto\
&#x20;`-i` --> muestra los puertos que nos muestran al exterior.\
&#x20;`-p` --> muestra todos los procesos relacionados con un PID.\
&#x20;`` -p `pidof [proceso]` `` --> lo mismo pero sin poner PID.

&#x20;**LSMOD** --> Lista los modulos instalados en el sistema.

&#x20;**MODPROVE** --> Habilita un módulo concreto.

&#x20;**RMMOD** --> Deshabilita un módulo concreto.

&#x20;**SYSCTL** --> Permite configurar los parametros del kernel\
&#x20;`-a` --> Lista los parametros\
&#x20;`-w` --> Permite modificarlos

&#x20;**LDD** --> Indica que librerias utiliza un programa concreto

&#x20;**FREE** --> Indica el uso de la memoria RAM
