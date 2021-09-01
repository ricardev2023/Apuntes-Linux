---
description: Ejemplo de actualización de Kernel.
---

# 12\_ACTUALIZAR\_KERNEL

El **Kernel** de Linux® es el elemento principal de los sistemas operativos \(SO\) Linux, y es la interfaz  
fundamental entre el hardware de una computadora y sus procesos. Los comunica entre sí y gestiona los  
recursos de la manera más eficiente posible.

Los kernel de Linux se actualizan en una pagina llamada kernel.org.

En ella hay un repositorio GIT llamado[ https://git.kernel.org/](https://git.kernel.org/) donde puedes buscar el que necesitas \(por regla general la ultima versión\).

1. Una vez en el repositorio hay que buscar uno confiable, como por ejemplo los de Torvalds \(creador de Linux\).
2. Tras descargarlo tendremos un archivo con el siguiente formato:  `linux-5.9-rc5.tar.gz`
3. Lo descomprimimos con `tar -xvzf linux-5.9-rc5.tar.gz`
4. Para evitar tener que configurar los módulos desde cero en el nuevo kernel, copiamos el archivo de configuracion del antiguo a la carpeta extraida:  `cp /boot/config-4.9.0-13-amd64 .config`
5. Una vez hecho esto, generamos el nuevo conjunto de módulos con:  `make menuconfig`
6. En este menu que aparece, seleccionamos los modulos y despues guardamos.
7. Tras esto, instalamos los nuevos modulos del kernel con:  `make`
8. Para instalar los modulos adicionales hacemos:  `make modulesinstall`
9. Para instalar el kernel:  `make install`
10. Para habilitar el kernel nuevo en el inicio:  `update-initramfs -c -k linux-(version descargada)`
11. Actualizar el GRUB:  `update-grub`
12. Por ultimo para que todo tenga efecto: `reboot` y rezar.









  
 













