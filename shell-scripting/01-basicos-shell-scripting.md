# 01- BÁSICOS SHELL SCRIPTING

## **BASICOS**

Llamamos **shell** a la consola de comandos. Existen varios tipos de shell en UNIX que se diferencian en pequeños detalles \(comandos, atributos, forma de interactuar, etc\). Por ejemplo tenemos:

* **BASH** \(la más utilizada en entornos Linux. Tambien se llama sh\)
* **BSH**
* **TCSH**
* **CSH**
* **ZSH**

{% hint style="info" %}
**ZSH** está ganando terreno a la shell **BASH** devido a su capacidad de personalización.
{% endhint %}

### **TIPOS DE COMANDOS**

Existen dos tipos de comandos:

* **Internos** --&gt; estan programados dentro de la Shell bash y no generan un nuevo proceso, no hay que instalarlos.
* **Externos** --&gt; hay que instalarlos y ejecutan un nuevo proceso.

{% hint style="info" %}
Los comandos internos de la bash se encuentran en /bin/
{% endhint %}

### **VARIABLES**

* **Locales**: solo se encuentran en el proceso iniciado. Al cerrar el script se borra. Se declaran con `VAR = valor`, aparecen al listarlas con **set** y no con **env**.
* **Globales**: se encuentran almacenadas en el proceso iniciado y en todos los subprocesos.  Se pasa de local a global con `export VAR`, y ya aparecería con el comando **env**.

#### **VARIABLES DE SISTEMA**

* **$DISPLAY:** Nos dice en que pantalla no gráfica se ejecuta una aplicación
* **$USER:** Almacena nombre de usuario conectado a la shell
* **$HISTFILE:** Se almacena el historial de comandos \(History\)
* **$HOME:** Indica la ruta del usuario
* **$LOGNAME:** Indica el usuario de acceso al sistema
* **$HOSTNAME:** Nombre del equipo
* **$LANG:** Configuración del idioma
* **$PATH:** Directorios de ejecución de los comandos
* **$PWD:** Muestra el directorio actual
* **$SHELL:** Muestra dirección de la shell usada
* **$TERM:** Muestra el emulador usado \(XTERM --&gt; modo gráfico o TTY --&gt; por sesión\)
* **$PS1:** prompt del terminal \(linea del terminal que aparece siempre...\)
* **$DISPLAY** sesión del entorno gráfico
* **Echo $!** Muestra PID último proceso del terminal
* **Echo $$** Muestra PID de la ventana Shell actual
* **Echo $?** Muestra 0 si el último proceso fue exitoso, 1 si es fallido
* **Echo $\_** Muestra atributos último proceso
* **$0** variable que representa el nombre del script
* **$1-9** Número de argumento que se da al script
* **$\#** Numero total de argumentos pasados al script actual
* **$\*** Lista completa de argumentos pasados \(cadena de texto\)
* **$@** Lista completa de argumentos pasados \(array\)
* **$-** Lista de opciones de la shell actual
* **$IFS** Separador de campos utilizado

### **CONSTANTES**

 Las constantes se almacenan el el archivo **`/home/usuario/.bashrc`**  
 Es útil para mantener los alias al apagar el equipo.

\*\*\*\*

### **COMANDOS**

**ENV** --&gt; muestra todas las variables del sistema  
 \(las variables del sistema empiezan siempre con $\)

**EXPORT** --&gt; pasa una variable de local a global  
 tambien se puede utilizar para generar una variable de sistema nueva.

**UNSET** --&gt; borra una variable de entorno

**LET** --&gt; Permite crear variables aritmeticas  
 let suma=4+6  
 let resta=6-4  
 let mult=6\*4  
 let div=12/6  
 let resto=6%4  
 let potencia=6\*\*4

**BASH** **-X** --&gt; da informacion de los pasos que sigue el programa.  
 muy util para depurado.

### **CONDICIONALES**

* **A == B** --&gt; Si A es igual a B.
* **A != B** --&gt; Si A es diferente a B.
* **A &gt; B** --&gt; Si A es mayor que B. 
* **A &lt; B** --&gt; Si A es menor que B. 
* **-n A** --&gt; Si A no es nulo. 
* **-s A** --&gt; Si A es nulo \(var vacia\).
* **A -lt B** --&gt; A es menor que B.
* **A -le B** --&gt; A es menor o igual que B.
* **A -eq B** --&gt; A es igual que B.
* **A -ge B** --&gt; A es mayor o igual que B.
* **A -gt B** --&gt; A es mayor que B.
* **A -ne B** --&gt; A es diferente que B.

### **OPERADORES LOGICOS**

* **\|\|** --&gt; Operador OR.
* **&&** --&gt; Operador AND.

### **ATRIBUTOS DE FICHERO**

`-d` --&gt; el fichero existe y es un directorio  
`-e` --&gt; el fichero existe  
`-f` --&gt; el fichero existe y es regular  
`-r` --&gt; tiene permisos de lectura  
`-x` --&gt; tiene permisos de ejecución  
`-s` --&gt; el directorio existe y no esta vacio  
`-a` --&gt; el archivo existe y tiene contenido

## ESTRUCTURAS DE CONTROL

### **IF**

Se traduce como SI condicional:

```text
if [ condicion $variable ]
then
 echo 1 (codigo a ejecutar si se cumple la condicion)
else
 echo 2 (codigo a ejecutar si no se cumple la condicion)
fi
```

### **CASE**

permite generar una respuesta para cada entrada de la variable

```text
echo "1- limpiar pantalla"
echo "2- directorio actual"
echo "3- ver historial"
echo "4- salir"
echo
echo "seleccione opcion" #hasta aqui se explica al usuario el contenido del script

read opcion (el usuario introduce una variable)

case $opcion in #en funcion del contenido de la variable empieza el case
1) clear ;; #si es 1
2) pwd;; #si es 2
3) history;; #si es 3
4) exit;; #si es 4
*) echo "no sabes escribir";; #cualquier otro contenido

esac #Se termina el case
```

### **FOR**

permite realizar un ciclo en una lista de elementos y ejecuta el codigo con cada uno de los valores.

```text
for variable in 'ls *.txt`; #da valor a variable, en este caso, 
                            #el nombre de todos los archivos.txt
                            #cada nombre es un valor para la variable
do   #empieza el codigo a ejecutar
 nano $variable
done #termina el codigo a ejecutar
```



### **WHILE**

permite ejecutar un codigo mientras se cumple una condicion \(mientras que ...\)

```text
variable=1 #creo la variable

while [ $variable -le 10 ] #indica la condicion que variable sea menor o 
                           #igual que 10
do #empieza el codigo a ejecutar cada ciclo)
 echo "Numero: $variable"
 variable=$(( $variable +1 )) #suma 1 a la variable al final de cada ciclo
done #termina el ciclo
```

### **UNTIL**

es como el while pero al revés \(la condicion es hasta que ...\)

```text
var=1

until [ $var -gt 10] #Para que tenga el mismo comportamiento que antes
                     #debe cambiarse la condición.
do
 echo "Numero $var"
 var=$(( $var +1 ))
done
```

### **SELECT**

```text
echo "¿Que quieres comer?"

select comida in sopa arroz carne #presenta por pantalla los 3 valores 
                                  #y se seleccionan con el numero de opcion.
do                                #Se puede poner el valor que uno quiera
 if [ $comida ] #si comida se corresponde con alguno de los valores select
 then           #se ejecuta el then, si no, el else
 echo "Hoy comes $comida"
 break
 else
 echo "No tenemos eso para comer"
 fi
done
```



## **FUNCIONES**

La estructura de las funciones es la siguiente:

```text
funcion ()
{
}
```

### EJEMPLO DE USO

{% embed url="https://blog.carreralinux.com.ar/2017/01/funciones-en-shell-scripts/" %}

Aunque el siguiente ejemplo es un tanto trivial, servirá para ilustrar el uso de funciones en shell scripts. Supongamos que tenemos un script que realiza ciertas tareas y al terminar cada una guarda en un archivo de texto o muestra por pantalla la hora de finalización. El siguiente script \(ejemplofuncion.sh\) comienza con la declaración de la función **Ahora**. Esta función, al ser invocada con un argumento \(como veremos más abajo\), hará una pausa de 5 segundos y mostrará la fecha y hora actuales por pantalla 3 veces:

```text
#!/bin/bash

# Declaramos la funcion
Ahora() {
    FECHA_HORA=$(date +'%d-%m-%Y %H:%M:%S')
    sleep 5
    echo "Tarea $1 completa - $FECHA_HORA"
}

# Primera tarea: desayuno
Ahora desayuno

# Segunda tarea
Ahora almuerzo

# Tercera tarea
Ahora cena
```

