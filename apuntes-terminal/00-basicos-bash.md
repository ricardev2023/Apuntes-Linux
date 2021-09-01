---
description: Conceptos y comándos básicos de bash.
---

# 00- BÁSICOS BASH

## CONCEPTOS BÁSICOS

### **COMODINES DEL TERMINAL**

**?** --&gt; Representa un único caracter cualquiera. \(tambien se puede representar con un punto como en grep\)

**\*** --&gt; Representa desde nada hasta cualquier cantidad de letras o digitos.

**\[1-5\]** --&gt; Representa un rango de digitos o letras \(guiado por ASCII\)

**\[!1-5\]** --&gt; Representa todo lo que no esta en el rango marcado

**{}** --&gt; Permite crear una lista para que se aplique el comando a todos. P.E: cp {sda\*,sdb\*} /usr/share

**\** --&gt; Secuencia de escape. Sirve para utilizar un comodin como caracter normal

**^\#** --&gt; Implica que la linea comience por \# \(en este caso\)

### **ATAJOS DEL TERMINAL**

**./** --&gt; Significa "en el directorio en el que me encuentro"  
 \(Ejecuta un archivo\) \*Debe tener permisos de ejecución\*

**reverse-i-search** --&gt;Se inicia con **ctrl + r**  
 Busca en el historial con el inicio de comando que escriba.  
 Si hay varios que empiecen igual, navego con ctrl + r

**!!** --&gt; Toma como argumento el comando ejecutado anteriormente.

**!$** --&gt; Toma como argumento el argumento del comando ejecutado anteriormente

### **CONCATENAR--**

**;** --&gt; Permite ejecutar varios comandos uno detrás de otro. Aunque fallen.

**&&** --&gt; And booleano. Se tiene que ejecutar correctamente el primer comando para  
 que ejecute el siguiente.

**\|\|** --&gt; Or booleano. Si se ejecuta correctamente el primer comando no ejecuta los sigientes.  
 Permite ejecutar varios comandos para hacer lo mismo y cuando uno funciona, para.

### **REDIRECCIONES**

**&gt;** --&gt; Introduce el resultado de la ejecución del comando en un archivo. Eliminando el resto del contenido.

**2&gt;** --&gt; Introduce el error resultante de un comando mal ejecutado en un archivo. Elimina el resto del contenido.

**&&gt;** --&gt; Introduce el resultado de la ejecucion del comando en un archivo, si esta ejecucion implica parte correcta  
 y parte error

**&gt;&gt;** --&gt; Introduce el resultado de la ejecución del comando en un archivo. Añadiendolo al resto del contenido.

**2&gt;&gt;** --&gt; Lo mismo que &gt;&gt; pero para errores que aparecen por pantalla al ejecutar un comando.

**&&gt;&gt;** --&gt; Lo mismo que &gt;&gt; pero con error + ejecucion correcta a la vez

**&lt;** --&gt; Introduce el contenido de un archivo como entrada en la ejecución de un comando.

### **TUBERIAS**

**\|** --&gt; comando 1 \| comando 2 \| comando n

  
 la salida del comando 1 es la entrada del comando 2, que es, a su vez la entrada del comando n  
 por pantalla sale el resultado del comando n.

 `dpkg -l | grep ^rc | cut -d " " -f 3 | sudo xargs apt-get purge`

  
 En el ejemplo:  
 dpkg lista los programas instalados \(salida\).  
 grep busca en esos programas instalados \(entrada\) los que empiezan linea con rc \(salida\)  
 cut corta de los que empiezan con rc \(entrada\) la tercera columna separando con espacios \(salida\)  
 apt-get purge no puede coger cut como entrada por que no tiene entradas sino argumentos.  
 xargs convierte cut en argumento de apt-get purge.

### **FICHEROS IMPORTANTES**

**/etc/environment** --&gt; almacena los comandos marcados por los usuarios que se van a ejecutar al arrancar  
 el sistema. Si no lo hemos tocado, estara vacio.

**/etc/init.d/\[servicio\] \[start / stop / restart\]** --&gt; Para gestionar cualquier servicio del sistema.

**/boot/grub/grub.cfg** --&gt; archivo de configuracion del sistema de arranque grub. Si queremos modificarlo,  
 debemos modificar los script del fichero /etc/grub.d y despues ejecutar el comando update-grub.

**/etc/default/grub** --&gt; aqui si que puedo modificar algunas opciones del sistema de arranque.

## **COMANDOS BASICOS**

**MAN** --&gt; Manual \(muestra información acerca de un comando\)  
 Para buscar --&gt; /palabras a buscar \(n para buscar siguiente / N anterior\)  
`-k` --&gt; busca coincidencias con lo buscado  
 hay diferentes manuales:

 **1** --&gt; ejecutables y comandos de shell  
 **2** --&gt; llamadas al sistema  
 **3** --&gt; llamadas a librerias \(librerias en C\)  
 **4** --&gt; archivos especiales \(dispositivos: /dev/\)  
 **5** --&gt; informacion y formato de un archivo \(passwd, host, etc\)  
 **6** --&gt; juegos, salvapantallas, etc  
 **7** --&gt; comandos no estandar  
 **8** --&gt; comandos de administracion  
 **9** --&gt; subprogramas del nucleo

 `man -k passwd #busca todas las entradas de manual que contienen passwd en su titulo`  
 `man 5 passwd #pagina de informacion sobre el ARCHIVO /etc/passwd`

**INFO** --&gt; Informacion de un comando. como MAN pero mas visual

**HELP** --&gt; Informacion reducida de un comando.

**WHATIS** --&gt; Da la funcion de un comando \(man pero muy resumido\)

**SU** --&gt; Super User \(cambia al modo superusuario\)

**SUDO** --&gt; SuperUser Do \(permite a un usuario ejecutar un comando con permisos de otro usuario\)  
 Si no se especifica nombre de usuario, se toma por defecto el usuario root.  
 Saca la informacion del archivo /etc/sudoers  
 ****`-l` --&gt; lista los comandos a los que tienes acceso de superusuario.  
 ****`-u` --&gt; permite indicar con que usuario estamos ejecutando el comando.  
 ****`-e` --&gt; permite modificar un archivo como root  
 `-L` --&gt; lista todas las opciones de sudo

 **visudo** --&gt; sirve para abrir el archivo /etc/sudoers.tmp

**UPTIME** --&gt; imprime el tiempo que lleva arrancado el sistema.  
 - a que hora se ha arrancado  
 - cuanto tiempo lleva levantado  
 - cuantos usuarios hay activos  
 - carga: 1min 5min 15min

**UNAME** --&gt; Unix Name \(imprime informacion del sistema  
 ****`-a` --&gt; imprime toda la infromacion del sistema  
 `-s` ****--&gt; imprime el nombre del kernel \(por defecto\)  
 `-n` --&gt; imprime el nombre del nodo hostname  
 `-r` ****--&gt; indica la release del Kernel \(la mas importante\)  
 ****`-v` --&gt; imprime la version del Kernel  
 `-m` ****--&gt; imprime la arquitectura de la maquina  
 `-p` ****--&gt; imprime el tipo de procesador \(no en virtualizado\)  
 ****`-o` --&gt; imprime el SO

**HOSTNAME** --&gt; Muestra el nombre de la maquina \(como uname -n\)  
 llama al archivo /etc/hostname

**SEQ** --&gt; Genera una secuencia numerica  
`seq 5 2 11 #(genera una lista del 5 al 11 de 2 en 2)`  
 Si el numero intermedio es negativo, se puede hacer regresiva.

**HYSTORY** --&gt; \(lista los comandos que se han utilizado en el terminal\)  
 `!339` --&gt; permite ejecutar el comando que está en el puesto 339.  
 `-c` ****--&gt; limpia el historial de comandos

**FC** --&gt; Como el history pero con mas opciones. Mirar man.

**ALIAS** --&gt; Permite ponerle otro nombre a un comando más complejo  
 `alias`--&gt; lista los ya existentes  
 `alias [otro nombre]= '[comando complejo entre comillas simples]'`  
 PE: `alias mostrar= 'ls -la'`

**ECHO** --&gt; Muestra una informacion por pantalla.  
 ****`-n` --&gt; elimina el salto de pagina al final del echo.  
 `-e` --&gt; detecta los caracteres especiales del teclado en el texto.  
 **\t** tabulador  
 **\n** salto de linea

**XARGS** --&gt; Coge como argumento el resultado del comando anterior

**READ** --&gt; Coge informacion del teclado y la almacena en una variable  
`read nombre #almacena una variable llamada nombre`  
`read nombre apellido1 #almacena una variablle llamada nombre y otra llamada apellido`  
 `read -a color #almacena un array donde cada palabra tiene un identificador`  
 **`echo "los colores son: ${color[0]}, {color[1]}"`**  
 `read -p "pulsa intro para continuar" #hace una pausa hasta darle al intro`

**WHICH** --&gt; Permite saber donde está instalado un programa o comando.  
 P.E. --&gt; `which ls` --&gt; nos dice /bin/ls

**TYPE** --&gt; \(Permite saber si los comandos están instalados o son intrinsecos de la consola\)  
 `type ls #nos dice ls is /bin/ls`  
 `type cd #nos dice cd is a shell builtin`

 **CLEAR** --&gt; Limpia nuestro terminal.

**SLEEP** --&gt; Pone el terminal en modo espera durante los segundos que le marquemos.

**EXIT** --&gt; Sale del terminal o de la sesión de su.

**REBOOT** --&gt; Reinicia el sistema

**HALT / INIT 0** --&gt; Apaga por completo el SO.

**POWEROFF** --&gt; Apaga el SO.

**SHUTDOWN** --&gt; Programa el apagado del SO en 1 min.

