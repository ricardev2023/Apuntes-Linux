---
description: Comandos para la gestión de permisos de recursos en ambientes Linux.
---

# 03- GESTIÓN DE PERMISOS EN ARCHIVOS Y DIRECTORIOS

## &#x20;**INFORMACION BASICA**

&#x20;Cuando usamos la opción -l en el comando ls para listar `ls -l`, mostrará el contenido de\
la carpeta en la que nos encontramos, o la que se indique en el comando, por ejemplo:\
`ls -l /root/Desktop`

&#x20;**`-rw-r–rwx root root 4566 mar 24 06:21 iptables.sh`**

&#x20;El resultado mostrado, dará información importante. Lo primero que nos encontramos,\
son un conjunto de 10 caracteres:

&#x20;`-rw-r–rwx`

* El primero elemento nos indica si es un archivo o una carpeta. En este caso al ser un\
  guión (-), sabemos que es un archivo. Si este paquete fuese (d) nos indicaría que es una\
  carpeta, pudiendo acceder con el comando cd.
* El segundo paquete (rw-): Esto nos dice que permisos tiene el propietario de este\
  archivo, en este caso r y w, es decir de lectura y escritura. No de ejecución, ya que en\
  vez de tener una (x) en su último caracter, tiene un guión -.
* Tercer paquete (r–): Son los permisos, NO del usuario propietario, si no del grupo\
  propietario. En este caso, todos los miembros del grupo propietario tienen solo permiso\
  de r (read) o lectura, no de (w), ni de (x), es decir, no pueden escribir, ni ejecutar este\
  archivo.
* Cuarto paquete(rwx): Nos dice que todos los usuarios, que NO sean el propietario\
  (segundo paquete), ni sean miembros del grupo de propietarios (tercer paquete), tienen\
  permiso de r (lectura), de w (escritura) y de x (ejecución).

{% hint style="info" %}
&#x20;Estos permisos pueden tener unos bits especiales en ejecucion:

&#x20;drwxrwxrwx --> esto es lo normal\
\---s------ --> **SUID** (todos los usuarios lo pueden ejecutar como propietario)\
\------s--- --> **SGID** (todo lo que entra en el directorio hereda el grupo propietario)\
\---------t --> **STICKY** (evita que los archivos sean borrados por usuarios no propietarios INCLUSO ROOT)
{% endhint %}

&#x20;Nos encontramos datos numéricos como su tamaño, fecha y hora. Finalmente el nombre del\
archivo, pero lo que quiero explicar es que son esas palabras: root root

* El primer **root**, es el usuario propietario, correspondiente al segundo paquete (rw-)
* El segundo **root**, es el grupo (no usuario) propietario, perteneciente a los permisos\
  del tercer paquete (r–)

## &#x20;**FICHEROS RELEVANTES**

&#x20;**/home/strelock/.profile** --> fichero oculto que contiene toda la informacion del usuario ricardo.\
&#x20;en este fichero se almacena la umask de cada usuario:

{% hint style="info" %}
umask 022 (equivale a permisos 755 predeterminados) \
Representa la diferencia entre los permisos maximos (777 para directorio o 666 para archivo) \
y los permisos predeterminados al crearlo. \
Se puede modificar para cada usuario.&#x20;
{% endhint %}

&#x20;**/home/strelock/.bashrc** --> fichero oculto que contiene toda la configuracion del usuario ricardo

## &#x20;**COMANDOS**

&#x20;**UMASK** --> permite cambiar la mascara de permisos.

&#x20;**CHMOD** --> Change mode (nos permite cambiar los permisos de un archivo o directorio)\
&#x20;`-R` --> Cambia los permisos de todos los archivos contenidos en una carpeta.

&#x20;P.E. (octal)--> `sudo chmod 037 /home/username/Escritorio/prueba.txt`

&#x20;**OCTAL**: Los permisos se dan con números del 0 al 7\
**0** --> - - -\
**1** --> - - x (permiso de ejecución)\
**2** --> - w - (permiso de escritura)\
**3** --> - w x \
**4** --> r - - (permiso de lectura) \
**5** --> r - x \
**6** --> r w - \
**7** --> r w x

\
&#x20;3 grupos de permisos:&#x20;

1. Primer número para el creador.
2. Segundo número para el grupo.
3. Tercer número para el resto.

&#x20;**CARACTER**: Los permisos se cambian usando 3 modificadores:

1. **u** (user) **g** (group) **o** (other) **a** (all)
2. **+** **-** **=** (añadir, eliminar o igualar)
3. **r** **w** **x** (tipo de permiso)

P.E.  `sudo chmod u=+x /home/username/Escritorio/prueba.txt`

### &#x20;**EJEMPLO**

&#x20;Si quisiera cambiar el usuario propietario, a otro usuario existente, por ejemplo\
javier, usaría el comando:

&#x20;`chown javier iptables.sh`

&#x20;Dando un `ls -l` aparecería lo siguiente:

&#x20;`-rw-r–rwx javier root 4566 mar 24 06:21 iptables.sh`

&#x20;Si ahora además quiero cambiar el grupo propietario por ejemplo a alumnos (debe existir\
o ser creado antes), uso el siguiente comando:

&#x20;`chgrp alumnos iptables.sh`

&#x20;Vuelvo a ejecutar `ls -l` y el resultado debe ser el siguiente:

&#x20;`-rw-r–rwx javier alumnos 4566 mar 24 06:21 iptables.sh`
