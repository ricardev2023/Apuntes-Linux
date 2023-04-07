---
description: Comandos para la gestión de archivos y directorios en ambientes Linux.
---

# 02- GESTIÓN DE ARCHIVOS Y DIRECTORIOS

## TIPOS DE FICHEROS

\
&#x20;**-** --> fichero regular\
&#x20;**d** --> directorio\
&#x20;**l** --> enlace\
&#x20;**c** --> dispositivos especiales de caracteres\
&#x20;**p** --> canales\
&#x20;**s** --> shocket

## **COMANDOS**

**PWD** --> Print Working Directory. Indica el directorio en el que estamos trabajando.

&#x20;**FILE** --> Da informacion del tipo de archivo que hemos seleccionado.\
&#x20;P.E: `file /bin/sync`

&#x20;**LS** --> List directory contents. Lista los elementos en el directorio.\
&#x20;`-l` --> nos da más información sobre los archivos.\
&#x20;`-a` --> incluye archivos y directorios ocultos.\
&#x20;`-R` --> incluye los subdirectorios de cada directorio.

&#x20;**SORT** --> Lista ordenadamente del contenido de los elementos de un directorio o una serie de archivos.\
&#x20;P.E: sort 1.txt 2.txt 3.txt\
&#x20;`-b` --> ignora los espacios en blanco iniciales\
&#x20;`-d` --> solo tiene en cuenta espacios y alfanumerico\
&#x20;`-f` --> ignora mayusculas o minusculas\
&#x20;`-r` --> saca el listado inverso

&#x20;**TREE** --> Lista en forma de arbol los directorios y subdirectorios desde\
&#x20;el directorio en el que me encuentro, para abajo.

&#x20;**GREP** --> Busqueda global. Busca una letra o palabra en el texto que sale por\
&#x20;pantalla. ---------> BUSCAR MAN POR QUE TIENE MIL POSIBILIDADES.\
&#x20;`grep [opciones] [patron] [archivo]`\
&#x20;`-i` --> no distingue entre mayusculas y minusculas\
&#x20;`-r` --> busqueda recursiva (busca en todos los archivos del directorio)\
&#x20;`-c` --> muestra cuantas lineas coinciden con el patron.\
&#x20;`-n` --> añade el numero de linea delante.\
&#x20;`-v` --> muestra por pantalla las lineas del documento que no coinciden con el texto buscado.\
&#x20;`-l` --> muestra el nombre de los archivos que SI tienen coincidencias.\
&#x20;`-L` --> muestra el nombre de los archios que NO tienen coincidencias.\
&#x20;`-o` --> muestra solo las palabras que coinciden, no toda la linea (util si busco varias palabras).\
&#x20;`-q` --> no muestra nada como salida (util para escribir codigos como el P.E.2)

\
&#x20;P.E.1 --> `grep -i comando /Desktop/01_Guias/Terminal/00_Guia_Basicos`\
&#x20;(muestra por pantalla el texto de las lineas del documento que incluyen la palabra comando).

\
&#x20;P.E.2 -->`grep -ir comando /Desktop/ && echo SI || echo NO`\
&#x20;(muestra por pantalla (SI y las lineas de texto que lo incluyen) si en alguno de los documentos de texto del directorio Desktop aparece la palabra comando (sin tener en cuenta mayusculas o minusculas). En caso contrario imprime (NO).

&#x20;**EGREP** --> Busqueda extendida\
&#x20;`egrep 'auto|iface|comando' /etc/network/interfaces #me busca las lineas que tienen cada una de las palabras`

&#x20;**FIND** --> Encontrar. Busca un archivo en el sistema.\
&#x20;`find [directorio inicio][opciones][que buscar]`\
&#x20;P.E. -->`find / -iname "nombre de archivo"`\
&#x20;**/** --> significa empezar a buscar en la raiz (\~ sirve para buscar en home)\
&#x20;`-name` --> busca por nombre\
&#x20;`-iname` --> busca por nombre sin tener en cuenta mayus\
&#x20;`-user` --> busca por usuario propietario\
&#x20;`-group` --> busca por grupo propietario\
&#x20;`-type` --> busca por tipo de archivo (según los tipos de este tema)\
&#x20;`-amin` --> archivos modificados en los ultimos \[-amin 3] minutos\
&#x20;`-atime` --> archivos modificados en los ultimo \[-atime 10] dias\
&#x20;`-syze` --> busca por tamaño\
&#x20;`!`--> NOT. Busca lo contrario de lo que se pone en la opcion de despues. Un ! por opcion.

&#x20;**LOCATE** --> Encontrar ficheros en el sistema. Necesita tener una base de datos actualizada.\
&#x20;`updatedb` --> actualiza la base de datos del sistema para usarla en locate.\
&#x20;`locate [que buscar]` --> busca en todo el sistema muy rapido.\
&#x20;`-i` --> no distingue entre mayusculas y minusculas.

&#x20;**WHEREIS** --> Para ver la ruta de un archivo.\
&#x20;`-b` --> nos muestra solo la ruta de archivos binarios.\
&#x20;`-m` --> muestra la ruta de los manuales\
&#x20;`-s` --> muestra la ruta de la fuente.

&#x20;**CD** --> Change Directory. Cambia al directorio que seleccionemos\
&#x20;P.E.--> `cd Escritorio/ #puedo utilizar tambien rutas absolutas`\
&#x20;`cd` --> me manda directamente a la carpeta de usuario.\
&#x20;`cd ..` --> me manda a la carpeta del nivel superior.

&#x20;**MKDIR** --> Make Directory (crea una carpeta en la ruta seleccionada)\
&#x20;`-p` --> permite crear un sistema de directorios

`-m` --> permite añadir permisos al directorio

\
&#x20;P.E: `mkdir -p test/{test1,test2,test3/{test3.1,test3.2}}/`\
&#x20;genera el directorio test con test1,2 y 3 en su interior y test3.1 y 3.2 dentro de test3.

\
&#x20;P.E: `mkdir -m 550 test`\
&#x20;genera el directorio test con permisos de lectura y ejecución para usuario y grupo propietario.

&#x20;**RMDIR** --> Remove Directory. Borra un directorio vacio.\
&#x20;`-p` --> elimina carpetas y subcarpetas.

&#x20;**TOUCH** --> Crea un archivo vacio en la ruta seleccionada.\
&#x20;Si el archivo ya existe le cambia la fecha de modificacion.

&#x20;**CP** --> Copy. Copia el archivo en la ruta absoluta seleccionada.\
&#x20;P.E.--> `cp prueba.txt /home/username/Escritorio`

&#x20;**DD** --> Data Duplicator. Permite copiar de manera secuencial.\
&#x20;Se utiliza mucho en analisis forense. Es muy potente.\
&#x20;`dd if=$inputdata of=$outputdata [opciones]`\
&#x20;`bs= [tamaño de los paquetes]`\
&#x20;`count= [cantidad de bloques a copiar]`

&#x20;**MV** --> Move. Mueve un archivo a la ruta absoluta seleccionada.

&#x20;**RM** --> Remove. Elimina un archivo en la ruta seleccionada o en la carpeta actual.\
&#x20;`-r` --> Si queremos borrar una carpeta no vacía.\
&#x20;`-f` --> fuerza la accion.\
&#x20;`-i` --> pregunta antes de ejecutar

&#x20;**SPLIT** --> Permite dividir un paquete en archivos mas pequeños\
&#x20;`-a` --> marca la longitud del sufijo\
&#x20;`-d` --> utiliza sufijos numericos empezando en 0, no alfabeticos\
&#x20;`-c` --> marca el tamaño maximo de los archivos de salida en BYTES.\
&#x20;`-l` --> marca el tamaño maximo de los archivos de salida en LINEAS.\
&#x20;P.E: `split -d -c 20k imagen.iso`

&#x20;**CAT** --> Concatenate. Muestra el contenido de un archivo.\
&#x20;`-n` --> numera los renglones\
&#x20;`-b` --> numera solo las lineas que no estaban en blanco\
&#x20;`-E` --> marca el final de las lineas con $ (util para programar)\
&#x20;`-s` --> muestra solo la primera linea en blanco si hay muchas.\
&#x20;`>` --> permite dar contenido a un documento. (termina con CTRL+D)\
&#x20;`>>` --> permite aumentar el contenido de un documento (termina con CTRL+D)

&#x20;**TAC** --> Invierte la salida de CAT. (la ultima linea pasa a ser la primera).

&#x20;**NL** --> Como cat pero numerando las lineas.

&#x20;**WC** --> Da informacion del contenido de un fichero.\
&#x20;`N (Lineas) N (palabras) N (caracteres)`

&#x20;**-W** --> cuenta solo las lineas.

&#x20;**DIFF** --> Busca diferencias entre dos archivos.\
&#x20;P.E: `diff 1.txt 2.txt`

&#x20;`-b` --> No hace caso de las diferencias por espacio en blanco\
&#x20;`-B` --> No hace caso de las diferencias por lineas en blanco\
&#x20;`-q` --> Solo informa de si difieren o no, sin mostrar los cambios\
&#x20;`-r` --> Recursivo en directorios. Compara dos ficheros cualesquiera\
&#x20;`-y` --> Emplea el formato de lado a lado.

&#x20;**UNIQ** --> Muestra las lineas no repetidas de un conjunto de archivos.\
&#x20;`-c` --> pone antes de cada linea el numero de coincidencias\
&#x20;`-d` --> muestra las lineas repetidas solo una por duplicidad\
&#x20;`-D` --> muestra TODAS las lineas duplicadas\
&#x20;`-i` --> ignora diferencia entre mayus y minus\
&#x20;`-u` --> muestra solo las lineas unicas

&#x20;**COLUMN** --> Pone el contenido por columnas.\
&#x20;`-t` --> utiliza los espacios como separadores\
&#x20;`-s` --> Se utiliza con -t para utilizar otro separador que no sea el espacio\
&#x20;P.E: column -t -s ":"

&#x20;**CUT** --> elimina secciones de cada fila de un fichero ------> tiene muchas opciones. Ver man.\
&#x20;`-c [a,b,c]` --> elimina solo las letras a, b y c.\
&#x20;`-d " "` --> marca el delimitador entre campos en un tabla (en este caso el espacio)\
&#x20;solo puede ser un unico caracter. Sirve para utilizar la opcion -f.\
&#x20;`-f [3]` --> coge solo la tercera columna (los espacios en blanco se consideran columnas en las tablas\
&#x20;en este caso)\
&#x20;P.E: `cut -d " " -f 3`

&#x20;**TEE** --> lee de entrada estandar y escribe a salida estandar y fichero.\
&#x20;En resumen: saca el resultado por pantalla y por fichero.\
&#x20;P.E: `ps aux | tee ps.txt #sale por pantalla y por fichero ps.txt`

&#x20;**BASENAME** --> Muestra nombre del archivo especificado en una ruta.

&#x20;**STAT** --> Muestra informacion de un fichero. Sin opciones pone fechas de acceso, modificacion y cambio.\
&#x20;`stat -c%U test.txt` -- Usuario propietario\
&#x20;`-c%u` --> PID usuario propietario\
&#x20;`-c%G` --> Grupo propietario\
&#x20;`-c%g` --> PID grupo propietario\
&#x20;`-c%n` --> nombre completo del archivo\
&#x20;`-c%F` --> tipo de fichero\
&#x20;`-c%A` --> permisos\
&#x20;`-c%a` --> permisos en octal\
&#x20;`-c%x` --> ultima fecha de acceso\
&#x20;`-c%y` --> ultima fecha de modificacion (cambian las caracteristicas P.E: permisos)\
&#x20;`-c%z` --> ultima fecha de cambio (cambia el contenido)

&#x20;**MORE** --> Como cat pero va mostrando poco a poco el texto. Cat mejorado.\
&#x20;`enter` --> muestra la siguiente linea\
&#x20;`space` --> muestra la siguiente pagina\
&#x20;`d` --> se mueve 11 lineas hacia delante\
&#x20;`5s` --> se mueve 5 lineas hacia delante\
&#x20;`5f` --> se mueve 5 lineas hacia detras\
&#x20;`v` --> abre el editor vim en la posicion del cursor\
&#x20;`h` --> muestra ayuda\
&#x20;`q` --> lo quita

&#x20;**LESS** --> Muy parecido al more, pero se mueve el contenido con los cursores.

&#x20;**HEAD** --> Muestra las primeras lineas de un fichero.

&#x20;**TAIL** --> Muestra las ultimas lineas de un fichero.

&#x20;**LN** --> Link. Crea enlaces entre archivos.\
&#x20;`-s` --> crea enlaces simbólicos

{% hint style="info" %}
Los ficheros en linux, se almacenan en el disco duro y se crea un puntero en la ruta seleccionada con acceso a esa informacion. Cuando hago un link, existen dos tipos principales:\
&#x20;**Hard link** --> Crea otro puntero a esa informacion que se almacena en el disco.\
&#x20;No se pueden generar entre particiones.\
&#x20;**Simbolic link** --> Crea un puntero al puntero de la informacion en el disco (como un shortcut)\
&#x20;Se pueden crear de una particion a otra.
{% endhint %}

&#x20;**SED** --> Editor de flujos y ficheros de forma no interactiva.\
&#x20;Permite modificar el contenido de las lineas de un fichero en base a comandos.\
&#x20;`-e` --> añade un script al comando\
&#x20;`-f` --> añade el script del archivo al comando

&#x20;**s** --> sustituir\
&#x20;`sed 's/a/A/g' hola.txt #sustituye(s) todas(g) las (a) por A.`\
&#x20;`sed '1,10s/a/A/g' hola.txt #solo hace la sustitución en las filas de 1 al 10.`\
&#x20;**d** --> eliminar\
&#x20;`sed '1,5d' hola.txt #Elimina las filas de la 1 a la 5.`

&#x20;**TR** --> filtro de sustitucion.\
&#x20;`-s` --> permite cambiar un conjunto de caracteres iguales por uno igual.\
&#x20;Sirve para convertir un tabulador en un espacio\
&#x20;`tr -s " " #Sustituye conjuntos de espacios en un espacio`\
&#x20;`-c` --> Sustituye en la salida todos los caracteres excepto los indicados en el argumento1 por los especificados en el argumento2.\
&#x20;`tr -c '[a-f][A-F][1-5]' x <> test.txt #Sustituye todo menos los tres conjuntos del arg1 por la letra x. Toma como entrada el archivo test.txt y como salida el mismo (de ahí ese <>).`\
&#x20;`-d` --> Suprime los caracteres asignados en el argumento-1.

`echo "Hola a todos" | tr -d o #Elimina la letra o en el output.`

&#x20;**PASTE** --> Concatena el contenido de varios archivos añadiendolos tabulados.\
&#x20;`-d` --> cambia el separador P.E: `-d "," #en vez de tabulador pone comas.`\
&#x20;`-s` --> concatena el contenido de varios archivos poniendo el contenido de cada uno en una fila.

&#x20;**EXPAND** --> Modifica un tabulador convirtiendolo en 8 espacios.\
&#x20;`-t` --> marca en cuantos espacios se convierte el tabulador

&#x20;**HEXDUMP** --> transforma un archivo a hexadecimal\
&#x20;`-C` --> Para sacar el hexadecimal y el ASCII (legible).

&#x20;**OD** --> transforma un archivo a octal

&#x20;**ICONV** --> permite convertir el codeset de un fichero.\
&#x20;`--list` --> lista los codeset disponibles.

&#x20;P.E: `iconv -f UTF-8 -t ISO-8888 fichero.tx`

{% hint style="info" %}
`Para saber más sobre los codesets aquí:` [`https://www.w3.org/International/articles/definitions-characters/index.es`](https://www.w3.org/International/articles/definitions-characters/index.es)
{% endhint %}

&#x20;**NANO** --> Editor de texto. Permite editar archivos de texto desde la terminal.

**VIM** --> Editor de texto de linea de comandos. Muy potente pero más complicado de utilizar que el nano.

&#x20;**GEDIT** --> Editor de texto grafico. Tipo bloc de notas. (Cada distribución de Linux tiene uno por defecto, éste es el de Debian).
