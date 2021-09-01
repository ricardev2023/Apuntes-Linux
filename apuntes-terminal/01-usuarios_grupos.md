---
description: Comandos para la gestión de usuarios y grupos en ambientes Linux.
---

# 01- GESTIÓN DE USUARIOS Y GRUPOS

## **INFORMACION GENERAL**

- Los nombres no deben empezar por numero  
- Los nombres no deben tener espacios  
- Linux diferencia entre mayuscula y minuscula

## **FICHEROS IMPORTANTES**

**/etc/group** --&gt; muestra la informacion de los grupos:

 `grupo1:x:1002:usuario1,usuario2  
nombre_grupo:contraseña:identificador_GID:usuarios_pertenecientes`

**/etc/passwd** --&gt; muestra la informacion de los usuarios:

 ****`ricardo:x:1001:1001:,,,:/home/ricardo:/bin/bash  
nombre_usuario:contraseña:UID:GID:datos_personales:directorio_usuario:shell`

**/etc/shadow** --&gt; amplia informacion de los usuarios

```text
ricardo:$6$78Q043V(continua):18436:0:99999:7:::

nombre_usuario:contraseña_cifrada:dias_desde_1ENE1970_hasta_ultimo_cambio_contraseña:
minimo_dias_entre_cambios_contraseña:max_dias_validez_cuenta:
aviso_dias_antes_cad_contraseña:dias_antes_deshab_cuenta_si_cad_contraseña:
fecha_cad_cuenta_en_dias_desde_1ENE1970
```

**/etc/gshadow** --&gt; amplia informacion de los grupos

 `grupo1:!::usuario1,usuario2  
nombre_grupo:contraseña_cifrada:usuarios_admin:usuarios_pertenecientes`

**/etc/sudoers** --&gt; incluye todos los usuarios con capacidad de superdo.

## **COMANDOS**

**ADDUSER** --&gt; Añadir Usuario \(crea un nuevo usuario con todos sus datos\)  
 No se puede configurar el usuario desde cero, vienen algunos campos predefinidos.  
 `-ingroup` --&gt; introduce al usuario nuevo directamente en un grupo  
 `--add_extra_groups` --&gt; lo mismo pero en mas grupos  
 P.E: `adduser --ingroup admin --add_extra_groups laboral`

**USERADD** --&gt; \(crea un usuario sin pedir ningún dato extra\)  
 Tiene muchas opciones para configurar completamente el ususario creado.  
 Para scripts es mas usado por que puede configurarse desde cero el usuario  
 `-d` --&gt; carpeta home  
 `-c` --&gt; comentario  
 `-e` --&gt; fecha en la que el usuario expira  
 `-g` --&gt; grupo  
 `-G` --&gt; grupos \(separados con comas\)  
 `-p` --&gt; contraseña  
 `-s` --&gt; elige la shell  
 `-U` --&gt; añade al usuario a un grupo con su nombre  
 `-u` --&gt; selecciona el uid para el usuario

**GROUPADD** --&gt; Añadir grupo \(crea un grupo de usuarios\)  
 P.E: `groupadd -p "password" grupo5`

**NEWGRP** --&gt; Cambia el grupo activo en la sesion

**USERMOD** --&gt; Modifica las características de un usuario  
`-a -G` --&gt; sirve para añadir \(-a\) el usuario a un grupo \(-G\)  
 P.E: `usermod -a -G test User1 #primero grupo y luego usuario)`

**GROUPMOD** --&gt; Modifica las caracteristicas de un grupo

**USERDEL** --&gt; Eliminar Usuario.

**GROUPDEL** --&gt; Eliminar Grupo, sin eliminar los usuarios.

**PASSWD** --&gt; cambia la contraseña de un usuario

**GPASSWD** --&gt; gestiona las contraseñas de los grupos  
 permite establecer la lista de administradores de Grupo. 

`gpasswd -A [usuario_admin] [grupo]`

**CHAGE** --&gt; permite cambiar las politicas de los usuarios \(la info del /etc/passwd\)  
 `-d` --&gt; Establece el dia del ultimo dia que se cambio la contraseña desde 1ENE1970  
 `-E` --&gt; Establece la fecha de caducidad del usuario con la misma premisa que -d  
 `-I` --&gt; Establece los dias que debe estar una cuenta inactiva para que se deshabilite  
 `-l` --&gt; Muestra la informacion de la edad de la cuenta  
 `-m` --&gt; Establece el numero minimo de dias antes de volver a cambiar la contraseña.  
 `-M` --&gt; Establece el numero maximo de dias  
 `-W` --&gt; Establece los dias que el sistema avisara al usuario antes de la expiracion de contraseña.

 Si el root pone \(chage -d 0 usuario1\) el usuario debe cambiarla la proxima vez que se conecte.

**PWCK** --&gt; comprueba la integridad del archivo passwd y el shadow.

**GRPCK** --&gt; comprueba la integridad de groups y gshadow.

**WHOAMI** --&gt; indica qué usuario estamos utilizando

**GROUPS** --&gt; \(muestra los grupos a los que pertenece el usuario\)

**ID** --&gt; imprime los ID de ususario y grupo reales y efectivos  
 si se busca un usuario concreto imprime dicha informacion

**W** --&gt; Muestra por pantalla usuarios logueados con informacion sobre que hacen

  
 **USER** --&gt; que usuario es  
 **TTY** --&gt; es la estacion  
 **FROM** --&gt;  
 **LOGIN** --&gt; a que hora se ha logueado  
 **IDLE** --&gt; tiempo que lleva disponible  
 **JCPU** --&gt; Tiempo de uso de CPU  
 **PCPU** --&gt; Tiempo de proceso actual  
 **WHAT** --&gt; que esta haciendo \(coincide con los procesos activos\)

 `-s` --&gt; muestra solo USER TTY FROM WHAT  
 `-i` --&gt; muestra la direccion IP en vez de FROM  
 `-v` --&gt; muestra la informacion de la version  
 `-user` --&gt; muestra informacion sobre un usuario concreto

**WHO** --&gt; Muestra por pantalla usuarios logueados y desde cuando.

**LAST** --&gt; Muestra un listado de los usuarios que se han logueado ultimamente

**CHOWN** --&gt; Change owner \(permite cambiar el usuario propietario a otro existente\)  
 P.E: `chown usuario1:grupo1 hola.txt #tambien cambia el grupo en el ejemplo`

**CHGRP** --&gt; Change group \(permite cambiar el grupo propietario a otro existente\)  
 P.E: `chgrp grupo2 hola.txt`

