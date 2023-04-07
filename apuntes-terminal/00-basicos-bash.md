---
description: Conceptos y comándos básicos de bash.
---

# 00- BÁSICOS BASH

## CONCEPTOS BÁSICOS

### **COMODINES DEL TERMINAL**

**?** --> Representa un único caracter cualquiera. (tambien se puede representar con un punto como en grep)

**\*** --> Representa desde nada hasta cualquier cantidad de letras o digitos.

**\[1-5]** --> Representa un rango de digitos o letras (guiado por ASCII)

**\[!1-5]** --> Representa todo lo que no esta en el rango marcado

**{}** --> Permite crear una lista para que se aplique el comando a todos. P.E: cp {sda\*,sdb\*} /usr/share

**\\** --> Secuencia de escape. Sirve para utilizar un comodin como caracter normal

**^#** --> Implica que la linea comience por # (en este caso)

### **ATAJOS DEL TERMINAL**

**./** --> Significa "en el directorio en el que me encuentro"\
&#x20;(Ejecuta un archivo) \*Debe tener permisos de ejecución\*

**reverse-i-search** -->Se inicia con **ctrl + r**\
&#x20;Busca en el historial con el inicio de comando que escriba.\
&#x20;Si hay varios que empiecen igual, navego con ctrl + r

**!!** --> Toma como argumento el comando ejecutado anteriormente.

**!$** --> Toma como argumento el argumento del comando ejecutado anteriormente

### **CONCATENAR--**

**;** --> Permite ejecutar varios comandos uno detrás de otro. Aunque fallen.

**&&** --> And booleano. Se tiene que ejecutar correctamente el primer comando para\
&#x20;que ejecute el siguiente.

**||** --> Or booleano. Si se ejecuta correctamente el primer comando no ejecuta los sigientes.\
&#x20;Permite ejecutar varios comandos para hacer lo mismo y cuando uno funciona, para.

### **REDIRECCIONES**

**>** --> Introduce el resultado de la ejecución del comando en un archivo. Eliminando el resto del contenido.

**2>** --> Introduce el error resultante de un comando mal ejecutado en un archivo. Elimina el resto del contenido.

**&>** --> Introduce el resultado de la ejecucion del comando en un archivo, si esta ejecucion implica parte correcta\
&#x20;y parte error

**>>** --> Introduce el resultado de la ejecución del comando en un archivo. Añadiendolo al resto del contenido.

**2>>** --> Lo mismo que >> pero para errores que aparecen por pantalla al ejecutar un comando.

**&>>** --> Lo mismo que >> pero con error + ejecucion correcta a la vez

**<** --> Introduce el contenido de un archivo como entrada en la ejecución de un comando.

### **TUBERIAS**

**|** --> comando 1 | comando 2 | comando n

\
&#x20;la salida del comando 1 es la entrada del comando 2, que es, a su vez la entrada del comando n\
&#x20;por pantalla sale el resultado del comando n.

&#x20;`dpkg -l | grep ^rc | cut -d " " -f 3 | sudo xargs apt-get purge`

\
&#x20;En el ejemplo:\
&#x20;dpkg lista los programas instalados (salida).\
&#x20;grep busca en esos programas instalados (entrada) los que empiezan linea con rc (salida)\
&#x20;cut corta de los que empiezan con rc (entrada) la tercera columna separando con espacios (salida)\
&#x20;apt-get purge no puede coger cut como entrada por que no tiene entradas sino argumentos.\
&#x20;xargs convierte cut en argumento de apt-get purge.

### **FICHEROS IMPORTANTES**

**/etc/environment** --> almacena los comandos marcados por los usuarios que se van a ejecutar al arrancar\
&#x20;el sistema. Si no lo hemos tocado, estara vacio.

**/etc/init.d/\[servicio] \[start / stop / restart]** --> Para gestionar cualquier servicio del sistema.

**/boot/grub/grub.cfg** --> archivo de configuracion del sistema de arranque grub. Si queremos modificarlo,\
&#x20;debemos modificar los script del fichero /etc/grub.d y despues ejecutar el comando update-grub.

**/etc/default/grub** --> aqui si que puedo modificar algunas opciones del sistema de arranque.

## **COMANDOS BASICOS**

**MAN** --> Manual (muestra información acerca de un comando)\
&#x20;Para buscar --> /palabras a buscar (n para buscar siguiente / N anterior)\
`-k` --> busca coincidencias con lo buscado\
&#x20;hay diferentes manuales:

&#x20;**1** --> ejecutables y comandos de shell\
&#x20;**2** --> llamadas al sistema\
&#x20;**3** --> llamadas a librerias (librerias en C)\
&#x20;**4** --> archivos especiales (dispositivos: /dev/)\
&#x20;**5** --> informacion y formato de un archivo (passwd, host, etc)\
&#x20;**6** --> juegos, salvapantallas, etc\
&#x20;**7** --> comandos no estandar\
&#x20;**8** --> comandos de administracion\
&#x20;**9** --> subprogramas del nucleo

&#x20;`man -k passwd #busca todas las entradas de manual que contienen passwd en su titulo`\
&#x20;`man 5 passwd #pagina de informacion sobre el ARCHIVO /etc/passwd`

**INFO** --> Informacion de un comando. como MAN pero mas visual

**HELP** --> Informacion reducida de un comando.

**WHATIS** --> Da la funcion de un comando (man pero muy resumido)

**SU** --> Super User (cambia al modo superusuario)

**SUDO** --> SuperUser Do (permite a un usuario ejecutar un comando con permisos de otro usuario)\
&#x20;Si no se especifica nombre de usuario, se toma por defecto el usuario root.\
&#x20;Saca la informacion del archivo /etc/sudoers\
&#x20;`-l` --> lista los comandos a los que tienes acceso de superusuario.\
&#x20;`-u` --> permite indicar con que usuario estamos ejecutando el comando.\
&#x20;`-e` --> permite modificar un archivo como root\
&#x20;`-L` --> lista todas las opciones de sudo

&#x20;**visudo** --> sirve para abrir el archivo /etc/sudoers.tmp

**UPTIME** --> imprime el tiempo que lleva arrancado el sistema.\
&#x20;\- a que hora se ha arrancado\
&#x20;\- cuanto tiempo lleva levantado\
&#x20;\- cuantos usuarios hay activos\
&#x20;\- carga: 1min 5min 15min

**UNAME** --> Unix Name (imprime informacion del sistema\
&#x20;`-a` --> imprime toda la infromacion del sistema\
&#x20;`-s` --> imprime el nombre del kernel (por defecto)\
&#x20;`-n` --> imprime el nombre del nodo hostname\
&#x20;`-r` --> indica la release del Kernel (la mas importante)\
&#x20;`-v` --> imprime la version del Kernel\
&#x20;`-m` --> imprime la arquitectura de la maquina\
&#x20;`-p` --> imprime el tipo de procesador (no en virtualizado)\
&#x20;`-o` --> imprime el SO

**HOSTNAME** --> Muestra el nombre de la maquina (como uname -n)\
&#x20;llama al archivo /etc/hostname

**SEQ** --> Genera una secuencia numerica\
`seq 5 2 11 #(genera una lista del 5 al 11 de 2 en 2)`\
&#x20;Si el numero intermedio es negativo, se puede hacer regresiva.

**HYSTORY** --> (lista los comandos que se han utilizado en el terminal)\
&#x20;`!339` --> permite ejecutar el comando que está en el puesto 339.\
&#x20;`-c` --> limpia el historial de comandos

**FC** --> Como el history pero con mas opciones. Mirar man.

**ALIAS** --> Permite ponerle otro nombre a un comando más complejo\
&#x20;`alias`--> lista los ya existentes\
&#x20;`alias [otro nombre]= '[comando complejo entre comillas simples]'`\
&#x20;PE: `alias mostrar= 'ls -la'`

**ECHO** --> Muestra una informacion por pantalla.\
&#x20;`-n` --> elimina el salto de pagina al final del echo.\
&#x20;`-e` --> detecta los caracteres especiales del teclado en el texto.\
&#x20;**\t** tabulador\
&#x20;**\n** salto de linea

**XARGS** --> Coge como argumento el resultado del comando anterior

**READ** --> Coge informacion del teclado y la almacena en una variable\
`read nombre #almacena una variable llamada nombre`\
`read nombre apellido1 #almacena una variablle llamada nombre y otra llamada apellido`\
&#x20;`read -a color #almacena un array donde cada palabra tiene un identificador`\
&#x20;**`echo "los colores son: ${color[0]}, {color[1]}"`**\
&#x20;`read -p "pulsa intro para continuar" #hace una pausa hasta darle al intro`

**WHICH** --> Permite saber donde está instalado un programa o comando.\
&#x20;P.E. --> `which ls` --> nos dice /bin/ls

**TYPE** --> (Permite saber si los comandos están instalados o son intrinsecos de la consola)\
&#x20;`type ls #nos dice ls is /bin/ls`\
&#x20;`type cd #nos dice cd is a shell builtin`

&#x20;**CLEAR** --> Limpia nuestro terminal.

**SLEEP** --> Pone el terminal en modo espera durante los segundos que le marquemos.

**EXIT** --> Sale del terminal o de la sesión de su.

**REBOOT** --> Reinicia el sistema

**HALT / INIT 0** --> Apaga por completo el SO.

**POWEROFF** --> Apaga el SO.

**SHUTDOWN** --> Programa el apagado del SO en 1 min.
