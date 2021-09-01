---
description: Comandos para la gestión de archivos y directorios en ambientes Linux.
---

# 02- GESTIÓN DE ARCHIVOS Y DIRECTORIOS

## TIPOS DE FICHEROS

  
 **-** --&gt; fichero regular  
 **d** --&gt; directorio  
 **l** --&gt; enlace  
 **c** --&gt; dispositivos especiales de caracteres  
 **p** --&gt; canales  
 **s** --&gt; shocket

## **COMANDOS**

**PWD** --&gt; Print Working Directory. Indica el directorio en el que estamos trabajando.

 **FILE** --&gt; Da informacion del tipo de archivo que hemos seleccionado.  
 P.E: `file /bin/sync`

 **LS** --&gt; List directory contents. Lista los elementos en el directorio.  
 `-l` --&gt; nos da más información sobre los archivos.  
 `-a` --&gt; incluye archivos y directorios ocultos.  
 `-R` --&gt; incluye los subdirectorios de cada directorio.

 **SORT** --&gt; Lista ordenadamente del contenido de los elementos de un directorio o una serie de archivos.  
 P.E: sort 1.txt 2.txt 3.txt  
 `-b` --&gt; ignora los espacios en blanco iniciales  
 `-d` --&gt; solo tiene en cuenta espacios y alfanumerico  
 `-f` --&gt; ignora mayusculas o minusculas  
 `-r` --&gt; saca el listado inverso

 **TREE** --&gt; Lista en forma de arbol los directorios y subdirectorios desde  
 el directorio en el que me encuentro, para abajo.

 **GREP** --&gt; Busqueda global. Busca una letra o palabra en el texto que sale por  
 pantalla. ---------&gt; BUSCAR MAN POR QUE TIENE MIL POSIBILIDADES.  
 `grep [opciones] [patron] [archivo]`  
 `-i` --&gt; no distingue entre mayusculas y minusculas  
 `-r` --&gt; busqueda recursiva \(busca en todos los archivos del directorio\)  
 `-c` --&gt; muestra cuantas lineas coinciden con el patron.  
 `-n` --&gt; añade el numero de linea delante.  
 `-v` --&gt; muestra por pantalla las lineas del documento que no coinciden con el texto buscado.  
 `-l` --&gt; muestra el nombre de los archivos que SI tienen coincidencias.  
 `-L` --&gt; muestra el nombre de los archios que NO tienen coincidencias.  
 `-o` --&gt; muestra solo las palabras que coinciden, no toda la linea \(util si busco varias palabras\).  
 `-q` --&gt; no muestra nada como salida \(util para escribir codigos como el P.E.2\)

  
 P.E.1 --&gt; `grep -i comando /Desktop/01_Guias/Terminal/00_Guia_Basicos`  
 \(muestra por pantalla el texto de las lineas del documento que incluyen la palabra comando\).

  
 P.E.2 --&gt;`grep -ir comando /Desktop/ && echo SI || echo NO`  
 \(muestra por pantalla \(SI y las lineas de texto que lo incluyen\) si en alguno de los documentos de texto del directorio Desktop aparece la palabra comando \(sin tener en cuenta mayusculas o minusculas\). En caso contrario imprime \(NO\).

 **EGREP** --&gt; Busqueda extendida  
 `egrep 'auto|iface|comando' /etc/network/interfaces #me busca las lineas que tienen cada una de las palabras`

 **FIND** --&gt; Encontrar. Busca un archivo en el sistema.  
 `find [directorio inicio][opciones][que buscar]`  
 P.E. --&gt;`find / -iname "nombre de archivo"`  
 **/** --&gt; significa empezar a buscar en la raiz \(~ sirve para buscar en home\)  
 `-name` --&gt; busca por nombre  
 `-iname` --&gt; busca por nombre sin tener en cuenta mayus  
 `-user` --&gt; busca por usuario propietario  
 `-group` --&gt; busca por grupo propietario  
 `-type` --&gt; busca por tipo de archivo \(según los tipos de este tema\)  
 `-amin` --&gt; archivos modificados en los ultimos \[-amin 3\] minutos  
 `-atime` --&gt; archivos modificados en los ultimo \[-atime 10\] dias  
 `-syze` --&gt; busca por tamaño  
 `!`--&gt; NOT. Busca lo contrario de lo que se pone en la opcion de despues. Un ! por opcion.

 **LOCATE** --&gt; Encontrar ficheros en el sistema. Necesita tener una base de datos actualizada.  
 `updatedb` --&gt; actualiza la base de datos del sistema para usarla en locate.  
 `locate [que buscar]` --&gt; busca en todo el sistema muy rapido.  
 `-i` --&gt; no distingue entre mayusculas y minusculas.

 **WHEREIS** --&gt; Para ver la ruta de un archivo.  
 `-b` --&gt; nos muestra solo la ruta de archivos binarios.  
 `-m` --&gt; muestra la ruta de los manuales  
 `-s` --&gt; muestra la ruta de la fuente.

 **CD** --&gt; Change Directory. Cambia al directorio que seleccionemos  
 P.E.--&gt; `cd Escritorio/ #puedo utilizar tambien rutas absolutas`  
 `cd` --&gt; me manda directamente a la carpeta de usuario.  
 `cd ..` --&gt; me manda a la carpeta del nivel superior.

 **MKDIR** --&gt; Make Directory \(crea una carpeta en la ruta seleccionada\)  
 `-p` --&gt; permite crear un sistema de directorios

`-m` --&gt; permite añadir permisos al directorio

  
 P.E: `mkdir -p test/{test1,test2,test3/{test3.1,test3.2}}/`  
 genera el directorio test con test1,2 y 3 en su interior y test3.1 y 3.2 dentro de test3.

  
 P.E: `mkdir -m 550 test`  
 genera el directorio test con permisos de lectura y ejecución para usuario y grupo propietario.

 **RMDIR** --&gt; Remove Directory. Borra un directorio vacio.  
 `-p` --&gt; elimina carpetas y subcarpetas.

 **TOUCH** --&gt; Crea un archivo vacio en la ruta seleccionada.  
 Si el archivo ya existe le cambia la fecha de modificacion.

 **CP** --&gt; Copy. Copia el archivo en la ruta absoluta seleccionada.  
 P.E.--&gt; `cp prueba.txt /home/username/Escritorio`

 **DD** --&gt; Data Duplicator. Permite copiar de manera secuencial.  
 Se utiliza mucho en analisis forense. Es muy potente.  
 `dd if=$inputdata of=$outputdata [opciones]`  
 `bs= [tamaño de los paquetes]`  
 `count= [cantidad de bloques a copiar]`

 **MV** --&gt; Move. Mueve un archivo a la ruta absoluta seleccionada.

 **RM** --&gt; Remove. Elimina un archivo en la ruta seleccionada o en la carpeta actual.  
 `-r` --&gt; Si queremos borrar una carpeta no vacía.  
 `-f` --&gt; fuerza la accion.  
 `-i` --&gt; pregunta antes de ejecutar

 **SPLIT** --&gt; Permite dividir un paquete en archivos mas pequeños  
 `-a` --&gt; marca la longitud del sufijo  
 `-d` --&gt; utiliza sufijos numericos empezando en 0, no alfabeticos  
 `-c` --&gt; marca el tamaño maximo de los archivos de salida en BYTES.  
 `-l` --&gt; marca el tamaño maximo de los archivos de salida en LINEAS.  
 P.E: `split -d -c 20k imagen.iso`

 **CAT** --&gt; Concatenate. Muestra el contenido de un archivo.  
 `-n` --&gt; numera los renglones  
 `-b` --&gt; numera solo las lineas que no estaban en blanco  
 `-E` --&gt; marca el final de las lineas con $ \(util para programar\)  
 `-s` --&gt; muestra solo la primera linea en blanco si hay muchas.  
 `>` --&gt; permite dar contenido a un documento. \(termina con CTRL+D\)  
 `>>` --&gt; permite aumentar el contenido de un documento \(termina con CTRL+D\)

 **TAC** --&gt; Invierte la salida de CAT. \(la ultima linea pasa a ser la primera\).

 **NL** --&gt; Como cat pero numerando las lineas.

 **WC** --&gt; Da informacion del contenido de un fichero.  
 `N (Lineas) N (palabras) N (caracteres)`

 **-W** --&gt; cuenta solo las lineas.

 **DIFF** --&gt; Busca diferencias entre dos archivos.  
 P.E: `diff 1.txt 2.txt`

 `-b` --&gt; No hace caso de las diferencias por espacio en blanco  
 `-B` --&gt; No hace caso de las diferencias por lineas en blanco  
 `-q` --&gt; Solo informa de si difieren o no, sin mostrar los cambios  
 `-r` --&gt; Recursivo en directorios. Compara dos ficheros cualesquiera  
 `-y` --&gt; Emplea el formato de lado a lado.

 **UNIQ** --&gt; Muestra las lineas no repetidas de un conjunto de archivos.  
 `-c` --&gt; pone antes de cada linea el numero de coincidencias  
 `-d` --&gt; muestra las lineas repetidas solo una por duplicidad  
 `-D` --&gt; muestra TODAS las lineas duplicadas  
 `-i` --&gt; ignora diferencia entre mayus y minus  
 `-u` --&gt; muestra solo las lineas unicas

 **COLUMN** --&gt; Pone el contenido por columnas.  
 `-t` --&gt; utiliza los espacios como separadores  
 `-s` --&gt; Se utiliza con -t para utilizar otro separador que no sea el espacio  
 P.E: column -t -s ":"

 **CUT** --&gt; elimina secciones de cada fila de un fichero ------&gt; tiene muchas opciones. Ver man.  
 `-c [a,b,c]` --&gt; elimina solo las letras a, b y c.  
 `-d " "` --&gt; marca el delimitador entre campos en un tabla \(en este caso el espacio\)  
 solo puede ser un unico caracter. Sirve para utilizar la opcion -f.  
 `-f [3]` --&gt; coge solo la tercera columna \(los espacios en blanco se consideran columnas en las tablas  
 en este caso\)  
 P.E: `cut -d " " -f 3`

 **TEE** --&gt; lee de entrada estandar y escribe a salida estandar y fichero.  
 En resumen: saca el resultado por pantalla y por fichero.  
 P.E: `ps aux | tee ps.txt #sale por pantalla y por fichero ps.txt`

 **BASENAME** --&gt; Muestra nombre del archivo especificado en una ruta.

 **STAT** --&gt; Muestra informacion de un fichero. Sin opciones pone fechas de acceso, modificacion y cambio.  
 `stat -c%U test.txt` -- Usuario propietario  
 `-c%u` --&gt; PID usuario propietario  
 `-c%G` --&gt; Grupo propietario  
 `-c%g` --&gt; PID grupo propietario  
 `-c%n` --&gt; nombre completo del archivo  
 `-c%F` --&gt; tipo de fichero  
 `-c%A` --&gt; permisos  
 `-c%a` --&gt; permisos en octal  
 `-c%x` --&gt; ultima fecha de acceso  
 `-c%y` --&gt; ultima fecha de modificacion \(cambian las caracteristicas P.E: permisos\)  
 `-c%z` --&gt; ultima fecha de cambio \(cambia el contenido\)

 **MORE** --&gt; Como cat pero va mostrando poco a poco el texto. Cat mejorado.  
 `enter` --&gt; muestra la siguiente linea  
 `space` --&gt; muestra la siguiente pagina  
 `d` --&gt; se mueve 11 lineas hacia delante  
 `5s` --&gt; se mueve 5 lineas hacia delante  
 `5f` --&gt; se mueve 5 lineas hacia detras  
 `v` --&gt; abre el editor vim en la posicion del cursor  
 `h` --&gt; muestra ayuda  
 `q` --&gt; lo quita

 **LESS** --&gt; Muy parecido al more, pero se mueve el contenido con los cursores.

 **HEAD** --&gt; Muestra las primeras lineas de un fichero.

 **TAIL** --&gt; Muestra las ultimas lineas de un fichero.

 **LN** --&gt; Link. Crea enlaces entre archivos.  
 `-s` --&gt; crea enlaces simbólicos

{% hint style="info" %}
Los ficheros en linux, se almacenan en el disco duro y se crea un puntero en la ruta seleccionada con acceso a esa informacion. Cuando hago un link, existen dos tipos principales:  
 **Hard link** --&gt; Crea otro puntero a esa informacion que se almacena en el disco.  
 No se pueden generar entre particiones.  
 **Simbolic link** --&gt; Crea un puntero al puntero de la informacion en el disco \(como un shortcut\)  
 Se pueden crear de una particion a otra.
{% endhint %}

 **SED** --&gt; Editor de flujos y ficheros de forma no interactiva.  
 Permite modificar el contenido de las lineas de un fichero en base a comandos.  
 `-e` --&gt; añade un script al comando  
 `-f` --&gt; añade el script del archivo al comando

 **s** --&gt; sustituir  
 `sed 's/a/A/g' hola.txt #sustituye(s) todas(g) las (a) por A.`  
 `sed '1,10s/a/A/g' hola.txt #solo hace la sustitución en las filas de 1 al 10.`  
 **d** --&gt; eliminar  
 `sed '1,5d' hola.txt #Elimina las filas de la 1 a la 5.`

 **TR** --&gt; filtro de sustitucion.  
 `-s` --&gt; permite cambiar un conjunto de caracteres iguales por uno igual.  
 Sirve para convertir un tabulador en un espacio  
 `tr -s " " #Sustituye conjuntos de espacios en un espacio`  
 `-c` --&gt; Sustituye en la salida todos los caracteres excepto los indicados en el argumento1 por los especificados en el argumento2.  
 `tr -c '[a-f][A-F][1-5]' x <> test.txt #Sustituye todo menos los tres conjuntos del arg1 por la letra x. Toma como entrada el archivo test.txt y como salida el mismo (de ahí ese <>).`  
 `-d` --&gt; Suprime los caracteres asignados en el argumento-1.

`echo "Hola a todos" | tr -d o #Elimina la letra o en el output.`

 **PASTE** --&gt; Concatena el contenido de varios archivos añadiendolos tabulados.  
 `-d` --&gt; cambia el separador P.E: `-d "," #en vez de tabulador pone comas.`  
 `-s` --&gt; concatena el contenido de varios archivos poniendo el contenido de cada uno en una fila.

 **EXPAND** --&gt; Modifica un tabulador convirtiendolo en 8 espacios.  
 `-t` --&gt; marca en cuantos espacios se convierte el tabulador

 **HEXDUMP** --&gt; transforma un archivo a hexadecimal  
 `-C` --&gt; Para sacar el hexadecimal y el ASCII \(legible\).

 **OD** --&gt; transforma un archivo a octal

 **ICONV** --&gt; permite convertir el codeset de un fichero.  
 `--list` --&gt; lista los codeset disponibles.

 P.E: `iconv -f UTF-8 -t ISO-8888 fichero.tx`

{% hint style="info" %}
`Para saber más sobre los codesets aquí:` [`https://www.w3.org/International/articles/definitions-characters/index.es`](https://www.w3.org/International/articles/definitions-characters/index.es)\`\`
{% endhint %}

 **NANO** --&gt; Editor de texto. Permite editar archivos de texto desde la terminal.

**VIM** --&gt; Editor de texto de linea de comandos. Muy potente pero más complicado de utilizar que el nano.

 **GEDIT** --&gt; Editor de texto grafico. Tipo bloc de notas. \(Cada distribución de Linux tiene uno por defecto, éste es el de Debian\).

