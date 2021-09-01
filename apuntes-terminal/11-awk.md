---
description: Aproximación al comando AWK.
---

# 11- COMANDO AWK

## **COMANDO AWK**

AWK es una herramienta de procesamiento de patrones en líneas de texto. Su utilización estándar es la de filtrar ficheros o salida de comandos de UNIX, tratando las líneas para, por ejemplo, mostrar una determinada información sobre las mismas.

### **FORMATO**

`awk '[opciones] { comandos }'`

###  OPCIONES

`-f` --&gt; lee el codigo del fichero que se marque \(nombre ruta\)  
`-F` --&gt; field separator. Cambia el separador \(espacio por defecto\)  
`-v var=VAL` --&gt; Asigna el valor VAL a la variable var.  
`-d` --&gt; muestra una lista de todas las variables. Puede servir para detectar errores tipograficos.

###  **VARIABLES DE COMANDO**

* **$0** --&gt; Mostrar la línea completa
* **$1-$N** --&gt; Mostrar los campos \(columnas\) de la línea especificados.
* **FS** --&gt; Field Separator \(" " por defecto\)
* **FIELDWIDTHS** --&gt; Longitud de los campos \(por defecto no tiene valores definidos\)
* **NF** --&gt; Número de campos \(fields\) en el registro actual
* **$NF** --&gt; Valor del ultimo campo de cada registro
* **FNR** --&gt; Número de registro \(records\) que se está leyendo en el fichero que se está procesando
* **NR** --&gt; Número de registros \(records\) que se esta leyendo en el stream a procesar.
* **OFS** --&gt; Output Field Separator \(" " por defecto\).
* **ORS** --&gt; Output Record Separator \("\n" por defecto\).
* **RS** --&gt; Input Record Separator \("\n" por defecto\).
* **BEGIN** --&gt; Define sentencias a ejecutar antes de empezar el procesado.
* **END** --&gt; Define sentencias a ejecutar tras acabar el procesado.
* **length** --&gt; Longitud de la línea en proceso.
* **FILENAME** --&gt; Nombre del fichero en procesamiento.
* **ARGC** --&gt; Número de parámetros de entrada al programa.
* **ARGV** --&gt; Valor de los parámetros de entrada al programa.
* **ENVIRON** --&gt; Es un array que contiene las variables de entorno \(P.E: ENVIRON\["HOME"\]
* **IGNORECASE** --&gt; Ignora diferencia entre mayusculas y minusculas \(Si su valor es =! 0\)

###  **CONTROL DE FLUJO**

* `if ( expr ) statement`
* `if ( expr ) statement else statement`
* `while ( expr ) statement`
* `do statement while ( expr )`
* `for ( opt_expr ; opt_expr ; opt_expr ) statement`
* `for ( var in array ) statement`
* `continue, break`
* `(condicion)? a : b --> if(condicion) a else b;`
* `function (){contenido de funcion}`



###  **OPERADORES SOPORTADOS**

| \* | / | % | + | - | = |  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| ++ | -- | += | -= | \*= | /= | %= |

###  **FUNCIONES INTERNAS**

* toupper\(\) --&gt; pone el contenido de la variable en mayusculas.
* tolower\(\) --&gt; pone el contenido de la variable en minuscula.
* lenght\(\) --&gt; indica la longitud de cada uno de los registros \(en numero de caracteres\)
* close\(fichero\_a\_reiniciar\_desde\_cero\)
* cos\(x\)
* sin\(x\)
* index\(\)
* int\(num\)
* substr\(str,pos,len\)
* system\(orden\_del\_sistema\_a\_ejecutar\)
* printf\(\) --&gt; permite imprimir por pantalla incluyendo contenido de variables:
* %s --&gt; string de texto
* %c --&gt; salida numérica de cadena de string
* %d --&gt; valor numerico entero
* %f --&gt; valor decimal



