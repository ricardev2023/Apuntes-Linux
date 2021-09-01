---
description: Comandos para la gestion de procesos y del sistema en ambientes Linux.
---

# 05- GESTIÓN DE PROCESOS

{% hint style="info" %}
Linux trabaja en dos planos de proceso:   
- Primer plano: utiliza la consola activamente e impide que la pueda seguir utilizando   
- Segundo plano: permite seguir utilizando la consola de comandos para otras cosas.   
  
Para mandar un comando a segundo plano hay que finalizar el comando con &.   
Para terminar un comando en primer plano ctrl+c   
Para pausar un comando en primer plano ctrl+z   
{% endhint %}

##  **NIVELES DE ACTIVACION DEL KERNEL**

 **Nivel 0** --&gt; Sistema detenido. Se paran los servicios al apagar el sistema.

 **Nivel 1** --&gt; Mantenimiento. Servicios detenidos. Usado por el root.

 **Nivel 2** --&gt; Tareas de administración. No se suele usar.

 **Nivel 3** --&gt; Todos los servicios iniciados pero sin entorno gráfico.

 **Nivel 4** --&gt; Similar al nivel 2.

 **Nivel 5** --&gt; Similar al 3 pero con entorno gráfico.

 **Nivel 6** --&gt; Nivel temporal. Nivel de un sistema que está reiniciando.

##  **FICHEROS RELEVANTES**

 **/etc/crontab** --&gt; nos permite modificar el system-wide crontab.

 **/etc/anacrontab** --&gt; permite ejecutar periodicamente los procesos sin estar 24h encendida  
 por regla general, se ejecutan los cron, no procesos aislados.

 **/etc/cron.daily** --&gt; directorio donde se encuentran las tareas diarias del cron.

 **/etc/cron.weekly** --&gt; directorio donde se encuentran las tareas semanales del cron.

 **/etc/cron.monthly** --&gt; directorio donde se encuentran las tareas mensuales del cron.

 **/var/spool/anacron/cron.\***--&gt; pequeños ficheros con la ultima fecha que se inicio anacron.  
 \(daily, weekly, monthly\)

 **/etc/rc0.d a rcS.d** --&gt; Se denominan runlevels y determinan que programas se ejecutan al inicio en LINUX.  
 **rc0** --&gt; apagado del sistema  
 **rc1** --&gt; modo monousuario \(modo de rescate\)  
 **rc2-5** --&gt; modo multiusuario \(por defecto\)  
 **rc6** --&gt; Reinicio del sistema  
 Dentro de cada nivel tenemos enlaces simbolicos a su carpeta en init.d que tienen la forma:  
 `[K | S] + nn + [string]`  
 **K** --&gt; El servicio se detiene al llegar al runlevel  
 **S** --&gt; El servicio se activa al llegar al runlevel  
 **nn** --&gt; Dos numeros que indican la prioridad al llegar al runlevel  
 **90** es la prioridad para el inicio  
 **01** es la prioridad de detencion.

 Si se añade un comando a un runlevel, hay que utilizar el comando `update-rc.d`  
 `update-rc.d test.sh start 90 2 3 4 5 stop 01 0 1 6`  
 `update-rc.d test.sh defaults #pone los valores por defecto.`

##  **COMANDOS**

 **RUNLEVEL** --&gt; Muestra el nivel de activación del kernel

 **TELINIT** --&gt; Cambia el nivel de activacion del kernel

 **DMESG** --&gt; Muestra el log de inicio del Kernel  
 `--clear` --&gt; limpia los mensajes y lo deja en blanco  
 `-u` --&gt; muestra solo los avisos del espacio usuario

 **PIDOF** --&gt; muestra el PID de un proceso dado.

 **TOP** --&gt; Muestra los procesos que se estan ejecutando en tiempo real.  
 **tecla q** para parar el TOP sin quitarlo de la pantalla  
 **tecla h** para ayuda.  
 **tecla k** para matar un proceso \(necesario PID\)  
 **tecla r** para cambiar las prioridades de un proceso \(NI de -20 a 20\)  
 **tecla p** para ordenar por % de uso de la cpu  
 **tecla ctrl+m** para ordenar por % de uso de memoria  
 **tecla esc** refresca la informacion

 **HTOP** --&gt; como el top pero más gráfico. Requiere de instalación.

 **PS** --&gt; Permite ver los procesos que se estan ejecutando en el Shell.  
 `-ef` --&gt; Muestra todos los procesos.  
 `aux` --&gt; Muestra todos los procesos del sistema.  
 `fax` --&gt; Hace lo mismo que el ps aux pero en otro formato mas visual

 **SERVICE** --&gt; permite modificar el estado en un servicio \(un servicio puede tener varios procesos\)  
 `status` --&gt; info del servicio  
 `stop` --&gt; mata un servicio  
 `start` --&gt; inicia un servicio  
 `restart` --&gt; reinicia un servicio

 Hace lo mismo que:  
 `/etc/init.d/[servicio] status/stop/start/restart`

 **JOBS** --&gt; Permite ver los servicios que se estan ejecutando en segundo plano.  
 `fg %1` --&gt; trae al primer plano el primer servicio del segundo plano  
 `bg %1` --&gt; manda al segundo plano el primer servicio y lo reactiva.

 **NOHUP** --&gt; Permite mantener un proceso activo aunque cierre la ventana

 **PGREP** --&gt; Es el buscador global de procesos  
 `-n` --&gt; muestra el PID del porceso activo  
 `-c [nombre de la aplicacion]`--&gt; cuenta los procesos activos de esa aplicacion.

 **PSTREE** --&gt; Muestra los procesos en forma de arbol

 **FUSER** --&gt; muestra todos los procesos que utilizan socket en un directorio dado.  
 `-v` --&gt; verbose  
 `-k` --&gt; mata el proceso  
 `-i` --&gt; modo interactivo \(permite interactuar con la salida de fuser\)

 **CRONTAB** --&gt; Permite crear un proceso en segundo plano que se ejecute periodicamente.

 `-l` --&gt; listar proceso ejecutando  
 `-r` --&gt; eliminar un proceso de crontab  
 `-e` --&gt; editar o crear un proceso de crontab

 Los datos a introducir son:  
 **minutos** --&gt; 0-59 \(si ponemos \* todos los minutos cumpliran la condición\)  
 **horas** --&gt; 0-23  
 **Día del mes** --&gt; 1-31  
 **mes** --&gt; 1-12 \(o meses en inglés  
 **día de la semana** --&gt; 0-6 \(domingo = 0\)  
 **comando a ejecutar** en el momento que se cumpla todo lo anterior.

 **AT** --&gt; Programa una tarea para una sola vez  
 `atq` --&gt; lista las tareas pendientes  
 `atrm` --&gt; elimina la tarea del ID marcado  
 `-t` --&gt; se le puede poner fecha a la tarea  
 P.E: `at -t 2008010700 #07:00 del 01 de Agosto de 2020`

 **NICE** --&gt; inicia un proceso con la prioridad 10.  
 un usuario cualquiera puede cambiarla de 20 a 0 \(0 es mas prioritario\)  
 el usuario root puede cambiarla de 20 a -20 \(siendo esta ultima la mas prioritaria\)

 **RENICE** --&gt; modifica la prioridad de un proceso

 **KILL** --&gt; finaliza un proceso sabiendo su PID  
 `-1` --&gt; para y reinicia el proceso  
 `-2` --&gt; termina el proceso  
 `-9` --&gt; fuerza el cierre  
 `-15` --&gt; solicita finalizar \(cierra de buenas\)  
 `-18` --&gt; reactivacion \(despues de usar -19\)  
 `-19` --&gt; pausa

 **PKILL** --&gt; finaliza un proceso por su nombre

 **LSOF** --&gt; muestra los ficheros y librerias que se utilizan en los procesos activos.  
 Si no pongo nada, me lo muestra de todos los procesos de sistema.  
 Si solo quiero uno, tengo que poner el proceso concreto  
 `-i` --&gt; muestra los puertos que nos muestran al exterior.  
 `-p` --&gt; muestra todos los procesos relacionados con un PID.  
 ``-p `pidof [proceso]``` --&gt; lo mismo pero sin poner PID.

 **LSMOD** --&gt; Lista los modulos instalados en el sistema.

 **MODPROVE** --&gt; Habilita un módulo concreto.

 **RMMOD** --&gt; Deshabilita un módulo concreto.

 **SYSCTL** --&gt; Permite configurar los parametros del kernel  
 `-a` --&gt; Lista los parametros  
 `-w` --&gt; Permite modificarlos

 **LDD** --&gt; Indica que librerias utiliza un programa concreto

 **FREE** --&gt; Indica el uso de la memoria RAM

