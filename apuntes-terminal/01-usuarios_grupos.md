---
description: Comandos para la gestión de usuarios y grupos en ambientes Linux.
---

# 01- GESTIÓN DE USUARIOS Y GRUPOS

## **INFORMACION GENERAL**

\- Los nombres no deben empezar por numero\
\- Los nombres no deben tener espacios\
\- Linux diferencia entre mayuscula y minuscula

## **FICHEROS IMPORTANTES**

**/etc/group** --> muestra la informacion de los grupos:

&#x20;`grupo1:x:1002:usuario1,usuario2`\
`nombre_grupo:contraseña:identificador_GID:usuarios_pertenecientes`

**/etc/passwd** --> muestra la informacion de los usuarios:

&#x20;`ricardo:x:1001:1001:,,,:/home/ricardo:/bin/bash`\
`nombre_usuario:contraseña:UID:GID:datos_personales:directorio_usuario:shell`

**/etc/shadow** --> amplia informacion de los usuarios

```
ricardo:$6$78Q043V(continua):18436:0:99999:7:::

nombre_usuario:contraseña_cifrada:dias_desde_1ENE1970_hasta_ultimo_cambio_contraseña:
minimo_dias_entre_cambios_contraseña:max_dias_validez_cuenta:
aviso_dias_antes_cad_contraseña:dias_antes_deshab_cuenta_si_cad_contraseña:
fecha_cad_cuenta_en_dias_desde_1ENE1970
```

**/etc/gshadow** --> amplia informacion de los grupos

&#x20;`grupo1:!::usuario1,usuario2`\
`nombre_grupo:contraseña_cifrada:usuarios_admin:usuarios_pertenecientes`

**/etc/sudoers** --> incluye todos los usuarios con capacidad de superdo.

## **COMANDOS**

**ADDUSER** --> Añadir Usuario (crea un nuevo usuario con todos sus datos)\
&#x20;No se puede configurar el usuario desde cero, vienen algunos campos predefinidos.\
&#x20;`-ingroup` --> introduce al usuario nuevo directamente en un grupo\
&#x20;`--add_extra_groups` --> lo mismo pero en mas grupos\
&#x20;P.E: `adduser --ingroup admin --add_extra_groups laboral`

**USERADD** --> (crea un usuario sin pedir ningún dato extra)\
&#x20;Tiene muchas opciones para configurar completamente el ususario creado.\
&#x20;Para scripts es mas usado por que puede configurarse desde cero el usuario\
&#x20;`-d` --> carpeta home\
&#x20;`-c` --> comentario\
&#x20;`-e` --> fecha en la que el usuario expira\
&#x20;`-g` --> grupo\
&#x20;`-G` --> grupos (separados con comas)\
&#x20;`-p` --> contraseña\
&#x20;`-s` --> elige la shell\
&#x20;`-U` --> añade al usuario a un grupo con su nombre\
&#x20;`-u` --> selecciona el uid para el usuario

**GROUPADD** --> Añadir grupo (crea un grupo de usuarios)\
&#x20;P.E: `groupadd -p "password" grupo5`

**NEWGRP** --> Cambia el grupo activo en la sesion

**USERMOD** --> Modifica las características de un usuario\
`-a -G` --> sirve para añadir (-a) el usuario a un grupo (-G)\
&#x20;P.E: `usermod -a -G test User1 #primero grupo y luego usuario)`

**GROUPMOD** --> Modifica las caracteristicas de un grupo

**USERDEL** --> Eliminar Usuario.

**GROUPDEL** --> Eliminar Grupo, sin eliminar los usuarios.

**PASSWD** --> cambia la contraseña de un usuario

**GPASSWD** --> gestiona las contraseñas de los grupos\
&#x20;permite establecer la lista de administradores de Grupo.&#x20;

`gpasswd -A [usuario_admin] [grupo]`

**CHAGE** --> permite cambiar las politicas de los usuarios (la info del /etc/passwd)\
&#x20;`-d` --> Establece el dia del ultimo dia que se cambio la contraseña desde 1ENE1970\
&#x20;`-E` --> Establece la fecha de caducidad del usuario con la misma premisa que -d\
&#x20;`-I` --> Establece los dias que debe estar una cuenta inactiva para que se deshabilite\
&#x20;`-l` --> Muestra la informacion de la edad de la cuenta\
&#x20;`-m` --> Establece el numero minimo de dias antes de volver a cambiar la contraseña.\
&#x20;`-M` --> Establece el numero maximo de dias\
&#x20;`-W` --> Establece los dias que el sistema avisara al usuario antes de la expiracion de contraseña.

&#x20;Si el root pone (chage -d 0 usuario1) el usuario debe cambiarla la proxima vez que se conecte.

**PWCK** --> comprueba la integridad del archivo passwd y el shadow.

**GRPCK** --> comprueba la integridad de groups y gshadow.

**WHOAMI** --> indica qué usuario estamos utilizando

**GROUPS** --> (muestra los grupos a los que pertenece el usuario)

**ID** --> imprime los ID de ususario y grupo reales y efectivos\
&#x20;si se busca un usuario concreto imprime dicha informacion

**W** --> Muestra por pantalla usuarios logueados con informacion sobre que hacen

\
&#x20;**USER** --> que usuario es\
&#x20;**TTY** --> es la estacion\
&#x20;**FROM** -->\
&#x20;**LOGIN** --> a que hora se ha logueado\
&#x20;**IDLE** --> tiempo que lleva disponible\
&#x20;**JCPU** --> Tiempo de uso de CPU\
&#x20;**PCPU** --> Tiempo de proceso actual\
&#x20;**WHAT** --> que esta haciendo (coincide con los procesos activos)

&#x20;`-s` --> muestra solo USER TTY FROM WHAT\
&#x20;`-i` --> muestra la direccion IP en vez de FROM\
&#x20;`-v` --> muestra la informacion de la version\
&#x20;`-user` --> muestra informacion sobre un usuario concreto

**WHO** --> Muestra por pantalla usuarios logueados y desde cuando.

**LAST** --> Muestra un listado de los usuarios que se han logueado ultimamente

**CHOWN** --> Change owner (permite cambiar el usuario propietario a otro existente)\
&#x20;P.E: `chown usuario1:grupo1 hola.txt #tambien cambia el grupo en el ejemplo`

**CHGRP** --> Change group (permite cambiar el grupo propietario a otro existente)\
&#x20;P.E: `chgrp grupo2 hola.txt`
