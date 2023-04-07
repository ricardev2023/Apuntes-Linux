---
description: Comandos para el montaje y la gestión de discos y dispositivos.
---

# 07- MONTAJE DE DISCOS Y DISPOSITIVOS

PARTICIONADO, FORMATEADO, MONTAJE DE DISCOS.\
CREACION DE CUOTAS DE DISCO PARA USUARIOS Y DISCOS.\
CONEXIONES PCI Y USB DEL DISCO.

## **INFORMACION BASICA**

* Los dispositivos en Linux deben estar siempre montados en el sistema.
* Los discos duros se suelen montar en **/dev/**
* Dispositivos CD-ROM o USB, se montan en **/media/**
* Las carpetas compartidas las monta en **/mnt/**
* Tambien puedo montar los dispositivos donde yo quiera.

Cuando se ejecuta `fdisk -l`, lista los discos y las particiones de cada uno de ellos.\
El primer disco se representa como `/dev/sda` . Esto significa que esta montado en dev\
y se llama sda (a por ser el primero, el segundo es b, c, etc). Sus particiones serán:

* **sda1 a sda4** --> Particiones primarias (de arranque) y extendidas.
* **sda5 en adelante** --> Particiones logicas

{% hint style="info" %}
Para poder utilizar un disco duro recien instalado, hay que particionarlo para ello utilizamos `fdisk.`\
Despues, debemos formatearlo para lo que utilizamos `mkfs`.\
Por ultimo, lo podemos montar donde queramos con `mount`.
{% endhint %}

Para poder utilizar un disco duro recien instalado, hay que particionarlo para ello utilizamos `fdisk.`\
Despues, debemos formatearlo para lo que utilizamos `mkfs`.\
Por ultimo, lo podemos montar donde queramos con `mount`.

**/etc/fstab** --> fichero donde se configuran los discos que se montan de inicio.\
&#x20;Si no se pone en este fichero, cada vez que inicie sesion tendre que montarlo.

* **\<file system>** Cual es el disco que vamos a montar en inicio.\
  &#x20;los identifica con UUID (se encuentra con comando blkid)\
  &#x20;tambien se puede identificar con nombre P.E: /dev/sdb1
* **\<mount point>** Donde vamos a montar el disco
* **\<type>** Que tipo de sistema de datos utiliza (normalmente ext4)
* &#x20;**\<options>** Opciones (hay que ver el manual, si no, default)
* **\<dump>** Copia de seguridad en inicio
* **\<pass>** comprobacion de errores (comando fsck). Va mas lento el inicio.

**/etc/mtab** --> fichero donde se listan todos los discos montados en el sistema\
&#x20;Es el fichero que se llama al hacer mount.

### **COMANDOS GESTION DE DISCOS**

**FDISK** --> Herramienta para gestionar el particionado del **disco duro tipo MBR**.\
&#x20;`-l` --> lista las particiones y los discos presentes en el sistema

Para gestionar un disco, hacemos lo siguiente:&#x20;

1. `fdisk /dev/sdb` En caso de querer gestionar sdb
2. Con la letra **m** muestra la ayuda.
3. Con la letra **n** se inicia un nuevo particionado.
4. El programa interroga si es partición primaria o extendida (empezamos con primaria).
5. Solicita el numero de la particion (por defecto 1).
6. Solicita el primer sector. Lo normal es empezar por el primero libre que ademas es el\
   predefinido.
7. Solicita el último sector. Por defecto la hace de todo el disco duro. Para darle un tamaño\
   utilizamos, por ejemplo: +2G (2Gb de particion)
8. Ya está la partición hecha.

**GDISK** --> Herramienta para gestionar el particionado de **discos duros tipo GPT**. Es mas novedoso que MBR, tiene sus ventajas y sus inconvenientes. Funciona muy parecido a fdisk. Utiliza un **GUID** (id unico de cada disco duro, no depende de la maquina)\
`gdisk sdb -l` --> Da listado de particiones del disco b (no funciona -l sin seleccionar disco)

**PARTED** --> Programa parecido al fdisk. Sirve para MBR y para GPT. Es mucho mas compleja de utilizar que las anteriores.\
&#x20;`-l` --> lista particiones y los discos presentes en el sistema.

**MKFS** --> Permite dar formato a un dispositivo de almacenamiento con un sist. de archivos.\
`-t` --> tipo de sist. de archivos. (P.E: ext4)\
tambien se puede hacer con mkfs.ext4 (si pongo mkfs. y doy al tab, me salen opciones)\
`-c` --> comprueba los bloques\
P.E: `mkfs -c -t ext4 /dev/sdb2 #formatea la particion 2 del disco b en ext4`

**MKE2FS** --> Comando antiguo para formatear en ext2.

**MOUNT** --> Gestiona los dispositivos montados.\
&#x20;`mount` --> Lista los dispositivos montados y donde. (llama al fichero `/etc/mtab`)\
&#x20;`mount /dev/sdb1 /mnt/disco1` (monta la particion 1 del disco b en la carpeta disco1)\
&#x20;Para que funcione la particion debe estar formateada con un formato de archivos.\
&#x20;`-a` --> monta todos los discos del fichero /etc/fstab\
&#x20;`-r` --> monta un disco en modo solo lectura.\
&#x20;`-o` --> modifica las opciones de montaje de un disco (segun los que tiene en /etc/fstab)\
&#x20;`-t` --> modifica el tipo de sistema de datos del disco para montaje.

**UMOUNT** --> Desmonta un disco montado en la ruta descrita.\
&#x20;`-a` --> desmonta todos los discos del fichero /etc/fstab\
&#x20;No se pueden desmontar si estan en uso.

**DF** --> Disk Free. Indica informacion acerca de todos los dispositivos montados)\
&#x20;`-h` --> pone los tamaños para que los entienda un humano.\
&#x20;`-H` --> permite ver el tamaño en mb/Gb etc. (hay que marcar que tipo de unidad quiero)\
&#x20;`-T` --> muestra el tipo de formato de archivos del disco montado

**DU** --> Disk Usage (indica como se utiliza el espacio en una determinada carpeta o disco)\
&#x20;`-h` --> pone los tamaños para ser leido por humanos.\
&#x20;`-s` --> muestra el tamaño.\
&#x20;`-a` --> muestra el uso para todos los ficheros encontrados, no solo los directorios.\
&#x20;`-c` --> muestra el total para todos los argumentos dados.\
&#x20;`-k` --> muestra el resultado en kb.\
&#x20;`-m` --> muestra el resultado en Mb.

**FSCK** --> Comprobacion de errores en discos. Deben estar desmontados para poder ejecutarlos\
&#x20;P.E: `fsck.ext4 /dev/sdc1`\
&#x20;`-a` --> Para solucionar problemas (INVESTIGAR)\
&#x20;`-p` --> Lo mismo que el -a (INVESTIGAR)\
&#x20;`-f` --> Fuerza la reparacion del disco\
&#x20;`-y` --> Por defecto dice que si a todo.

**DUMPE2FS** --> Saca informacion de los bloques (se utiliza para Benchmark de discos duros P.E.)

**BLKID** --> Informacion acerca de los discos con UUID.\
Es muy útil para obtener el UUID de un disco duro que queremos particionar.

**E2FSCK** -->Comando antiguo para comprobar errores en sistemas de archivos ext2.

**TUNE2FS** --> Pasa de ext2 a ext 3 (con la opcion -j)

## **COTAS DE DISCO**

Permite controlar el espacio asignado a cada usuario en un sistema.

* **Soft Limit** --> Avisa de que se esta llegando al limite de espacio
* **Hard Limit** --> No permite seguir almacenando nueva informacion.
* **Bloques** --> Unidad de almacenamiento mas pequeña (4kb por defecto). Solo puede contener un archivo.
* **Inodos** --> Contiene la informacion de un fichero o directorio y sus metadatos (lo que muestra ls -l)

Para definir las cuotas, vamos a hacer lo siguiente:

1. `apt-get install quota*`
2. En **/etc/fstab** buscamos el disco en que vayamos a definir cuotas y ponemos en opciones:\
   &#x20;`defaults,usrquota,grpquota`
3. volvemos a montar el disco para que se apliquen los cambios en las opciones:\
   &#x20;`mount -o remount /mnt/disco1`
4. Comprobamos que el disco en el que quiero definir las cuotas, las soporta:\
   &#x20;`quotacheck -ugmv /mnt/disco1`
5. Activo las cuotas en el disco:\
   &#x20;`quotaon -ugv /mnt/disco1`
6. Administro las cuotas (modificando soft y hard):\
   &#x20;`edquota -u prueba`
7. Comprobamos el espacio disponible en mi cuota (usuario activo).\
   &#x20;`quota -sp`
8. Modificamos el periodo de gracia. (lo podemos cambiar por bloques o por inodos)\
   &#x20;`edquota -t`
9. Para terminar, comprobar las cuotas de todos para comprobar fallos.\
   &#x20;`repquota -asv`

### **COMANDOS COTAS DE DISCO**

**QUOTACHECK** --> verifica el sistema de cuotas de un disco.\
&#x20;`-a` --> analiza todos los sistema del /etc/mtab\
&#x20;`-u` --> comprueba el soporte de cuotas de usuario\
&#x20;`-g` --> comprueba el soporte de cuotas de grupo\
&#x20;`-m` --> evita que los discos con la opcion remount-ro se monten en modo solo lectura.\
&#x20;`-v` --> verbose\
&#x20;`-f` --> force

**QUOTAON** --> Activar las cuotas.\
&#x20;Las mismas opciones que quotacheck excepto f:\
&#x20;`-f` --> quota off

**EDQUOTA** --> para administrar las cuotas.\
&#x20;`-t` --> para administrar el tiempo de gracia en dias por bloques o inodos.

**QUOTA** --> para ver el espacio restante en mi cuota.\
&#x20;`-s` --> legible por humanos.\
&#x20;`-p` --> muestra el tiempo de gracia en segundos ya pasados.

**REPQUOTA** --> reporte del estado de las cuotas\
&#x20;`-a` --> para todas las cuotas\
&#x20;`-v` --> verbose\
&#x20;`-s` --> legible por humanos

**LSPCI** --> Lista las conexiones PCI del interior de nuestra maquina\
&#x20;En sistemas virtualizados no funciona al 100%.

**LSUSB** --> Lista las conexiones USB de nuestra maquina.
