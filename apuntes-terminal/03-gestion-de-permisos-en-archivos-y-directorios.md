---
description: Comandos para la gestión de permisos de recursos en ambientes Linux.
---

# 03- GESTIÓN DE PERMISOS EN ARCHIVOS Y DIRECTORIOS

##  **INFORMACION BASICA**

 Cuando usamos la opción -l en el comando ls para listar `ls -l`, mostrará el contenido de  
la carpeta en la que nos encontramos, o la que se indique en el comando, por ejemplo:  
`ls -l /root/Desktop`

 **`-rw-r–rwx root root 4566 mar 24 06:21 iptables.sh`**

 El resultado mostrado, dará información importante. Lo primero que nos encontramos,  
son un conjunto de 10 caracteres:

 `-rw-r–rwx`

* El primero elemento nos indica si es un archivo o una carpeta. En este caso al ser un guión \(-\), sabemos que es un archivo. Si este paquete fuese \(d\) nos indicaría que es una carpeta, pudiendo acceder con el comando cd.
* El segundo paquete \(rw-\): Esto nos dice que permisos tiene el propietario de este archivo, en este caso r y w, es decir de lectura y escritura. No de ejecución, ya que en vez de tener una \(x\) en su último caracter, tiene un guión -.
* Tercer paquete \(r–\): Son los permisos, NO del usuario propietario, si no del grupo propietario. En este caso, todos los miembros del grupo propietario tienen solo permiso de r \(read\) o lectura, no de \(w\), ni de \(x\), es decir, no pueden escribir, ni ejecutar este archivo.
* Cuarto paquete\(rwx\): Nos dice que todos los usuarios, que NO sean el propietario \(segundo paquete\), ni sean miembros del grupo de propietarios \(tercer paquete\), tienen permiso de r \(lectura\), de w \(escritura\) y de x \(ejecución\).

{% hint style="info" %}
 Estos permisos pueden tener unos bits especiales en ejecucion:

 drwxrwxrwx --&gt; esto es lo normal  
---s------ --&gt; **SUID** \(todos los usuarios lo pueden ejecutar como propietario\)  
------s--- --&gt; **SGID** \(todo lo que entra en el directorio hereda el grupo propietario\)  
---------t --&gt; **STICKY** \(evita que los archivos sean borrados por usuarios no propietarios INCLUSO ROOT\)
{% endhint %}

 Nos encontramos datos numéricos como su tamaño, fecha y hora. Finalmente el nombre del  
archivo, pero lo que quiero explicar es que son esas palabras: root root

* El primer **root**, es el usuario propietario, correspondiente al segundo paquete \(rw-\)
* El segundo **root**, es el grupo \(no usuario\) propietario, perteneciente a los permisos del tercer paquete \(r–\)

##  **FICHEROS RELEVANTES**

 **/home/strelock/.profile** --&gt; fichero oculto que contiene toda la informacion del usuario ricardo.  
 en este fichero se almacena la umask de cada usuario:

{% hint style="info" %}
umask 022 \(equivale a permisos 755 predeterminados\)   
Representa la diferencia entre los permisos maximos \(777 para directorio o 666 para archivo\)   
y los permisos predeterminados al crearlo.   
Se puede modificar para cada usuario. 
{% endhint %}

 **/home/strelock/.bashrc** --&gt; fichero oculto que contiene toda la configuracion del usuario ricardo

##  **COMANDOS**

 **UMASK** --&gt; permite cambiar la mascara de permisos.

 **CHMOD** --&gt; Change mode \(nos permite cambiar los permisos de un archivo o directorio\)  
 `-R` --&gt; Cambia los permisos de todos los archivos contenidos en una carpeta.

 P.E. \(octal\)--&gt; `sudo chmod 037 /home/username/Escritorio/prueba.txt`

 **OCTAL**: Los permisos se dan con números del 0 al 7  
**0** --&gt; - - -  
**1** --&gt; - - x \(permiso de ejecución\)  
**2** --&gt; - w - \(permiso de escritura\)  
**3** --&gt; - w x   
**4** --&gt; r - - \(permiso de lectura\)   
**5** --&gt; r - x   
**6** --&gt; r w -   
**7** --&gt; r w x

  
 3 grupos de permisos: 

1. Primer número para el creador.
2. Segundo número para el grupo.
3. Tercer número para el resto.

 **CARACTER**: Los permisos se cambian usando 3 modificadores:

1. **u** \(user\) **g** \(group\) **o** \(other\) **a** \(all\)
2. **+** **-** **=** \(añadir, eliminar o igualar\)
3. **r** **w** **x** \(tipo de permiso\)

P.E.  `sudo chmod u=+x /home/username/Escritorio/prueba.txt`

###  **EJEMPLO**

 Si quisiera cambiar el usuario propietario, a otro usuario existente, por ejemplo  
javier, usaría el comando:

 `chown javier iptables.sh`

 Dando un `ls -l` aparecería lo siguiente:

 `-rw-r–rwx javier root 4566 mar 24 06:21 iptables.sh`

 Si ahora además quiero cambiar el grupo propietario por ejemplo a alumnos \(debe existir  
o ser creado antes\), uso el siguiente comando:

 `chgrp alumnos iptables.sh`

 Vuelvo a ejecutar `ls -l` y el resultado debe ser el siguiente:

 `-rw-r–rwx javier alumnos 4566 mar 24 06:21 iptables.sh`

