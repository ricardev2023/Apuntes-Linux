---
description: >-
  Comandos para la instalación de paquetes en diferentes formatos en ambientes
  Linux.
---

# 04- INSTALACIÓN DE PAQUETES

## **DEFINICIONES**

**PAQUETE** --&gt; conjunto de ficheros que forman un programa.

**FICHERO** --&gt; unidad de instalacion basica.

**DEPENDENCIAS** --&gt; algunos paquetes dependen de otros para funcionar, al instalar uno, normalmente  
 se instalan tambien sus dependencias.

**DEPENDENCIAS HUERFANAS -**-&gt; Si desinstalamos mal una aplicación pueden quedar dependencias  
 inservibles que es recomendable eliminar.

## **APT-GET**

**APT-GET** --&gt; Advance Packaging Tool. Permite utilizar comandos para la administración de paquetes.  
 P.E.--&gt; `sudo apt install nombre_programa #siempre con privilegios de superusuario.`

{% hint style="info" %}
`En las nuevas versiones, el  gestor de paquetes se llama directamente con "apt" y no con "apt-get" que se encuentra deprecated.`
{% endhint %}

 **UPDATE** --&gt; actualiza repositorios

 **UPGRADE** --&gt; actualiza los paquetes no criticos

 **DIST-UPGRADE** --&gt; actualiza TODOS los paquetes de la distribucion

 **FULL-UPGRADE** --&gt; lo mismo que el anterior

 **INSTALL** --&gt; permite instalar nuevos paquetes o librerias siempre que esté en el  
 repositorio activo

 **REMOVE** --&gt; desinstala un paquete

 **PURGE** --&gt; elimina tambien los archivos de configuración.

 **AUTOREMOVE** --&gt; elimina dependencias huerfanas.

 **CLEAN** --&gt; limpia la cache de paquetes instalados.

**APT-CACHE** --&gt; muestra informacion sobre los paquetes que se encuentran en el repositorio

 showrc --&gt; muestra las fuentes  
 search --&gt; busca en el repositorio paquetes relacionados  
 P.E: apt-cache search "Web" \(buscara todo lo que tenga que ver con la web\)  
 depends --&gt; muestra las dependencias del paquete \(rdepends inversas\)  
 show --&gt; muestra la descripcion del paquete  
 pkgnames --&gt; muestra nombre del paquete  
 policy --&gt; muestra parametros de las normas  
 stats --&gt; muestra estadísticas de la cache.  
 unmet --&gt; muestra dependencias incumplidas

**DSELECT** --&gt; Paquete de entorno gráfico para APT. Requiere instalación.

**APTITUDE** --&gt; APT pero mejorado. Gestiona mejor las dependencias.  
 tiene las mismas opciones que APT

**SYNAPTIC** --&gt; APT con entorno grafico. Requiere instalación.

## **DPKG**

**DPKG** --&gt; Programa que permite instalar paquetes .deb \(arquitectura debian\)

 `-i` --&gt; instalar paquetes  
 P.E. `dpkg -i *.deb #instalara todos los paquetes .deb en la carpeta en uso.`  
 `-l` --&gt; lista paquetes .deb instalados  
 P.E. `dpkg -l thunderbird #sin .deb comprueba si está instalado`  
 `-r` --&gt; desinstala paquetes .deb instalados  
 P.E. `dpkg -r thunderbird #sin .deb desintala el programa`  
 `-P` --&gt; purgar. Elimina los archivos de configuración despues de desinstalar  
 `-L` --&gt; lista todos los ficheros de un paquete.  
 `-S` --&gt; lista los paquetes a los que esta asociado un determinado fichero  
 `-V` --&gt; verifica la integridad del paquete.  
 `--info` --&gt; da información del paquete  
 `--reconfigure` --&gt; permite reconfigurar el gestor de paquetes si ha dejado de funcionar

## **YUM**

Yellow Dog Update Modified. \(mejora de la instalacion de RPM\)

 **CHECK-UPDATE** --&gt; actualiza los repositorios \(eq APT-GET UPDATE\)

 **UPDATE** --&gt; actualiza los paquetes no criticos \(eq APT-GET UPGRADE\)

 **UPGRADE** --&gt; actualiza TODOS los paquetes \(eq APT-GET DIST-UPGRADE\)

 **SEARCH** --&gt; busca un paquete en los repositorios \(eq APT-CACHE SEARCH\)

 **INFO** --&gt; muestra informacion de un paquete \(eq APT-GET SHOW\)

 **INSTALL** --&gt; instala un paquete \(eq APT-GET INSTALL\)

 **ERASE** --&gt; desinstala un paquete \(eq APT-GET REMOVE\)

**YUMDOWNLOADER** --&gt; Programa que permite descargar paquetes rpm  
 No los instala, solo los descarga  
 Se obtiene instalando yum-utils

**/etc/yum.conf** --&gt; archivo de configuracion de yum  
**/etc/ym.repos.d** --&gt; directorio con los repositorios de yum  
**/var/log/yum.log** --&gt; log de eventos de yum

## **RPM**

Red Hat Package Manager \(gestor en Fedora, Red Hat, CentOS, etc\)

 Parametros  
 `-q` --&gt; Query \(comprueba los paquetes existentes\)  
 Opciones generales  
 `-a` --&gt; all. Todos los paquetes ¿de la base de datos rpm?  
 `-f` --&gt; file. Encuentra el paquete de un archivo indicado  
 `-g` --&gt; group. Paquetes que tienen un grupo  
 `-p` --&gt; package. Paquete no instalados \(con nombre concreto\)

* Opciones especificas \(van acompañando a las opciones generales\)  `--changelog` --&gt; log de cambio de versiones  `-c` --&gt; archivos de configuracion que usa el paquete  `-i` --&gt; muestra información del paquete  `-l` --&gt; lista los paquetes instalados \(con -p no funciona\)  `-s` --&gt; estado de los archivos o directorios  `-R` --&gt; muestra las dependencias

 `-V` --&gt; Verify \(si esta descargado, nos dirá el estado del archivo .rpm\)

* Opciones generales \(las misma que -q\)
* Opciones especificas  `-nodeps` --&gt; no verifica dependencias  `-nofiles` --&gt; no verifica atributos del archivo  `-nomtime` --&gt; no verifica cambio de modificacion  `-nosize` --&gt; no verifica cambio de tamaño  `-nouser` --&gt; no veridica cambio de usuarios  `-nordev` --&gt; no verifica correspondencia de los atributos

 `-i` --&gt; instala el paquete  
 `--allfiles` --&gt; instala los paquetes que faltan  
 `--excludedocs` --&gt; instala sin archivos de documentación  
 `--force` --&gt; fuerza la instalación o actualizacion  
 `--hash (-h)` --&gt; imprime los hashes

 `-U` --&gt; actualiza y si no esta el paquete, lo instala  
 `--ignoresize` --&gt; ignora el tamaño disponible en destino  
 `--ignorearch` --&gt; ignora la arquitectura en destino  
 `--ignoreos` --&gt; ignora Sist. Op. en destino  
 `--includedocs` --&gt; instala archivos de documentacion

 `-F` --&gt; actualiza y si no esta el paquete, NO lo instala  
 `--justdb` --&gt; solo actualiza la base de datos  
 `--nodigest` --&gt; ignora digest  
 `--nosignature` --&gt; ignora la firma del paquete  
 `--nodeps` --&gt; evita problemas con dependencias  
 `--noorder` --&gt; no reordena la lista de paquetes  
 `--noplugins` --&gt; no ejecuta ni carga plugins  
 `--oldpackage` --&gt; version anterior  
 `--percent` --&gt; muesta porcentaje  
 `--test` --&gt; realiza un test sin instalar  
 `-e` --&gt; elimina un paquete

 Salidas en Verificar

 **S** --&gt; tamaño cambiado  
 **M** --&gt; permisos cambiados  
 **5** --&gt; Digest MD5 cambiado  
 **D** --&gt; modificación del archivo  
 **L** --&gt; cambios de enlaces  
 **U** --&gt; usuario propietario modificado  
 **G** --&gt; grupo propietario modificado  
 **T** --&gt; fecha modificacion alterada  
 **P** --&gt; capacidades modificadas

 **c** --&gt; archivo de configuracion  
 **d** --&gt; archivo de documentacion  
 **g** --&gt; archivo con contenido no incluido en el paquete  
 **l** --&gt; archivo de licencia  
 **r** --&gt; archivo de texto

**/var/lib/rpm** --&gt; base de datos de aplicaciones .rpm

**ALIEN** --&gt; \(Programa que permite ejecutar paquetes .rpm\) \*Es posible que requiera instalación\*

## **TAR**

Permite trabajar con archivos comprimidos .tar

 `-c` --&gt; crear un fichero  
 `-f` --&gt; especificar la ruta  
 `-v` --&gt; modo verbose  
 `-x` --&gt; extraer fichero  
 `-z` --&gt; comprime o descomprime en gzip \(.gz\)  
 `-j` --&gt; comprime o descomprime en bzip2 \(.bz2\)  
 `-J` --&gt; comprime o descomprime en xz \(.xz\)  
 `-t` --&gt; lista los archivos que se encuentran dentro del comprimido.  
 P.E:  
 `tar -cvf [ruta del contenedor creado] [ruta de archivos que van dentro del contenedor]`  
 crea un contenedor .tar con los archivos de la ruta seleccionada  
 `tar -zcvf [ruta del contenedor creado] [ruta de archivos que van dentro del contenedor]`  
 crea in contenedor .tar.gz comprimido con los archivos seleccionados.

**GUNZIP** --&gt; Descomprime un archivo .gz

**MAKE** --&gt; \(Compila un programa\)

## **DESCARGAR DE GITHUB**

Se pueden descargar aplicaciones desde GITHUB en binarios lo que permite instalarlas en el entorno LINUX.  
Para ello, puedo descargarla directamente de la web y si no, puede utilizar el comando:

`git clone [ruta web]`

Despues de descargarlo debemos leer el archivo README.md donde se explican los pasos a seguir para la instalacion y configuración del programa.

Normalmente habrá un archivo llamado configure, para las configuraciones previas a la instalacion

Despues, tendremos el archivo INSTALL.sh

Para compilar los archivos necesarios del programa, empezamos con el comando make. Este comando lista los archivos a compilar y los compila de uno en uno.

