---
description: Conceptos y comandos básicos para la gestión de redes en ambientes Linux.
---

# 06- GESTIÓN DE REDES

## **INFORMACIÓN GENERAL**

### **CONCEPTOS**

**IPv4** --&gt; Cada equipo conectado a una red tiene una IPv4 que lo identifica, esta IP puede ser:

 **Publica** --&gt; Son las que identifican los equipos en internet. IANA es la organizacion encargada  
 del reparto de las IPs públicas y de los dominios .com / .net y ya se han agotado hace años.  
 Ahora se reparten IPv6

 **Privada** --&gt; Sirven para identificarse en una red local, son:  
 10.0.0.0 255.0.0.0  
 172.16.0.0 255.255.0.0  
 192.168.0.0 255.255.255.0  
 169.254.0.0

**IPv6** --&gt; Las IPv6 tambien identifican individualmente a los equipos, con la diferencia de que no diferencian  
 entre IP publica o privada, son todas publicas. Da para 340 sextillones de direcciones. Esta formada  
 por 32 caracteres hexadecimales \(de 0 a F\).  
 REGLA 1 --&gt; En este caso, los ceros a la izquierda de cada grupo se pueden quitar.  
 REGLA 2 --&gt; Se pueden utilizar una vez los dos puntos dobles, para representar un cumulo de ceros.

 P.E: FF00:0000:0000:0000:0000:0FE3:000C:0083 --&gt; IPv6 completa.  
 FF00:0:0:0:0:FE3:C:83 --&gt; IPv6 utilizando la primera regla.  
 FF00::FE3:C:83 --&gt; IPv6 utilizando las dos reglas.

**VIP** --&gt; Direccion IP Virtual. Se basa en general un tunel virtual que de salida \(por ejemplo\) por dos cauces  
 diferentes a internet. Entonces generamos un grupo HSRP de tal manera que si el Master falla,  
 siempre podre tener acceso a internet a traves del slave.

**MASCARA DE SUBRED** --&gt; sirve para delimitar el ambito de una red de ordenadores. Tambien permite terminar de  
identificar un equipo de una red. Hay tres tipos principales:

 **Clase C** --&gt; 255.255.255.0 /24 \(254 hosts\)

 **Clase B** --&gt; 255.255.0.0 /16 \(65.534 hosts\)

 **Clase A** --&gt; 255.0.0.0 /8 \(16.777.214 hosts\)

 **Clase D** --&gt; Multicast

 **Clase E** --&gt; Desarrollos experimentales

**SUBNETING** --&gt; Si no utilizamos las mascaras de subred habituales y utilizamos /28 o /17 podemos modificar  
 el maximo de equipos conectados a la red. Para ello el switch debe ser compatible con VLSM. Si no  
 lo es, hay que utilizar un protocolo que sea compatible.

**DIRECCION DE RED** --&gt; Manera estandar de referirse a una red. \(192.168.1.0\)

**DIRECCION DE BROADCAST** --&gt; Permite la comunicación a todos los host de una red. \(192.168.1.255 --- FF01::1/128\)

**PUERTA DE ENLACE** --&gt; Dispositivo \(normalmente router\) que actua de interfaz entre red interna e internet.  
 Transforma la IP privada a una IP publica propia de la puerta de enlace. \(192.168.1.1\)

**APIPA** --&gt; Con la asignación automática de direcciones IP privadas, los clientes DHCP se asignan  
 automáticamente una dirección IP y una máscara de subred, cuando no está disponible un servidor  
 DHCP. El dispositivo se asigna su propia dirección IP en el rango 169.254.1.0 a 169.254.254.255.  
 En IPv6 equivale a FE80::/64

**LOCAL HOST** --&gt; permite referirse a la misma maquina. Es 127.0.0.1 y en IPv6 1/128

**DIRECCION MAC** --&gt; Media Access Control. Identificador de 48bits que corresponde a una tarjeta de red.  
 P.E: 50:56:BF:00:12:2F.  
 Si empieza por 08.00.x.x.x.x significa que es una maquina virtualizada.

 Si hablamos de una MAC IPv6 se añade en medio FF:FF o FF:FE. para poder virtualizar todas las MAC  
 P.E: 50:56:BF:FF:FF:00:12:2F

**DNS** --&gt; Domain Name System. Servidores con una base de datos que almacena IP asociadas a nombres de dominios.  
 Hay tres tipo principales

 **DNS hosts** --&gt; Un archivo en el host donde se guardan algunas relaciones. Se realiza la primera busqueda.

 **DNS interno** --&gt; Interno de una empresa para identificar todos los equipos de una red local.

 **DNS externo** --&gt; Propiedad de un servidor de internet, se acceden desde internet.

**DHCP** --&gt; Dinamic Host Configuration Protocol. Permite asignar una IP publica a un equipo de manera automatica.  
 Estas IP,s publicas no son las mismas para los equipos, por ello, no se puede utilizar este protocolo  
 en servidores que deban ser accesibles.

**LOOPBACK \(INTERFAZ LO\)** --&gt; Existe por defecto. Sirve para trabajos locales \(lo utilizan las aplicaciones\)  
 Su IPv4 es 127.0.0.1 y es siempre la misma para identificar a mi propio equipo.

Existen muchos protocolos de transmisión de la información:

### PROTOCOLOS DE RED

 **TCP** --&gt; **Transmission Control Protocol**. es un protocolo orientado a conexión, es decir, que permite que dos  
 máquinas que están comunicadas controlen el estado de la transmisión. Con el uso del protocolo TCP,  
 las aplicaciones pueden comunicarse en forma segura \(gracias al sistema de acuse de recibo del  
 protocolo TCP\). Durante una comunicación usando el protocolo TCP, las dos máquinas deben establecer  
 una conexión. La máquina emisora \(cliente\) y la receptora \(servidor\). La comunicación se realiza  
 en ambas direcciones. Una conexión tcp/ip empieza con elthree−way−handshake:  
 − La maquina que desea conectarse a otra envia un paquete con flag SYN  
 − Si la otra maquina acepta, envia un SYN/ACK  
 − Entonces la máquina establece la conexión.

 **UDP** --&gt; **User Datagram Protocol**. Permite el envío de datagramas a través de la red sin que se haya  
 establecido previamente una conexión, ya que el propio datagrama incorpora suficiente información  
 de direccionamiento en su cabecera.  
 Su uso principal es para protocolos como DHCP, BOOTP, DNS.  
 No es fiable. No emplea control del flujo ni ordena los paquetes.No tiene confirmacion.

 **ICMP** --&gt;**Protocolo de Mensajes de Control de Internet.** sub protocolo de control y notificación de  
 errores del Protocolo IP. eneralmente no se utiliza directamente por las aplicaciones de  
 usuario en la red. La única excepción es la herramienta ping y traceroute.

 **HTTP** --&gt;Es el protocolo de comunicación que permite las transferencias de información en la  
 World Wide Web. HTTP define la sintaxis y la semántica que utilizan los elementos de  
 software de la arquitectura web \(clientes, servidores, proxies\) para comunicarse. HTTP  
 es un protocolo sin estado, es decir, no guarda ninguna información sobre conexiones  
 anteriores. El desarrollo de aplicaciones web necesita frecuentemente mantener estado.  
 Para esto se usan las cookies, que es información que un servidor puede almacenar en el  
 sistema cliente. Esto le permite a las aplicaciones web instituir la noción de "sesión",  
 y también permite rastrear usuarios ya que las cookies pueden guardarse en el cliente por  
 tiempo indeterminado.

 **FTP** --&gt; **File Transfer Protocol**. protocolo de red para la transferencia de archivos entre sistemas  
 conectados a una red TCP. utilizando normalmente el puerto de red 20 y el 21.todo el intercambio  
 de información, desde el login y password del usuario en el servidor hasta la transferencia de  
 cualquier archivo, se realiza en texto plano sin ningún tipo de cifrado.  
 Para solucionar este problema son de gran utilidad aplicaciones como SCP y SFTP, incluidas en el  
 paquete SSH, que permiten transferir archivos pero cifrando todo el tráfico.

### **PUERTOS IMPORTANTES TCP**

**20 FTP  
21 FTP \(por defecto\)  
22 SSH  
23 TELNET  
25 SMTP \(correo electronico\)  
37 TIME  
53 DNS  
66 ORACLE SQLNET  
67 DHCP  
68 DHCP  
80 HTTP  
110 POP3  
139 NETBIOS  
143 IMAP  
161 SNMP  
389 LDAP \(autenticacion WinServer\)  
443 HTTPS  
465 SMTP \(Cifrado\)  
631 IIP \(impresoras\)  
993 IMAP \(Cifrado\)  
995 POP3 \(Cifrado\)  
1194 OpenVPN  
1433 SQL SERVER  
2525 SMTP \(reserva\)  
3306 MYSQL  
10000 WEBMINS  
20000 USERMIN**

### **TIPOS DE CONEXIONES**

**NAT** --&gt; mecanismo utilizado por routers IP para intercambiar paquetes entre dos redes que asignan  
 mutuamente direcciones incompatibles. Consiste en convertir, en tiempo real, las direcciones  
 utilizadas en los paquetes transportados. También es necesario editar los paquetes para permitir  
 la operación de protocolos que incluyen información de direcciones dentro de la conversación del  
 protocolo.

**PAT** --&gt; traduce conexiones TCP y UDP hechas por un host y un puerto en una red externa a otra dirección y  
 puerto de la red interna. Permite que una sola dirección IP sea utilizada por varias máquinas de  
 la intranet. Con PAT, una IP externa puede responder hasta a ~64000 direcciones internas.

**DNAT** --&gt; Port Forwarding.

**SNAT** --&gt;

## **FICHEROS IMPORTANTES**

**/etc/network/interfaces** --&gt; permite gestionar las interfaces de red.  
 Para añadir una interface:  
 auto \[nombre interface\]  
 iface \[nombre interface\] inet static \(ip estatica\)/dhcp \(ip dinamica\)  
 address \[direccion ip\] \(de aquí para abajo solo en caso de static\)  
 netmask \[mascara de subred\]  
 gateaway \[puerta\]  
 broadcast \[direccion broadcast\]

**/etc/resolv.conf** --&gt; Gestionar los servidores DNS.  
 para saber que DNS va mejor mando ping a sus IP y luego comparo  
 SEARCH --&gt; Dominio en el que realizar las busquedas internas.  
 DOMAIN --&gt; Dominio al que pertenece el equipo.  
 NAMESERVER --&gt; DNS,s en los que buscar. Entre los mejores estan:  
 8.8.8.8 DNS google  
 80.58.61.250 DNS telefonica

**/proc/sys/net/ipv4/ip\_forward** --&gt; Permite IP forwarding. Se encarga de la retransmision de los paquetes que  
 se reciben por una interfaz fisica a otra interfaz hacia otro nodo.

**/etc/nsswitch.conf** --&gt; marca prioridades del sistema. P.E: prioridad de busqueda de hosts en DNS,s.

**/etc/protocols** --&gt; listado de puertos de protocolos de red

**/etc/services** --&gt; listado de puertos de aplicaciones

## **COMANDOS**

**PING** --&gt; \(envía paquetes ICMP para comprobar si un host está levantado\)  
 no para hasta que le damos a las teclas ctrl+C.  
 como resultado da las estadísticas resultantes.  
 `-b` --&gt; permite mandar ICMP a una direccion broadcast  
 `-c` --&gt; para despues de mandar un numero limitado de pings  
 `-i` --&gt; permite marcar un intervalo entre pings  
 `-m` --&gt; marca los paquetes que salen  
 `-f` --&gt; fuerza un flujo de paquetes muy rapido.

**PING6** --&gt; envia PING a una IPv6  
 `ping6 [IPv6]%[interfaz]`

**FPING** --&gt; Permite hacer ping a varios host simultaneamente contenidos en un  
 Archivo de lista de IPs.  
 Está enfocado para su uso en scripts.  
 P.E. `fping -g 192.168.0.0/24 2> /dev/null | grep alive`  
 El ejemplo muestra qué máquinas de una red están levantadas.

**HOST** --&gt; resuelve la IPv4 y la IPv6, ademas de otros datos de interes de un dominio.

**GETENT** --&gt; resuelve las IP,s externas de un dominio  
 `getent ahosts google.es`

 **HOSTNAME** --&gt; cambia el nombre del host \($HOSTNAME\)

**DOMAINNAME** --&gt; cambia el nombre del dominio \($DOMAINNAME\). NO EN DEBIAN.

 **IFCONFIG** --&gt; muestra los adaptadores de red y sus datos. Permite config.  
 Si no esta instalado, instalar net-tools

 `IFDOWN [interfaz]` --&gt; tumba un interfaz de red \(en caso de que este en el /etc/network/interfaces\)  
 `IFUP [interfaz]` --&gt; levanta un interfaz de red \(en caso de que este en el /etc/network/interfaces\)  
 Se puede forzar una IP/netmask: `ifconfig enp0s3 up 192.168.1.25/24`

**IWCONFIG** --&gt; muestra los adaptadores de red INALAMBRICA y sus datos.  
 Si no esta instalado, instalar wireless-tools

**IP ADDRESS** --&gt; Es el comando que va a sustituir ifconfig en el corto plazo

**NMBLOOKUP** --&gt; resuelve nombres NetBios en direcciones IP.  
 `-M -- -` muestra las IPs de una red.  
 `-A` muestra los datos del equipo P.E: nmblookup -A 192.168.0.101

**NETSTAT** --&gt; Network Statistics. Lista las conexiones activas tanto entrantes como salientes  
 `-r` --&gt; nos permite ver las rutas de los equipos  
 `-s` --&gt; muestra las estadísticas de los protocolos  
 `-i` --&gt; muestra la transmisión por interfaces de red  
 `-a` --&gt; muestra todo  
 `-panut` --&gt; muestra la informacion mas relevante de la red.  
 Protocolo / Trafico / IP + puerto \(privada\) / IP + puerto \(publico\) / Estado / PID + Servicio

**TRACEROUTE** --&gt; muestra la ruta que sigue un paquete  
 `-n` --&gt; cambia los nombres por IP,s  
 `-I` --&gt; trafico ICMP  
 `-T` --&gt; trafico TCP  
 `-r` --&gt; se intenta hacer un bypass  
 `-p` --&gt; utiliza un puerto concreto

**TRACEROUTE6** --&gt; igual pero con IPv6

**ROUTE** --&gt; Muestra la tabla de enrutamiento de nuestro equipo  
 `-n` --&gt; no traduce los nombres con DNS, deja las IP,s  
 `add` --&gt; añade una ruta a la tabla  
 `del` --&gt; elimina una ruta de la tabla.  
 `-net` --&gt; poner un destino  
 `-host` --&gt; poner como destino un host unico  
 `netmask` --&gt; mascara de red  
 `gw` --&gt; puerta de enlace  
 `metric` --&gt;

 P.E: `route add -net 192.168.58.0 netmask 255.255.255.0 gw 10.0.2.2`

**NSLOOKUP** --&gt; Permite saber si el DNS funciona correctamente. \(instalar dnsutils\)  
 Permite saber la dirección IP sabiendo nombre y viceversa.

**DIG** --&gt; herramienta parecida a la anterior pero con mas informacion.

**WHOIS** --&gt; muestra informacion de un dominio.  
 Los dominios nacionales no dependen de IANA y no sirve el comando.

**TCPDUMP** --&gt; permite esnifar el tráfico de la red. \(VER MAN\)  
 `-A` --&gt; lo muestra en ASCII \(permite sacar hash de una contraseña\)

