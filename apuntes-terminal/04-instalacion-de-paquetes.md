---
description: >-
  Comandos para la instalación de paquetes en diferentes formatos en ambientes
  Linux.
---

# 04- INSTALACIÓN DE PAQUETES

## **DEFINICIONES**

**PAQUETE** --> conjunto de ficheros que forman un programa.

**FICHERO** --> unidad de instalacion basica.

**DEPENDENCIAS** --> algunos paquetes dependen de otros para funcionar, al instalar uno, normalmente\
&#x20;se instalan tambien sus dependencias.

**DEPENDENCIAS HUERFANAS -**-> Si desinstalamos mal una aplicación pueden quedar dependencias\
&#x20;inservibles que es recomendable eliminar.

## **APT-GET**

**APT-GET** --> Advance Packaging Tool. Permite utilizar comandos para la administración de paquetes.\
&#x20;P.E.--> `sudo apt install nombre_programa #siempre con privilegios de superusuario.`

{% hint style="info" %}
`En las nuevas versiones, el  gestor de paquetes se llama directamente con "apt" y no con "apt-get" que se encuentra deprecated.`
{% endhint %}

&#x20;**UPDATE** --> actualiza repositorios

&#x20;**UPGRADE** --> actualiza los paquetes no criticos

&#x20;**DIST-UPGRADE** --> actualiza TODOS los paquetes de la distribucion

&#x20;**FULL-UPGRADE** --> lo mismo que el anterior

&#x20;**INSTALL** --> permite instalar nuevos paquetes o librerias siempre que esté en el\
&#x20;repositorio activo

&#x20;**REMOVE** --> desinstala un paquete

&#x20;**PURGE** --> elimina tambien los archivos de configuración.

&#x20;**AUTOREMOVE** --> elimina dependencias huerfanas.

&#x20;**CLEAN** --> limpia la cache de paquetes instalados.

**APT-CACHE** --> muestra informacion sobre los paquetes que se encuentran en el repositorio

&#x20;showrc --> muestra las fuentes\
&#x20;search --> busca en el repositorio paquetes relacionados\
&#x20;P.E: apt-cache search "Web" (buscara todo lo que tenga que ver con la web)\
&#x20;depends --> muestra las dependencias del paquete (rdepends inversas)\
&#x20;show --> muestra la descripcion del paquete\
&#x20;pkgnames --> muestra nombre del paquete\
&#x20;policy --> muestra parametros de las normas\
&#x20;stats --> muestra estadísticas de la cache.\
&#x20;unmet --> muestra dependencias incumplidas

**DSELECT** --> Paquete de entorno gráfico para APT. Requiere instalación.

**APTITUDE** --> APT pero mejorado. Gestiona mejor las dependencias.\
&#x20;tiene las mismas opciones que APT

**SYNAPTIC** --> APT con entorno grafico. Requiere instalación.

## **DPKG**

**DPKG** --> Programa que permite instalar paquetes .deb (arquitectura debian)

&#x20;`-i` --> instalar paquetes\
&#x20;P.E. `dpkg -i *.deb #instalara todos los paquetes .deb en la carpeta en uso.`\
&#x20;`-l` --> lista paquetes .deb instalados\
&#x20;P.E. `dpkg -l thunderbird #sin .deb comprueba si está instalado`\
&#x20;`-r` --> desinstala paquetes .deb instalados\
&#x20;P.E. `dpkg -r thunderbird #sin .deb desintala el programa`\
&#x20;`-P` --> purgar. Elimina los archivos de configuración despues de desinstalar\
&#x20;`-L` --> lista todos los ficheros de un paquete.\
&#x20;`-S` --> lista los paquetes a los que esta asociado un determinado fichero\
&#x20;`-V` --> verifica la integridad del paquete.\
&#x20;`--info` --> da información del paquete\
&#x20;`--reconfigure` --> permite reconfigurar el gestor de paquetes si ha dejado de funcionar

## **YUM**

Yellow Dog Update Modified. (mejora de la instalacion de RPM)

&#x20;**CHECK-UPDATE** --> actualiza los repositorios (eq APT-GET UPDATE)

&#x20;**UPDATE** --> actualiza los paquetes no criticos (eq APT-GET UPGRADE)

&#x20;**UPGRADE** --> actualiza TODOS los paquetes (eq APT-GET DIST-UPGRADE)

&#x20;**SEARCH** --> busca un paquete en los repositorios (eq APT-CACHE SEARCH)

&#x20;**INFO** --> muestra informacion de un paquete (eq APT-GET SHOW)

&#x20;**INSTALL** --> instala un paquete (eq APT-GET INSTALL)

&#x20;**ERASE** --> desinstala un paquete (eq APT-GET REMOVE)

**YUMDOWNLOADER** --> Programa que permite descargar paquetes rpm\
&#x20;No los instala, solo los descarga\
&#x20;Se obtiene instalando yum-utils

**/etc/yum.conf** --> archivo de configuracion de yum\
**/etc/ym.repos.d** --> directorio con los repositorios de yum\
**/var/log/yum.log** --> log de eventos de yum

## **RPM**

Red Hat Package Manager (gestor en Fedora, Red Hat, CentOS, etc)

&#x20;Parametros\
&#x20;`-q` --> Query (comprueba los paquetes existentes)\
&#x20;Opciones generales\
&#x20;`-a` --> all. Todos los paquetes ¿de la base de datos rpm?\
&#x20;`-f` --> file. Encuentra el paquete de un archivo indicado\
&#x20;`-g` --> group. Paquetes que tienen un grupo\
&#x20;`-p` --> package. Paquete no instalados (con nombre concreto)

* Opciones especificas (van acompañando a las opciones generales)\
  &#x20;`--changelog` --> log de cambio de versiones\
  &#x20;`-c` --> archivos de configuracion que usa el paquete\
  &#x20;`-i` --> muestra información del paquete\
  &#x20;`-l` --> lista los paquetes instalados (con -p no funciona)\
  &#x20;`-s` --> estado de los archivos o directorios\
  &#x20;`-R` --> muestra las dependencias

&#x20;`-V` --> Verify (si esta descargado, nos dirá el estado del archivo .rpm)

* Opciones generales (las misma que -q)
* Opciones especificas\
  &#x20;`-nodeps` --> no verifica dependencias\
  &#x20;`-nofiles` --> no verifica atributos del archivo\
  &#x20;`-nomtime` --> no verifica cambio de modificacion\
  &#x20;`-nosize` --> no verifica cambio de tamaño\
  &#x20;`-nouser` --> no veridica cambio de usuarios\
  &#x20;`-nordev` --> no verifica correspondencia de los atributos

&#x20;`-i` --> instala el paquete\
&#x20;`--allfiles` --> instala los paquetes que faltan\
&#x20;`--excludedocs` --> instala sin archivos de documentación\
&#x20;`--force` --> fuerza la instalación o actualizacion\
&#x20;`--hash (-h)` --> imprime los hashes

&#x20;`-U` --> actualiza y si no esta el paquete, lo instala\
&#x20;`--ignoresize` --> ignora el tamaño disponible en destino\
&#x20;`--ignorearch` --> ignora la arquitectura en destino\
&#x20;`--ignoreos` --> ignora Sist. Op. en destino\
&#x20;`--includedocs` --> instala archivos de documentacion

&#x20;`-F` --> actualiza y si no esta el paquete, NO lo instala\
&#x20;`--justdb` --> solo actualiza la base de datos\
&#x20;`--nodigest` --> ignora digest\
&#x20;`--nosignature` --> ignora la firma del paquete\
&#x20;`--nodeps` --> evita problemas con dependencias\
&#x20;`--noorder` --> no reordena la lista de paquetes\
&#x20;`--noplugins` --> no ejecuta ni carga plugins\
&#x20;`--oldpackage` --> version anterior\
&#x20;`--percent` --> muesta porcentaje\
&#x20;`--test` --> realiza un test sin instalar\
&#x20;`-e` --> elimina un paquete

&#x20;Salidas en Verificar

&#x20;**S** --> tamaño cambiado\
&#x20;**M** --> permisos cambiados\
&#x20;**5** --> Digest MD5 cambiado\
&#x20;**D** --> modificación del archivo\
&#x20;**L** --> cambios de enlaces\
&#x20;**U** --> usuario propietario modificado\
&#x20;**G** --> grupo propietario modificado\
&#x20;**T** --> fecha modificacion alterada\
&#x20;**P** --> capacidades modificadas

&#x20;**c** --> archivo de configuracion\
&#x20;**d** --> archivo de documentacion\
&#x20;**g** --> archivo con contenido no incluido en el paquete\
&#x20;**l** --> archivo de licencia\
&#x20;**r** --> archivo de texto

**/var/lib/rpm** --> base de datos de aplicaciones .rpm

**ALIEN** --> (Programa que permite ejecutar paquetes .rpm) \*Es posible que requiera instalación\*

## **TAR**

Permite trabajar con archivos comprimidos .tar

&#x20;`-c` --> crear un fichero\
&#x20;`-f` --> especificar la ruta\
&#x20;`-v` --> modo verbose\
&#x20;`-x` --> extraer fichero\
&#x20;`-z` --> comprime o descomprime en gzip (.gz)\
&#x20;`-j` --> comprime o descomprime en bzip2 (.bz2)\
&#x20;`-J` --> comprime o descomprime en xz (.xz)\
&#x20;`-t` --> lista los archivos que se encuentran dentro del comprimido.\
&#x20;P.E:\
&#x20;`tar -cvf [ruta del contenedor creado] [ruta de archivos que van dentro del contenedor]`\
&#x20;crea un contenedor .tar con los archivos de la ruta seleccionada\
&#x20;`tar -zcvf [ruta del contenedor creado] [ruta de archivos que van dentro del contenedor]`\
&#x20;crea in contenedor .tar.gz comprimido con los archivos seleccionados.

**GUNZIP** --> Descomprime un archivo .gz

**MAKE** --> (Compila un programa)

## **DESCARGAR DE GITHUB**

Se pueden descargar aplicaciones desde GITHUB en binarios lo que permite instalarlas en el entorno LINUX.\
Para ello, puedo descargarla directamente de la web y si no, puede utilizar el comando:

`git clone [ruta web]`

Despues de descargarlo debemos leer el archivo README.md donde se explican los pasos a seguir para la instalacion y configuración del programa.

Normalmente habrá un archivo llamado configure, para las configuraciones previas a la instalacion

Despues, tendremos el archivo INSTALL.sh

Para compilar los archivos necesarios del programa, empezamos con el comando make. Este comando lista los archivos a compilar y los compila de uno en uno.
