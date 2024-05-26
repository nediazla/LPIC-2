![](img/sudo.png)
# Administrar Dispositivos de Almacenamiento

Los volúmenes RAID y lógicos se consideran configuraciones avanzadas de dispositivos de almacenamiento, debido a sus estructuras complicadas y los muchos términos confusos que los rodean.
Las figuraciones pueden ayudar a proteger sus datos, así como a mejorar sus velocidades generales de acceso a los datos. Además, a medida que aumentan las necesidades de almacenamiento de sus datos, estas estructuras de almacenamiento ofrecen una progresión de medios de almacenamiento bastante fluida. Varias utilidades pueden ayudar a configurar las opciones del kernel para admitir y configurar estos dispositivos avanzados. Algunas de estas utilidades también son útiles para monitorear los dispositivos. Comprender estos dispositivos y su configuración y administración es importante para la gestión de sus datos. Todos estos temas se tratan en este capítulo.
### Configuración de RAID
Por motivos de rendimiento y protección de datos del sistema, muchas empresas y particulares recurren a RAID. Una matriz redundante de discos independientes (RAID) es un conjunto de múltiples particiones de discos físicos combinadas en una única unidad virtual. Dependiendo de la estructura RAID elegida, esta unidad lógica puede lograr un rendimiento de acceso mejorado, una mayor protección de datos y un tiempo de inactividad reducido.
### Entendiendo el RAID
Las matrices RAID vienen en varias estructuras (a veces llamadas niveles RAID). Cada estructura se indica con un número y proporciona beneficios particulares. Si bien no sustituyen a las copias de seguridad, algunas estructuras RAID pueden mejorar la protección de los datos. Otras estructuras pueden mejorar los tiempos de lectura. Primero, determine sus necesidades de datos particulares para cada sistema y aplicación. Una vez que tenga esos requisitos a la mano, revise estas diversas estructuras RAID para elegir las mejores para satisfacer sus necesidades de datos.
RAID 0 Esta estructura RAID también se denomina división de discos. Cada archivo de datos se distribuye en varios discos de la matriz. Por ejemplo, si tiene dos discos, los datos de un archivo se dividen en partes entre los dos discos. En la Figura 5.1 se muestra un ejemplo diagramado de RAID 0 de dos discos.

![](img/5.1.png)

La lectura y escritura en diferentes fragmentos de archivos puede ocurrir en paralelo, lo que potencialmente puede acelerar las lecturas y escrituras en el archivo. Esta estructura RAID se utiliza normalmente para aplicaciones de gráficos o espacio de intercambio. La desventaja es que no hay tolerancia a fallos. Si alguna unidad de la matriz RAID falla, perderá toda la matriz.

La duplicación de disco RAID 1 es el otro nombre para este tipo de estructura RAID. Los mismos datos se escriben en dos discos diferentes, lo que proporciona una copia de seguridad original y una copia de seguridad reflejada. La estructura requiere un mínimo de dos discos, y los discos siempre deben ser múltiplos de dos: un disco para los datos y un disco para la copia de datos (espejo). En la Figura 5.2 se muestra un ejemplo de RAID 1 de dos discos.

![](img/5.2.png)

Esta estructura RAID proporciona una alta tolerancia a fallos. Si pierde un disco, tiene una copia de seguridad a la que se puede acceder inmediatamente. El principal problema de esta estructura RAID es su coste. Debe comprar una unidad duplicada por cada unidad que se incluirá en la matriz.
RAID 10 También llamada duplicación y división de discos o RAID 1+0, esta estructura RAID es una combinación de RAID 1 (duplicación) y RAID 0 (separación). Necesita un mínimo de cuatro discos: dos discos para la creación de bandas y dos discos para reflejar los discos de la creación de bandas. En la Figura 5.3 se muestra un ejemplo de RAID 10 de cuatro discos.

![](img/5.3.png)

Si bien esta estructura de matriz proporciona tolerancia a fallas, incluida una regeneración muy rápida de cualquier disco defectuoso, el costo es alto. Debe tener el doble de capacidad para la parte de la estructura de espejo.

RAID 2, 3, 4 Estas tres estructuras RAID normalmente ya no se utilizan, aunque es posible que todavía existan algunas matrices RAID 4. RAID 2 es una forma de RAID 0, que proporcionaba una comprobación de errores especializada que ahora gestionan las propias unidades de disco.

RAID 3 también es una forma de RAID 0, pero agrega datos de paridad y utiliza un mínimo de tres discos. Los datos de paridad se almacenan en un disco designado, llamado disco de paridad. Otros datos, como los datos de archivos, se almacenan en los otros dos discos. Se requiere un mínimo de tres discos. Si falla un solo disco de datos, los datos se pueden regenerar utilizando el otro disco de datos y el disco de paridad. Sin embargo, no hay regeneración si falla el disco de paridad.

La estructura RAID 4 es una forma de RAID 3 y también requiere un mínimo de tres discos. La diferencia es que proporciona un acceso más rápido que RAID 3, porque RAID 3 procesa bytes de datos, mientras que RAID 4 procesa bloques de datos. La estructura RAID 4 todavía tiene el defecto fatal de no regenerar los datos originales si falla el disco de paridad.

RAID 5 Esta estructura RAID también se denomina división de discos con paridad, porque divide tanto los datos como la paridad. Los datos de paridad no se escriben en una sola unidad, como en RAID 3 o RAID 4, sino que se distribuyen entre los discos. En la Figura 5.4 se muestra un ejemplo de RAID 5 de tres discos.

![](img/5.4.png)

RAID 5 se puede implementar mediante controladores de software o de hardware, pero normalmente se recomiendan controladores de hardware para implementaciones de RAID 5 de gran tamaño. Con un controlador de hardware, el rendimiento de escritura se puede mejorar agregando memoria caché adicional.

Para RAID 5, se requiere un mínimo de tres discos. Al distribuir la paridad entre las unidades, se mejora la tolerancia a fallos con respecto a RAID 3 y RAID 4 y se consiguen mejores tiempos de lectura de datos. Sin embargo, si falla una sola unidad, se necesita tiempo para reconstruir los datos de la unidad perdida. En ese tiempo, si otra unidad falla (y puede ocurrir), habrá perdido toda la matriz RAID. Por este motivo, muchas empresas con grandes instalaciones de datos no recomiendan una estructura RAID 5.

RAID 6 Esta estructura de matriz RAID también se denomina división de discos con doble paridad. Secciona tanto los datos como la paridad, como RAID 5, excepto que el mismo fragmento de datos de paridad se escribe dos veces, cada una en un disco diferente. Esto permite que dos unidades fallen sin problemas y aumenta su tolerancia a fallos. En la Figura 5.5 se muestra un ejemplo de RAID 6 de cuatro discos.

![](img/5.5.png)

Hay un requisito mínimo de cuatro discos para RAID 6, lo que lo hace un poco más caro que RAID 5. Además, las escrituras son ligeramente más lentas debido a la doble paridad. Sin embargo, esta estructura proporciona lecturas más rápidas, por lo que es útil para aplicaciones de datos de gran tamaño.

Es bueno tener opciones, y las diversas estructuras de matriz RAID ofrecen varias. Al comprender estas variedades de RAID y sus requisitos de datos particulares, puede elegir la estructura más aplicable para satisfacer las necesidades de sus sistemas.
### Implementación de RAID en Linux
Esta sección se centra en implementar y mantener una estructura RAID de Linux mediante software. Las matrices RAID de software de Linux se implementan a través del controlador de dispositivo Múltiples dispositivos (md) y son compatibles con RAID 0, 1, 10, 4, 5 y 6.
Antes de configurar una matriz RAID en Linux, debe verificar algunas cosas en su sistema. Además, debe preparar todas las unidades necesarias para ser miembros de la matriz RAID. Una vez que haya manejado estos preliminares, puede crear su matriz RAID. Una vez creada la matriz RAID, intervienen varias utilidades para administrarla. 
### Comprobando su sistema
El primer elemento que debe verificar en su sistema es si el kernel admite RAID. El kernel de Linux v2.6 y superior puede admitir todos los niveles de RAID. Puede verificar la versión de su kernel usando el comando `uname -r`, como se muestra aquí en una distribución de Ubuntu:

```sh
uname -r 
3.13.0–71-generic
```

Además, verifique si su sistema tiene el archivo `/proc/mdstat`. Este útil archivo proporciona información sobre el estado actual del RAID del sistema. Sólo su presencia es otro indicador positivo de que su sistema admite RAID:

```sh
ls /proc/mdstat
/proc/mdstat
```

Otra verificación utiliza el comando `modprobe` para ver si puede cargar varios módulos del kernel RAID. Usando privilegios de super usuario, escriba `modprobe raid6` en la línea de comando, como se muestra aquí:

```sh
sudo modprobe raid6
[sudo] password for christine:
```

No recibir ningún mensaje de error después de ejecutar este comando `modprobe` es una buena señal. Sin embargo, verifique que funcionó mostrando el contenido actual del `/proc/mdstat file`:

```sh
cat /proc/mdstat
Personalities: [raid6] [raid5] [raid4]
unused devices: <none> 
```

Observe que la línea Personalidades en el archivo `/proc/mdstat` de esta distribución de Ubuntu muestra tres niveles RAID diferentes: 6, 5 y 4. Esto indica que este sistema admite esos niveles RAID.

En este punto, puede verificar los niveles RAID adicionales admitidos continuando emitiendo `modprobe raid#`, donde `#` es el nivel RAID que desea verificar. Normalmente, encontrará que los niveles RAID 0, 1, 10, 4, 5 y 6 son compatibles con las distribuciones actuales de Linux sin ninguna modificación. Si un nivel no es compatible actualmente, recibirá un mensaje de error similar al siguiente:

```sh
sudo modprobe raid3
[sudo] password for christine:
modprobe: FATAL: Module raid3 not found.
```

Una vez que sepa que su sistema Linux puede admitir el nivel RAID deseado, deberá ver si su sistema tiene instalada la utilidad Administración de dispositivos o discos múltiples (`mdadm`). En esta distribución de Ubuntu, no está instalado de forma predeterminada:

```sh
dpkg -s mdadm
dpkg-query: package 'mdadm' is not installed and
 no information is available
[...]
```

Sin embargo, en este sistema CentOS, la utilidad `mdadm` está instalada de forma predeterminada:

```sh
rpm -qa | grep mdadm
mdadm-3.3.2–2.el7_1.1.x86_64 
```

Si no tiene la utilidad `mdadm` y necesita instalarla, su paquete se llama convenientemente `mdadm`. Entonces, por ejemplo, en un sistema Ubuntu puede instalarlo mediante el comando `sudo apt-get install mdadm`, asumiendo que tiene privilegios de super usuario.

Una vez que se completen estas comprobaciones del sistema y se realicen los cambios necesarios, puede continuar con la implementación de una matriz RAID. El siguiente paso implica las unidades de disco.
### Preparar una unidad para ser miembro de RAID
Antes de crear una matriz RAID, debe particionar las distintas unidades que serán miembros de la matriz. Pero antes de comenzar a particionar, debe pensar en algunas cuestiones importantes, como el código de tipo de partición que se utilizará, así como el tamaño de la partición y cuánto espacio en disco dejará sin particionar.

Una partición de disco de datos normal normalmente tiene un código de tipo de partición de 83 (para particiones MBR) o 8300 (para particiones GPT). Para un miembro de la matriz RAID, el código de tipo de partición se puede configurar en da (solo particiones MBR) o fd.

Deberá elegir el tipo de código correcto según la tabla de particiones y el _superbloque md_, a veces llamado _metadatos_. Cuando se crea una matriz RAID, de forma predeterminada, el superbloque md se escribe en una ubicación particular en todos los discos de la matriz. Actualmente, Linux reconoce dos grupos de versiones de md superblock, v0.90 y v1.0 y superiores. La principal diferencia entre estos dos grupos de versiones es la ubicación del superbloque en el disco. También ayudan a determinar qué tipo de código de partición utilizar.

Si está utilizando una tabla de particiones GPT, se recomienda el código de tipo fd (0xFD00), porque el sistema Linux puede detectar RAID automáticamente. Si su sistema utiliza md superblock v1.0 o superior (lo que suele ser el caso, si no ha creado una matriz RAID usando esta partición) y es una partición MBR, use el código de tipo de partición da (0xDA).

Lo ideal es que todas las unidades de la matriz RAID y las unidades de repuesto sean del mismo tamaño, pero no siempre es así. En situaciones en las que las unidades no tienen el mismo tamaño, puede ser una buena idea dejar algo de espacio sin particionar. Esto puede resultar útil si sus discos de repuesto son ligeramente más pequeños que los miembros de la unidad de matriz RAID y necesita usarlos para reemplazar una unidad de matriz defectuosa.

Para las unidades que se utilizarán en la misma matriz RAID (miembros y repuestos), haga que todas tengan el mismo tamaño de partición. El controlador del dispositivo md puede manejar diferentes tamaños de partición en una matriz RAID ignorando el exceso. Sin embargo, estarás desperdiciando ese espacio no coincidente.

Ahora que ha determinado el código de tipo de partición y el tamaño, está listo para particionar sus unidades. Utilice la herramienta de partición adecuada, como `fdisk` o `parted`, para crear las particiones necesarias. En el ejemplo recortado aquí, se particionan cinco unidades en una distribución CentOS utilizando privilegios de super usuario para prepararlas para la membresía en una matriz RAID:

```sh
lsblk

NAME       MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT 
sda         8:0    0    8G  0 disk
├─sda1      8:1    0  500M  0 part  /boot
└─sda2      8:2    0  7.5G  0 part
[...]

sde         8:64   0    1G  0 disk 
sdf         8:80   0    1G  0 disk 
sdg         8:96   0    1G  0 disk 
sdh         8:112  0    1G  0 disk 
sdi         8:128  0    1G  0 disk
[...]


fdisk /dev/sde
[...]
Command (m for help): n
Partition type:    
	p   primary (0 primary, 0 extended, 4 free)
	e   extended
Select (default p): p
Partition number (1–4, default 1): 1 
First sector (2048–2097151, default 2048):
Using default value 2048
[...]
Command (m for help): t
Selected partition 1
Hex code (type L to list all codes): da 
Changed type of partition 'Linux' to 'Non-FS data'

Command (m for help): w
[...]
fdisk /dev/sdf
[...]
fdisk /dev/sdg
[...]
fdisk /dev/sdh
[...]
fdisk /dev/sdi
[...]

lsblk
NAME       MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT 
sda         8:0    0    8G  0 disk
├─sda1      8:1    0  500M  0 part  /boot
└─sda2      8:2    0  7.5G  0 part
[...]
sde         8:64   0    1G  0 disk 
└─sde1      8:65   0 1023M  0 part sdf         8:80   0    1G  0 disk 
└─sdf1      8:81   0 1023M  0 part sdg         8:96   0    1G  0 disk 
└─sdg1      8:97   0 1023M  0 part sdh         8:112  0    1G  0 disk 
└─sdh1      8:113  0 1023M  0 part sdi         8:128  0    1G  0 disk 
└─sdi1      8:129  0 1023M  0 part
[...]
```

En este ejemplo, el comando `lsblk` se utiliza para mostrar todos los distintos dispositivos de bloque actualmente conectados al sistema. La utilidad `fdisk` se emplea para crear particiones de disco completas en cinco unidades. Observe que el código de tipo de partición utilizado es da (0xDA).

Una vez que haya verificado la compatibilidad con RAID de su sistema, haya instalado los paquetes necesarios y haya preparado las unidades necesarias para ser miembro de la matriz RAID, estará listo para la siguiente tarea: crear una matriz RAID.
### Creando una matriz RAID
Para configurar una matriz RAID, debe emplear la Administración de dispositivos o discos múltiples

(`mdadm`) utilidad. La sintaxis básica de esta herramienta flexible es `mdadm  [--mode] raid-device [opciones] componentes-dispositivos`

La utilidad `mdadm` es un programa único que realiza muchos trabajos relacionados con matrices RAID. Requiere privilegios de super usuario y tiene varios modos de funcionamiento. Cada modo de funcionamiento está diseñado para una función particular, como la creación de una matriz RAID. Además, cada modo tiene sus propias opciones de comando `mdadm` específicas. Puede elegir el modo de funcionamiento con la opción `--mode` y las sus opciones.

```
Options

Options for selecting a mode are:

-A, --assemble
Assemble a pre-existing array.

-B, --build
Build a legacy array without superblocks.

-C, --create
Create a new array.

-F, --follow, --monitor
Select Monitor mode.

-G, --grow
Change the size or shape of an active array.

-I, --incremental
Add/remove a single device to/from an appropriate array, and possibly start the array.

--auto-detect
Request that the kernel starts any auto-detected arrays. This can only work if _md_ is compiled into the kernel - not if it is a module. Arrays can be auto-detected by the kernel if all the components are in primary MS-DOS partitions with partition type FD, and all use v0.90 metadata. In-kernel autodetect is not recommended for new installations. Using _mdadm_ to detect and assemble arrays - possibly in an _initrd_ - is substantially more flexible and should be preferred.

If a device is given before any options, or if the first option is --add, --fail, or --remove, then the MANAGE mode is assumed. Anything other than these will cause the Misc mode to be assumed.
```

La atención se centra aquí en el modo de creación `mdadm`. Debido a que las unidades particionadas anteriormente no tenían superbloques, es necesario crear los superbloques en ellas. Una vez completado, las unidades se ensamblan en la configuración RAID deseada.

En el siguiente ejemplo recortado, cuatro (`-n 4`) de los discos previamente particionados se crean (`-C`) en una matriz RAID de nivel 6 de muestra (`-l 6`), designada por `/dev/md0`, en una distribución CentOS. El comando de ejemplo aquí está dividido en varias líneas para mayor claridad:

```
mdadm -C /dev/md0 -l 6 -n 4 \
> /dev/sdf1 /dev/sdg1 /dev/sdh1 /dev/sdi1 
mdadm: Defaulting to version 1.2 metadata 
mdadm: array /dev/md0 started. 
```

Si la utilidad encuentra algo en las particiones que sea un problema potencial, muestra un mensaje sobre el problema potencial junto con la pregunta: ¿Continuar creando matriz?. Si encuentra algún mensaje de problema con la utilidad `mdadm`, investigue a fondo antes de continuar con la creación de la matriz RAID.

Observe que en el ejemplo anterior, cuando la utilidad `mdadm` crea un superbloque en los nuevos miembros de la matriz RAID, utiliza de forma predeterminada los metadatos de la versión 1.2 (superbloque). Además, una vez que se escribe un superbloque en las particiones, se inicia la nueva matriz RAID, `/dev/md0`.

Cuando se creó la matriz RAID nivel 6 en el ejemplo anterior, se utilizaron opciones cortas en el comando `mdadm`. Puede utilizar las opciones largas, si lo desea.

Anteriormente mencionamos que cada modo de utilidad `mdadm` tiene su propio conjunto de opciones. Puede ver rápidamente estas opciones en la línea de comando ingresando al modo y luego escribiendo `--help`, como se muestra aquí:

```sh
mdadm --create --help 
Usage:  mdadm --create device -chunk=X --level=Y --raid-devices=Z devices
[...] 
Options that are valid with --create (-C) are:
--bitmap=            : Create a bitmap for the array with the given filename or an internal bitmap is 'internal' is given
 --chunk=         -c  : chunk size in kibibytes
 --rounding=          : rounding factor for linear array (==chunk size)
 --level=         -l  : raid level: 0,1,4,5,6,10,linear,multipath and synonyms
 --parity=        -p  : raid5/6 parity algorithm: {left,right}-{,a}symmetric
 --layout=            : same as --parity, for RAID10: [fno]NN
 --raid-devices=  -n  : number of active devices in array
 --spare-devices= -x  : number of spare (eXtra) devices in initial array
 --size=          -z  : Size (in K) of each drive in RAID1/4/5/6/10 - optional
 --data-offset=       : Space to leave between start of device and start of array data.  
 --force          -f  : Honour devices as listed on command line.  Dont insert a missing drive for RAID5.  
 --run            -R  : insist of running the array even if not all devices are present or some look odd.
 --readonly       -o  : start the array readonly - not supported yet.
 --name=          -N  : Textual name for array - max 32 characters  
 --bitmap-chunk=      : bitmap chunksize in Kilobytes.
 --delay=         -d  : bitmap update delay in seconds.
```

Esta opción `--help` es útil si necesita recuperar rápidamente la sintaxis de la opción de un modo en particular. Tenga en cuenta que el modo de detección automática no tiene opciones, por lo que al utilizar `--help` solo se mostrará información de ayuda general de `mdadm`.
### Comprobando una matriz RAID
Una vez que cree una matriz RAID, debe verificar inmediatamente para asegurarse de que todo esté bien. El archivo `/proc/mdstat` es útil aquí, porque contiene el estado actual de cualquier matriz RAID en ejecución. En este ejemplo, se muestra la información de estado actual de la matriz RAID nivel 6 `/dev/md0`:

```
cat /proc/mdstat
Personalities: [raid6] [raid5] [raid4]
md0: active raid6 sdi1[3] sdh1[2] sdg1[1] sdf1[0]
      2093056 blocks super 1.2 level 6, 512k chunk, [...]
unused devices: <none> #
```

El estado de la matriz RAID `/dev/md0` parece bueno. Las cuatro particiones participan activamente. También puede ver información sobre el nivel RAID de la matriz (nivel 6) y su tamaño de fragmento (512k).

Otra buena comprobación requiere el uso del modo misceláneo de la utilidad `mdadm`. A continuación se muestra un ejemplo de cómo verificar la muestra `/dev/md0 RAID array`:

```
mdadm --misc --detail  /dev/md0 /dev/md0:
        Version: 1.2
  Creation Time: Tue Feb  9 14:05:42 2017
     Raid Level: raid6
     Array Size: 2093056 (2044.34 MiB 2143.29 MB)
  Used Dev Size: 1046528 (1022.17 MiB 1071.64 MB)
   Raid Devices: 4
  Total Devices: 4
    Persistence: Superblock is persistent

    Update Time: Tue Feb  9 14:05:54 2017
          State: clean
 Active Devices: 4
Working Devices: 4
 Failed Devices: 0
  Spare Devices: 0
         Layout: left-symmetric
     Chunk Size: 512K
           Name: localhost.localdomain: [...]
           UUID: 38edfd0d:45092996:954b269a:9e919b3a
         Events: 17

Number   Major   Minor   RaidDevice State
0                      8       81        0      active sync   /dev/sdf1
1                      8       97        1      active sync   /dev/sdg1
2                      8      113        2      active sync   /dev/sdh1
3                      8      129        3      active sync   /dev/sdi1
```

Este comando proporciona una gran cantidad de información útil. Observe en el ejemplo anterior que no solo se proporciona información de estado, sino que también se muestra información de identificación, como el UUID. Estos datos pueden ayudarle a diagnosticar cualquier problema que haya ocurrido durante la creación de la matriz RAID.
### Formatee y monte la matriz RAID
Una vez que se ha creado (o ensamblado) y verificado una matriz RAID, se puede tratar como cualquier otra partición: formateándola con un sistema de archivos y montándola. En el ejemplo recortado aquí, puede ver que la matriz RAID 6 de muestra, `/dev/md0`, está formateada con un sistema de archivos ext4 y luego montada en un directorio temporal:

```sh
mkfs -t ext4 /dev/md0
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
[...]

mount -t ext4 /dev/md0 Temp
ls Temp
lost+found

touch Temp/My_RAID_File.txt

ls Temp
lost+found 
My_RAID_File.txt
```

En el ejemplo anterior, observe que el directorio `lost+found` está en el sistema de archivos `/dev/md0`, como lo vería en una partición no RAID formateada con el sistema de archivos ext4. Una vez que haya montado su matriz RAID en la ubicación permanente deseada, al igual que con otros sistemas de archivos, agregue un registro al archivo `/etc/fstab`, de modo que la matriz RAID se monte automáticamente en el momento del arranque del sistema.
### Guardar configuración de matriz RAID
Debido a que el kernel, el controlador `md` y `mdadm` pueden leer el superbloque de cada miembro RAID, no es absolutamente necesario un archivo de configuración. Además, al crear una matriz RAID, no se crea un archivo de configuración. Si existe un archivo de configuración RAID, la utilidad `mdadm` no lo actualiza automáticamente.

Sin embargo, es una buena idea crear y mantener un archivo de configuración RAID. Este archivo de utilidad `mdadm` es útil para una posible situación de recuperación de una matriz RAID, y algunas distribuciones de Linux producen errores cuando intenta ensamblar una matriz si no hay ningún archivo de configuración presente.

El archivo de configuración de `mdadm`, `mdadm.conf`, debe almacenarse en el directorio `/etc/` o en el directorio `/etc/mdadm/`, dependiendo de su distribución. Dado que no se crea cuando se instala la utilidad `mdadm`, deberá verificar qué ubicación del archivo de configuración utiliza su distribución. Puede averiguarlo escribiendo `man mdadm.conf` en la línea de comando..

Una vez que se determina la ubicación adecuada para su archivo de configuración, puede crearlo. La mejor manera de crear este archivo es utilizando la opción `--scan` de la utilidad `mdadm`. Primero, simplemente haga un escaneo simple para ver qué producirá el comando, como se muestra aquí en este ejemplo recortado:

```sh
mdadm --verbose --detail --scan /dev/md0
ARRAY /dev/md0 level=raid6 num-devices=4 metadata=1.2
name=localhost.localdomain:0 UUID=38edfd0d:45092996:954[...]
	devices=/dev/sdf1,/dev/sdg1,/dev/sdh1,/dev/sdi1
```

Esta es la información que debe almacenarse dentro de su archivo de configuración para esta matriz RAID en particular. Observe que la palabra clave `ARRAY` aparece con la información. Esta palabra clave se puede utilizar en el archivo `mdadm.conf` para identificar una matriz RAID.

En lugar de escribir esta información, lo que podría introducir errores tipográficos, redirija la salida estándar del comando al nombre de archivo de configuración adecuado, como se muestra aquí en esta distribución de CentOS:

```sh
ls /etc/mdadm.conf
ls: cannot access /etc/mdadm.conf: No such file or directory

mdadm --verbose --detail --scan /dev/md0 >> /etc/mdadm.conf

cat /etc/mdadm.conf
ARRAY /dev/md0 level=raid6 num-devices=4 metadata=1.2 name=localhost
	.localdomain:0 UUID=38edfd0d:45092996:954[...]    devices=/dev/sdf1,/dev/sdg1,/dev/sdh1,/dev/sdi1 #
```

Una vez que haya creado este archivo de configuración y/o haya almacenado en él la nueva información de la matriz RAID, habrá completado la fase de implementación de la matriz RAID. Sin embargo, puede modificar el archivo para agregar información de configuración adicional con fines de monitoreo. Hay muchas formas de monitorear y administrar su matriz RAID correctamente, algunas de las cuales incluyen modificar este archivo de configuración. Estos temas se tratan más apropiadamente en la fase de administración de una matriz RAID.
### Administrar una matriz RAID
Una vez que tenga su matriz RAID en producción, pasará a la fase de administración. La gestión de matrices RAID implica monitorearlas para detectar problemas, manejar cualquier dificultad, ajustar su configuración si es necesario, etc. 
### Monitoreo de su matriz RAID
Una de las tareas de administración de matrices RAID más importantes es la supervisión (también llamada _seguimiento_). La supervisión le permite tomar medidas rápidas cuando se producen problemas, mejorar el rendimiento del acceso a los datos y reducir las interrupciones.

La utilidad `mdadm` tiene un modo de monitor, que es fundamental para monitorear su matriz RAID controlada por software. Con este modo, puede monitorear sus conjuntos RAID para detectar ciertos eventos (también llamados _alertas_). 

```
       mdadm has several major modes of operation:

       Assemble

              Assemble the components of a previously created  array  into  an
              active  array.  Components  can  be  explicitly  given or can be
              searched for.  mdadm checks that the components do form  a  bona
              fide  array,  and can, on request, fiddle superblock information
              so as to assemble a faulty array.

       Build  Build an array that doesn’t have  per-device  superblocks.   For
              these  sorts  of  arrays,  mdadm  cannot  differentiate  between
              initial creation and subsequent assembly of an array.   It  also
              cannot  perform any checks that appropriate components have been
              requested.  Because of this, the Build mode should only be  used
              together with a complete understanding of what you are doing.

       Create Create a new array with per-device superblocks.

       Follow or Monitor
              Monitor  one  or  more  md devices and act on any state changes.
              This is only meaningful for raid1, 4,  5,  6,  10  or  multipath
              arrays,  as  only these have interesting state.  raid0 or linear
              never have missing, spare, or failed drives, so there is nothing
              to monitor.

       Grow   Grow  (or shrink) an array, or otherwise reshape it in some way.
              Currently supported growth options including changing the active
              size  of  component  devices  and  changing the number of active
              devices in RAID levels 1/4/5/6, as well as adding or removing  a
              write-intent bitmap.

       Incremental Assembly

              Add a single device to an appropriate array.  If the addition of
              the device makes the array runnable, the array will be  started.
              This  provides  a convenient interface to a hot-plug system.  As
              each device is detected, mdadm has a chance  to  include  it  in
              some array as appropriate.

       Manage This is for doing things to specific components of an array such
              as adding new spares and removing faulty devices.

       Misc   This is an ’everything else’ mode that  supports  operations  on
              active  arrays,  operations on component devices such as erasing
              old superblocks, and information gathering operations.

       Auto-detect
              This mode does not act on a specific device or array, but rather
              it  requests  the  Linux  Kernel  to  activate any auto-detected
              arrays.
```

El proceso de monitoreo se puede iniciar manualmente en la línea de comando. La sintaxis básica de la utilidad `mdadm` para iniciar el monitoreo es `mdadm --monitor options devices`
Puede sustituir `--follow` por `--monitor` en el comando. Este comando inicia `mdadm monitor`, donde examinará las matrices RAID cada 60 segundos (de forma predeterminada) e informará cualquier evento.

Tenga en cuenta que cuando la utilidad `mdadm` inicia su modo de monitoreo y encuentra matrices para monitorear, no saldrá. Por lo tanto, es una buena idea agregar un símbolo (`&`) al final del comando y ejecutarlo en segundo plano.

Puede configurar varias opciones con el modo monitor para satisfacer las necesidades de su sistema. Aquí se muestra una lista de las opciones del monitor `mdadm` en una distribución CentOS:

```sh
mdadm --monitor --help
[...] 
Options that are valid with the monitor (-F --follow) mode are:
 --mail=       -m  : Address to mail alerts of failure to
 --program=    -p  : Program to run when an event is detected
 --alert=          : same as --program
 --syslog      -y  : Report alerts via syslog
 --increment=  -r  : Report RebuildNN events in the given increment. default=20
 --delay=      -d  : seconds of delay between polling state. default=60
 --config=     -c  : specify a different config file
 --scan        -s  : find mail-address/program in config file
 --daemonise   -f  : Fork and continue in child, parent exits
 --pid-file=   -i  : In daemon mode write pid to specified file instead of stdout
 --oneshot     -1  : Check for degraded arrays, then exit
 --test        -t  : Generate a TestMessage event against each array at startup
```

La opción `--mail` le permite designar una única dirección de correo electrónico para recibir notificaciones de eventos. La opción `--program` designa un programa que se ejecutará tras una notificación de evento. Como alternativa al uso de estas opciones, puede usar la opción `--scan`, que hará que la utilidad `mdadm` busque estas configuraciones dentro del archivo de configuración `mdadm.conf`. Dentro del archivo de configuración, agrega la palabra clave `MAILADDR` seguida de una única dirección de correo electrónico. Además, puede agregar la palabra clave `PROGRAM` seguida del nombre de un programa o script de shell para ejecutar, en caso de que se produzca una alerta. Si usa la opción `--scan` y el archivo `mdadm.conf` no tiene palabras clave de programa o correo electrónico, o si inicia el modo de monitoreo sin las opciones `--mail` o `--program`, las notificaciones de eventos se envían a la salida estándar.

Otra opción interesante es `--daemonise`. Esto le permite iniciar `mdadm` en modo monitor como demonio. Esta útil opción se puede incluir en un script de inicio del sistema.
### Agregar un disco de repuesto a una matriz RAID
Puede agregar un disco de repuesto a una matriz RAID cuando la crea. Sin embargo, si no agregó uno (o más) en el momento de la creación, o si su disco de repuesto se ha convertido en un miembro RAID activo debido a una falla de otra unidad, es posible que desee agregar un disco de repuesto a una matriz RAID activa.

Cuando necesite agregar una unidad de repuesto a una matriz RAID, primero debe asegurarse de que no sea miembro de la matriz RAID. Es posible que esto no sea necesario para un solo sistema de matriz RAID, pero si tiene una instalación de matriz grande, vale la pena dedicar unos minutos adicionales. A continuación se muestra un ejemplo recortado de cómo verificar la pertenencia a una matriz en una unidad:

```sh
mdadm --misc --examine /dev/sde1
mdadm: No md superblock detected on /dev/sde1.

mdadm --misc --examine /dev/sdf1 
/dev/sdf1:
          Magic: a92b4efc
          Version: 1.2
[...]
```

Este ejemplo anterior muestra el resultado que recibe tanto para un miembro que no es RAID como para un miembro RAID activo. La partición `/dev/sde1` no es parte de una matriz RAID, pero la partición `/dev/sdf1` es un miembro de la matriz RAID. Tenga en cuenta que si la unidad aún no está particionada, deberá pasar el nombre completo de la unidad, `/dev/sde` en este caso, a la utilidad `mdadm` en lugar del nombre de la partición para verificar la membresía de RAID.

Antes de agregar un repuesto a su matriz RAID, verifique la cantidad actual de repuestos de la matriz usando el comando `grep`, junto con la opción `--detail` del modo misceláneo de la utilidad `mdadm`. Aquí se muestra un ejemplo:****

```sh
mdadm --misc --detail /dev/md0 | grep Spare
Spare Devices: 0
```

La matriz RAID `/dev/md0` actualmente no tiene unidades de repuesto. Para solucionar esta situación, la partición `/dev/sde1` se agrega en caliente aquí usando el modo de administración de la utilidad `mdadm`:

```sh
mdadm --manage --add /dev/md0 /dev/sde1
mdadm: added /dev/sde1

mdadm --misc --detail /dev/md0 | grep Spare
Spare Devices: 1
```

Notice that once the partition was added, the Spare Devices count went up by one. You can add more than one device at a time, if desired.
### Ampliación de la matriz RAID
Puede cambiar el tamaño o la forma de su matriz RAID utilizando la utilidad `mdadm`. _Tamaño_ o _forma_ se refiere a la capacidad de cambiar los elementos de configuración de la matriz RAID, como el tamaño del fragmento y el número de miembros activos de la matriz RAID. Incluso puede realizar conversiones, como cambiar una matriz RAID de nivel 5 a una matriz RAID de nivel 6.

El modo de crecimiento de la utilidad `mdadm` maneja estos diversos cambios. Tenga en cuenta que cambiar el tamaño y la forma de su matriz RAID requiere mucho tiempo (desde horas hasta días) y una actividad potencialmente peligrosa para los datos. Asegúrese siempre de haber completado las copias de seguridad antes de cualquier actividad en el modo de crecimiento. Para ver todas las opciones del modo de crecimiento, escriba `mdadm --grow --help` en la línea de comando
### Eliminación de una matriz RAID
Si lo desea, puede eliminar una matriz RAID completa. Para hacerlo, primero debe detener la matriz usando el modo de administración de la utilidad `mdadm`.

La matriz RAID `/dev/md0` de muestra se detiene en este ejemplo:

```sh
mdadm --manage --stop /dev/md0
mdadm: stopped /dev/md0
```

Una vez que se detiene una matriz RAID, sus miembros y unidades de repuesto se pueden eliminar eliminando su superbloque. Puede hacer esto una unidad a la vez o eliminar los superbloques de todas las unidades al mismo tiempo, como se muestra aquí:

```sh
mdadm --zero-superblock  /dev/sde1

mdadm --zero-superblock  /dev/sdf1 /dev/sdg1 /dev/sdh1
```

Una vez que se retira el superbloque de las unidades, se pueden emplear en otras matrices RAID o para otros fines. Asegúrese de actualizar el archivo de configuración `mdadm.conf` al eliminar cualquier matriz RAID.
### Ajuste de dispositivos de almacenamiento
Hoy en día, normalmente no es necesario ajustar sus dispositivos de almacenamiento. Sin embargo, es importante comprender estos conceptos y sus utilidades asociadas. Esto es especialmente cierto si se encuentra con una situación única que requiere modificar los atributos de un dispositivo de almacenamiento. 
### Analizando los conceptos de interfaz de unidad
Al considerar el ajuste de varios dispositivos de almacenamiento, tiene sentido revisar algunos conceptos básicos de la interfaz de la unidad. Los siguientes términos y conceptos le ayudarán a aprender a utilizar las utilidades de Linux creadas para ajustarlos.

**PATA**  _Parallel Advanced Technology Attachment (PATA)_, también llamado simplemente ATA o IDE (que aquí significa Integrated Drive Electronics), es una tecnología de interfaz de unidad que comenzó con el estándar ATA-1 en 1988. Depende de una cinta paralela. cables y proporciona velocidades de transferencia de hasta 133 MiB/segundo en modo ráfaga.

Históricamente en Linux, las unidades de disco PATA se indicaban mediante los archivos de dispositivo `/dev/hd*`. Actualmente, la mayoría de los controladores PATA tratan los discos PATA como si fueran discos SCSI, por lo que las unidades se indican mediante archivos de dispositivo `/dev/sd*`.

**SATA**  _Serial Advanced Technology Attachment (SATA)_ también es una tecnología de interfaz de unidad. Se considera un avance con respecto a la interfaz PATA debido a su uso de cables seriales, que no se ven obstaculizados por límites de longitud de cable como lo están los cables planos. SATA se configura automáticamente, permite Plug and Play (PnP) y proporciona velocidades de transferencia de hasta 6 Gbits/segundo. En Linux, las unidades de disco SATA se indican mediante archivos de dispositivo `/dev/sd*`.

**ATAPI**  _Interfaz de paquetes de conexión de tecnología avanzada (ATAPI)_ es un protocolo de interfaz de cinta y medios ópticos que utiliza interfaces de disco PATA o SATA. Introducido en 1997, era parte del estándar de interfaz de disco IDE mejorado (EIDE), que está fuertemente asociado con el estándar de interfaz de disco ATA-2 lanzado aproximadamente al mismo tiempo.

**SCSI**  _Small Computer System Interface (SCSI)_ es una tecnología de interfaz de unidad más antigua que comenzó a principios de los años 1980. Los dispositivos SCSI utilizan una interfaz paralela y son independientes de la plataforma. Los SCSI pueden transferir hasta 80 MB/segundo y admiten cable de fibra. En Linux, las unidades de disco SCSI, como las unidades SATA, se indican mediante archivos de dispositivo `/dev/sd*`.

**SAS**  Una versión más nueva de SCSI es _Serial Attached SCSI (SAS)_ y se está volviendo muy popular. Utiliza un controlador de puerto serie síncrono (SSP) que admite el protocolo de interfaz periférica serie (SPI). Los dispositivos SAS tienen un costo menor que los dispositivos SCSI tradicionales y brindan mayor confiabilidad, así como velocidades de transferencia en serie más rápidas. En Linux, las unidades de disco SAS, al igual que las unidades SCSI tradicionales, se indican mediante archivos de dispositivo `/dev/sd*`.

**iSCSI**  _Internet Small Computer System Interface (iSCSI)_ es un protocolo de transporte de red de almacenamiento. Los comandos SCSI, utilizando el protocolo iSCSI, se pueden enviar a dispositivos de almacenamiento remotos en redes locales o de área amplia e incluso a través de Internet. Cuando se configura, el disco de un servidor de almacenamiento SCSI aparece como un disco del lado del cliente conectado localmente. En Linux, las unidades de disco iSCSI, al igual que las unidades SCSI tradicionales, se indican mediante archivos de dispositivo `/dev/sd*`.

**AHCI**  La interfaz avanzada de controlador de host (ACHI) es una especificación heredada implementada en hardware que permite la comunicación de software con dispositivos SATA. Esta tecnología proporciona funciones estándar SATA avanzadas, como la conexión en caliente. También permite utilizar TRIM en unidades de estado sólido (SSD). El kernel de Linux admite el estándar AHCI desde la versión 2.6.19.

**NVMe**  Presentado en marzo de 2011, Non-Volatile Memory Express (NVMe) es un estándar creado originalmente por una asociación de más de 90 empresas. Actualmente está dirigido por un grupo promotor de 13 empresas. Específicamente, NVMe es una interfaz de dispositivo lógico y un conjunto de comandos estándar para SSD conectados a través del bus PCI Express. El kernel de Linux contiene un controlador de interfaz estándar NVMe desde la versión 3.3.

En Linux, los SSD con interfaz NVMe están representados por los archivos de dispositivo `/dev/nvme*`. Sin embargo, la convención de nomenclatura de archivos de dispositivo `/dev/nvme*` es ligeramente diferente a la convención de nomenclatura para unidades SATA y SCSI. El estándar NVMe utiliza una arquitectura de espacio de nombres, que es una capa superior adicional disponible para subdividir en particiones. Por ejemplo, aquí hay una referencia de archivo de dispositivo NVMe:

```sh
/dev/nmve0n1p1
```

El nmve indica que la unidad es un SSD estándar NVMe. El 0 en el nombre del archivo del dispositivo indica que esta es la primera unidad NVMe. El n1 indica que este es el espacio de nombres de la unidad. El p1 denota que esta es la partición 1 dentro del espacio de nombres uno de esta unidad.

Por lo tanto, la unidad NVMe aparece en primer lugar; el espacio de nombres es la subdivisión de la unidad; y la partición es una subdivisión del espacio de nombres. Si desea hacer referencia al tercer espacio de nombres y a la segunda partición de una segunda unidad NMVe, utilice el nombre de archivo del dispositivo `/dev/nvme1n3p2`.

Es importante comprender cómo ve el kernel de Linux las distintas interfaces de unidad, así como los archivos de dispositivo utilizados para acceder a ellas. La siguiente cuestión es cómo probar y ajustar estas distintas interfaces.
### Pruebas y ajustes de unidades
Un elemento que puede ajustar es el _acceso directo a memoria (DMA)_. DMA permite enviar datos directamente hacia/desde un dispositivo conectado hacia/desde la memoria del sistema. Esto permite que los procesadores se liberen de tener que lidiar con problemas de transferencia de datos, lo que a su vez puede acelerar el sistema. Para habilitar esta función, se requiere compatibilidad con DMA de la placa base, el BIOS y la unidad del sistema.

Otro elemento a ajustar es el almacenamiento en caché de reescritura. Cuando se utiliza el almacenamiento en caché con reescritura, una unidad almacena los datos que se escribirán en un búfer de caché antes de escribirlos físicamente en la unidad. Una vez que los datos están en la memoria caché, se le indica al sistema que los datos se han guardado en el disco. En ciertos escenarios de grandes volúmenes de datos con el almacenamiento en caché de reescritura habilitado, la unidad puede aceptar datos mucho más rápido que antes y mejora su velocidad de escritura. La desventaja es que una falla del sistema puede provocar la pérdida de datos no confirmados en el caché. Sin embargo, dado que la mayoría de los sistemas de archivos están registrados, el riesgo es mínimo.
### Using `hdparm`
La utilidad `hdparm` se diseñó originalmente para unidades PATA y dispositivos con interfaz de medios ópticos ATAPI. Sin embargo, también puede manejar almacenamiento SATA. Además, si sus dispositivos SCSI admiten traducción de comandos SCSI/ATA (SAT), también se pueden utilizar en ellos algunas opciones dentro de la utilidad `hdparm`.

Verifique si su sistema tiene instalada la utilidad `hdparm`. En Ubuntu, pruebe el comando `dpkg -s hdparm`. En un sistema Red Hat, como CentOS, utilizando privilegios de superusuario, ingrese el comando `rpm -qa | grep hdparm` en la línea de comando. Si su distribución no tiene instalada la utilidad `hdparm`, puede obtenerla del paquete `hdparm`.

Al utilizar `hdparm`, puede ver, probar y, si es necesario, modificar varias configuraciones de la unidad. Tenga en cuenta que la mayoría de las unidades vienen con su configuración óptima ya establecida.

Para fines de demostración aquí, en una distribución de Ubuntu, hemos configurado dos pequeñas unidades de muestra. Una es una unidad SATA y está representada por el archivo de dispositivo `/dev/sde`. La otra es una unidad PATA (IDE). Se trata como un dispositivo SCSI y está representado por el archivo de dispositivo `/dev/sda`.

Al usar `hdparm` con la opción `-I` en la unidad SATA, `/dev/sde`, puede obtener mucha información útil, como se muestra en la lista recortada aquí:

```sh
sudo hdparm -I /dev/sde
[sudo] password for christine:

/dev/sde:

ATA device, with non-removable media
[..]
...Serial Number:      VB3c70fec6-fd2c80f3
...Firmware Revision:  1.0 Standards:
...Used: ATA/ATAPI-6 published, ANSI INCITS 361–2002
...Supported: 6 5 4 
Configuration:
[...]
Capabilities:
[...]
   DMA: mdma0 mdma1 mdma2 udma0 udma1 udma2 udma3 udma4 
   udma5 *udma6
[...] 
control=120ns 
Commands/features:
   Enabled   Supported:
      *      Power Management feature set       
      *      Write cache
[...]
Checksum: correct
```

Observe que la caché de escritura está habilitada. El asterisco (*) junto a udma6 indica que este formulario DMA también está habilitado. Esto también funciona bien con la unidad PATA, `/dev/sda`, que Linux trata como un disco SCSI, como se muestra aquí:

```sh
$ sudo hdparm -I /dev/sda
[sudo] password for christine: 
/dev/sda:

ATA device, with non-removable media
[...]
   DMA: mdma0 mdma1 mdma2 udma0 udma1 *udma2 udma3 udma4
udma5 udma6
[...]    
Enabled   Supported:
      *      Power Management feature set       
      *      Write cache
[...]
```

Esta unidad utiliza una forma DMA diferente, `udma2`. Sin embargo, tiene habilitada la caché de escritura, al igual que la unidad `/dev/sde`.

Las diversas funciones de la utilidad `hdparm` pueden funcionar o no con unidades SCSI. En estos casos, la utilidad `sdparm` puede resultar útil.

Varias opciones de `hdparm` le permiten ver si una sola característica está configurada. A continuación se muestra un ejemplo de cómo verificar la configuración de devolución de caché de escritura en la unidad `/dev/sda`:

```sh
sudo hdparm -W /dev/sde
[sudo] password for christine:

/dev/sde:  write-caching =  1 (on)

sudo hdparm -W /dev/sda

/dev/sda:  
write-caching =  1 (on) $
```

Si por alguna razón desea desactivar el almacenamiento en caché de escritura, puede hacerlo fácilmente. Simplemente use la opción `-W` nuevamente como tal: `hdparm -W 0 /dev/device`. Muchas de las opciones de la utilidad `hdparm` utilizadas por sí mismas muestran la configuración actual y, si se usan con un parámetro de opción, cambian esa configuración.

Hay varias opciones disponibles con la utilidad `hdparm` para ver y establecer varias configuraciones de la unidad.

```
OPTIONS         

       When no options are given, -acdgkmur is assumed.  For "Get/set"
       options, a query without the optional parameter (e.g. -d) will
       query (get) the device state, and with a parameter (e.g., -d0)
       will set the device state.

       -a     Get/set sector count for filesystem (software) read-ahead.
              This is used to improve performance in sequential reads of
              large files, by prefetching additional blocks in
              anticipation of them being needed by the running task.
              
              Many IDE drives also have a separate built-in read-ahead
              function, which augments this filesystem (software) read-
              ahead function.

       -A     Get/set the IDE drive´s read-lookahead feature (usually ON
              by default).  Usage: -A0 (disable) or -A1 (enable).

       -b     Get/set bus state.

       -B     Get/set Advanced Power Management feature, if the drive
              supports it. A low value means aggressive power management
              and a high value means better performance.  Possible
              settings range from values 1 through 127 (which permit
              spin-down), and values 128 through 254 (which do not
              permit spin-down).  The highest degree of power management
              is attained with a setting of 1, and the highest I/O
              performance with a setting of 254.  A value of 255 tells
              hdparm to disable Advanced Power Management altogether on
              the drive (not all drives support disabling it, but most
              do).

       -c     Get/set (E)IDE 32-bit I/O support.  A numeric parameter
              can be used to enable/disable 32-bit I/O support.
              Currently supported values include 0 to disable 32-bit I/O
              support, 1 to enable 32-bit data transfers, and 3 to
              enable 32-bit data transfers with a special sync sequence
              required by many chipsets.  The value 3 works with nearly
              all 32-bit IDE chipsets, but incurs slightly more
              overhead.  Note that "32-bit" refers to data transfers
              across a PCI or VLB bus to the interface card only; all
              (E)IDE drives still have only a 16-bit connection over the
              ribbon cable from the interface card.

       -C     Check the current IDE power mode status, which will always
              be one of unknown (drive does not support this command),
              active/idle (normal operation), standby (low power mode,
              drive has spun down), or sleeping (lowest power mode,
              drive is completely shut down).  The -S, -y, -Y, and -Z
              options can be used to manipulate the IDE power modes.

       -d     Get/set the "using_dma" flag for this drive.  This option
              now works with most combinations of drives and PCI
              interfaces which support DMA and which are known to the
              kernel IDE driver.  It is also a good idea to use the
              appropriate -X option in combination with -d1 to ensure
              that the drive itself is programmed for the correct DMA
              mode, although most BIOSs should do this for you at boot
              time.  Using DMA nearly always gives the best performance,
              with fast I/O throughput and low CPU usage.  But there are
              at least a few configurations of chipsets and drives for
              which DMA does not make much of a difference, or may even
              slow things down (on really messed up hardware!).  Your
              mileage may vary.

       --dco-freeze
              DCO stands for Device Configuration Overlay, a way for
              vendors to selectively disable certain features of a
              drive.  The --dco-freeze option will freeze/lock the
              current drive configuration, thereby preventing software
              (or malware) from changing any DCO settings until after
              the next power-on reset.

       --dco-identify
              Query and dump information regarding drive configuration
              settings which can be disabled by the vendor or OEM
              installer.  These settings show capabilities of the drive
              which might be disabled by the vendor for "enhanced
              compatibility".  When disabled, they are otherwise hidden
              and will not show in the -I identify output.  For example,
              system vendors sometimes disable 48_bit addressing on
              large drives, for compatibility (and loss of capacity)
              with a specific BIOS.  In such cases, --dco-identify will
              show that the drive is 48_bit capable, but -I will not
              show it, and nor will the drive accept 48_bit commands.

       --dco-restore
              Reset all drive settings, features, and accessible
              capacities back to factory defaults and full capabilities.
              This command will fail if DCO is frozen/locked, or if a
              -Np maximum size restriction has also been set.  This is
              EXTREMELY DANGEROUS and will very likely cause massive
              loss of data.  DO NOT USE THIS COMMAND.

       --direct
              Use the kernel´s "O_DIRECT" flag when performing a -t
              timing test.  This bypasses the page cache, causing the
              reads to go directly from the drive into hdparm's buffers,
              using so-called "raw" I/O.  In many cases, this can
              produce results that appear much faster than the usual
              page cache method, giving a better indication of raw
              device and driver performance.

       --drq-hsm-error

              VERY DANGEROUS, DON'T EVEN THINK ABOUT USING IT.  This
              option causes hdparm to issue an IDENTIFY command to the
              kernel, but incorrectly marked as a "non-data" command.
              
              This results in the drive being left with its
              DataReQust(DRQ) line "stuck" high.  This confuses the
              kernel drivers, and may crash the system immediately with
              massive data loss.  The option exists to help in testing
              and fortifying the kernel against similar real-world drive
              malfunctions.  VERY DANGEROUS, DO NOT USE!!

       -D     Enable/disable the on-drive defect management feature,
              whereby the drive firmware tries to automatically manage
              defective sectors by relocating them to "spare" sectors
              reserved by the factory for such.  Control of this feature
              via the -D option is not supported for most modern drives
              since ATA-4; thus this command may fail.

       -E     Set cd/dvd drive speed.  This is NOT necessary for regular
              operation, as the drive will automatically switch speeds
              on its own.  But if you want to play with it, just supply
              a speed number after the option, usually a number like 2
              or 4.  This can be useful in some cases, though, to smooth
              out DVD video playback.

       -f     Sync and flush the buffer cache for the device on exit.
              This operation is also performed internally as part of the
              -t and -T timings and other options.

       --fallocate
              This option currently works only on ext4 and xfs
              filesystem types.  When used, this must be the only option
              given.  It requires two parameters: the desired file size
              in kilo-bytes (byte count divided by 1024), followed by
              the pathname for the new file.  It will create a new file
              of the specified size, but without actually having to
              write any data to the file.  This will normally complete
              very quickly, and without thrashing the storage device.
              E.g. Create a 10KByte file: hdparm --fallocate 10
              temp_file

       --fibmap
              When used, this must be the only option given.  It
              requires a file path as a parameter, and will print out a
              list of the block extents (sector ranges) occupied by that
              file on disk.  Sector numbers are given as absolute LBA
              numbers, referenced from sector 0 of the physical device
              rather than from the partition or filesystem.  This
              information can then be used for a variety of purposes,
              such as examining the degree of fragmenation of larger
              files, or determining appropriate sectors to deliberately
              corrupt during fault-injection testing procedures.
              
              This option uses the new FIEMAP (file extent map) ioctl()
              when available, and falls back to the older FIBMAP (file
              block map) ioctl() otherwise.  Note that FIBMAP suffers
              from a 32-bit block-number interface, and thus not work
              beyond 8TB or 16TB.  FIBMAP is also very slow, and does
              not deal well with preallocated uncommitted extents in
              ext4/xfs filesystems, unless a sync() is done before using
              this option.

       --fwdownload
              When used, this should be the only option given.  It
              requires a file path immediately after the option,
              indicating where the new drive firmware should be read
              from.  The contents of this file will be sent to the drive
              using the (S)ATA DOWNLOAD MICROCODE command, using either
              transfer protocol 7 (entire file at once), or, if the
              drive supports it, transfer protocol 3 (segmented
              download).  This command is EXTREMELY DANGEROUS and could
              destroy both the drive and all data on it.  DO NOT USE
              THIS COMMAND.  The --fwdownload-mode3 , --fwdownload-
              mode3-max , and --fwdownload-mode7 variations on basic
              --fwdownload allow overriding automatic protocol detection
              in favour of forcing hdparm to use a specific transfer
              protocol, for testing purposes only.

       -F     Flush the on-drive write cache buffer (older drives may
              not implement this).

       -g     Display the drive geometry (cylinders, heads, sectors),
              the size (in sectors) of the device, and the starting
              offset (in sectors) of the device from the beginning of
              the drive.

       -h     Display terse usage information (help).

       -H     Read the temperature from some (mostly Hitachi) drives.
              Also reports if the temperature is within operating
              condition range (this may not be reliable). Does not cause
              the drive to spin up if idle.

       -i     Display the identification info which the kernel drivers
              (IDE, libata) have stored from boot/configuration time.
              This may differ from the current information obtainable
              directly from the drive itself with the -I option.  The
              data returned may or may not be current, depending on
              activity since booting the system.  For a more detailed
              interpretation of the identification info, refer to AT
              Attachment Interface for Disk Drives, ANSI ASC X3T9.2
              working draft, revision 4a, April 19/93, and later
              editions.

       --idle-immediate
              Issue an ATA IDLE_IMMEDIATE command, to put the drive into
              a lower power state.  Usually the device remains spun-up.

       --idle-unload
              Issue an ATA IDLE_IMMEDIATE_WITH_UNLOAD command, to unload
              or park the heads and put the drive into a lower power
              state.  Usually the device remains spun-up.

       -I     Request identification info directly from the drive, which
              is displayed in a new expanded format with considerably
              more detail than with the older -i option.

       --Iraw <pathname>
              This option dumps the drive's identify data in raw binary
              to the specified file.

       --Istdin
              This is a special variation on the -I option, which
              accepts a drive identification block as standard input
              instead of using a /dev/hd* parameter.  The format of this
              block must be exactly the same as that found in the
              /proc/ide/*/hd*/identify "files", or that produced by the
              --Istdout option described below.  This variation is
              designed for use with collected "libraries" of drive
              identification information, and can also be used on ATAPI
              drives which may give media errors with the standard
              mechanism.  When --Istdin is used, it must be the *only*
              parameter given.

       --Istdout
              This option dumps the drive's identify data in hex to
              stdout, in a format similar to that from
              /proc/ide/*/identify, and suitable for later use with the
              --Istdin option.

       -J     Get/set the Western Digital (WD) Green Drive's "idle3"
              timeout value.  This timeout controls how often the drive
              parks its heads and enters a low power consumption state.
              
              The factory default is eight (8) seconds, which is a very
              poor choice for use with Linux.  Leaving it at the default
              will result in hundreds of thousands of head load/unload
              cycles in a very short period of time.  The drive
              mechanism is only rated for 300,000 to 1,000,000 cycles,
              so leaving it at the default could result in premature
              failure, not to mention the performance impact of the
              drive often having to wake-up before doing routine I/O.
              
              WD supply a WDIDLE3.EXE DOS utility for tweaking this
              setting, and you should use that program instead of hdparm
              if at all possible.  The reverse-engineered implementation
              in hdparm is not as complete as the original official
              program, even though it does seem to work on at a least a
              few drives.  A full power cycle is required for any change
              in setting to take effect, regardless of which program is
              used to tweak things.
              
              A setting of 30 seconds is recommended for Linux use.
              
              Permitted values are from 8 to 12 seconds, and from 30 to
              300 seconds in 30-second increments.  Specify a value of
              zero (0) to disable the WD idle3 timer completely (NOT
              RECOMMENDED!).

       -k     Get/set the "keep_settings_over_reset" flag for the drive.
              When this flag is set, the drive will preserve the -dmu
              settings over a soft reset, (as done during the error
              recovery sequence).  This option defaults to off, to
              prevent drive reset loops which could be caused by
              combinations of -dmu settings.  The -k option should
              therefore only be set after one has achieved confidence in
              correct system operation with a chosen set of
              configuration settings.  In practice, all that is
              typically necessary to test a configuration (prior to
              using -k) is to verify that the drive can be read/written,
              and that no error logs (kernel messages) are generated in
              the process (look in /var/log/messages on most systems).

       -K     Set the drive´s "keep_features_over_reset" flag.  Setting
              this enables the drive to retain the settings for -APSWXZ
              over a soft reset (as done during the error recovery
              sequence).  Not all drives support this feature.

       -L     Set the drive´s doorlock flag.  Setting this to 1 will
              lock the door mechanism of some removable hard drives
              (e.g. Syquest, ZIP, Jazz..), and setting it to 0 will
              unlock the door mechanism.  Normally, Linux maintains the
              door locking mechanism automatically, depending on drive
              usage (locked whenever a filesystem is mounted).  But on
              system shutdown, this can be a nuisance if the root
              partition is on a removable disk, since the root partition
              is left mounted (read-only) after shutdown.  So, by using
              this command to unlock the door after the root filesystem
              is remounted read-only, one can then remove the cartridge
              from the drive after shutdown.

       -m     Get/set sector count for multiple sector I/O on the drive.
              A setting of 0 disables this feature.  Multiple sector
              mode (aka IDE Block Mode), is a feature of most modern IDE
              hard drives, permitting the transfer of multiple sectors
              per I/O interrupt, rather than the usual one sector per
              interrupt.  When this feature is enabled, it typically
              reduces operating system overhead for disk I/O by 30-50%.
              On many systems, it also provides increased data
              throughput of anywhere from 5% to 50%.  Some drives,
              however (most notably the WD Caviar series), seem to run
              slower with multiple mode enabled.  Your mileage may vary.
              Most drives support the minimum settings of 2, 4, 8, or 16
              (sectors).  Larger settings may also be possible,
              depending on the drive.  A setting of 16 or 32 seems
              optimal on many systems.  Western Digital recommends lower
              settings of 4 to 8 on many of their drives, due tiny
              (32kB) drive buffers and non-optimized buffering
              algorithms.  The -i option can be used to find the maximum
              setting supported by an installed drive (look for
              MaxMultSect in the output).  Some drives claim to support
              multiple mode, but lose data at some settings.  Under rare
              circumstances, such failures can result in massive
              filesystem corruption.

       --make-bad-sector
              Deliberately create a bad sector (aka. "media error") on
              the disk.  EXCEPTIONALLY DANGEROUS. DO NOT USE THIS
              OPTION!!  This can be useful for testing of device/RAID
              error recovery mechanisms.  The sector number is given as
              a (base10) parameter after the option.  Depending on the
              device, hdparm will choose one of two possible ATA
              commands for corrupting the sector.  The WRITE_LONG works
              on most drives, but only up to the 28-bit sector boundary.
              Some very recent drives (2008) may support the new
              WRITE_UNCORRECTABLE_EXT command, which works for any LBA48
              sector.  If available, hdparm will use that in preference
              to WRITE_LONG.  The WRITE_UNCORRECTABLE_EXT command itself
              presents a choice of how the new bad sector should behave.
              By default, it will look like any other bad sector, and
              the drive may take some time to retry and fail on
              subsequent READs of the sector.  However, if a single
              letter f is prepended immediately in front of the first
              digit of the sector number parameter, then hdparm will
              issue a "flagged" WRITE_UNCORRECTABLE_EXT, which causes
              the drive to merely flag the sector as bad (rather than
              genuinely corrupt it), and subsequent READs of the sector
              will fail immediately (rather than after several retries).
              
              Note also that the --repair-sector option can be used to
              restore (any) bad sectors when they are no longer needed,
              including sectors that were genuinely bad (the drive will
              likely remap those to a fresh area on the media).

       -M     Get/set Automatic Acoustic Management (AAM) setting. Most
              modern harddisk drives have the ability to speed down the
              head movements to reduce their noise output.  The possible
              values are between 0 and 254. 128 is the most quiet (and
              therefore slowest) setting and 254 the fastest (and
              loudest). Some drives have only two levels (quiet / fast),
              while others may have different levels between 128 and
              254.  At the moment, most drives only support 3 options,
              off, quiet, and fast.  These have been assigned the values
              0, 128, and 254 at present, respectively, but integer
              space has been incorporated for future expansion, should
              this change.

       -n     Get or set the "ignore_write_errors" flag in the driver.
              Do NOT play with this without grokking the driver source
              code first.

       -N     Get/set max visible number of sectors, also known as the
              Host Protected Area setting.  Without a parameter, -N
              displays the current setting, which is reported as two
              values: the first gives the current max sectors setting,
              and the second shows the native (real) hardware limit for
              the disk.  The difference between these two values
              indicates how many sectors of the disk are currently
              hidden from the operating system, in the form of a Host
              Protected Area (HPA).  This area is often used by computer
              makers to hold diagnostic software, and/or a copy of the
              originally provided operating system for recovery
              purposes.  Another possible use is to hide the true
              capacity of a very large disk from a BIOS/system that
              cannot normally cope with drives of that size (eg. most
              current {2010} BIOSs cannot deal with drives larger than
              2TB, so an HPA could be used to cause a 3TB drive to
              report itself as a 2TB drive).  To change the current max
              (VERY DANGEROUS, DATA LOSS IS EXTREMELY LIKELY), a new
              value should be provided (in base10) immediately following
              the -N option.  This value is specified as a count of
              sectors, rather than the "max sector address" of the
              drive.  Drives have the concept of a temporary (volatile)
              setting which is lost on the next hardware reset, as well
              as a more permanent (non-volatile) value which survives
              resets and power cycles.  By default, -N affects only the
              temporary (volatile) setting.  To change the permanent
              (non-volatile) value, prepend a leading p character
              immediately before the first digit of the value.  Drives
              are supposed to allow only a single permanent change per
              session.  A hardware reset (or power cycle) is required
              before another permanent -N operation can succeed.  Note
              that any attempt to set this value may fail if the disk is
              being accessed by other software at the same time.  This
              is because setting the value requires a pair of back-to-
              back drive commands, but there is no way to prevent some
              other command from being inserted between them by the
              kernel.  So if it fails initially, just try again.  Kernel
              support for -N is buggy for many adapter types across many
              kernel versions, in that an incorrect (too small) max size
              value is sometimes reported.  As of the 2.6.27 kernel,
              this does finally seem to be working on most hardware.

       --offset
              Offsets to given number of GiB (1024*1024*1024) when
              performing -t timings of device reads.  Speed changes
              (about twice) along many mechanical drives.  Usually the
              maximum is at the beginning, but not always.  Solid-state
              drives (SSDs) should show similar timings regardless of
              offset.

       -p     Attempt to reprogram the IDE interface chipset for the
              specified PIO mode, or attempt to auto-tune for the "best"
              PIO mode supported by the drive.  This feature is
              supported in the kernel for only a few "known" chipsets,
              and even then the support is iffy at best.  Some IDE
              chipsets are unable to alter the PIO mode for a single
              drive, in which case this option may cause the PIO mode
              for both drives to be set.  Many IDE chipsets support
              either fewer or more than the standard six (0 to 5) PIO
              modes, so the exact speed setting that is actually
              implemented will vary by chipset/driver sophistication.
              
              Use with extreme caution!  This feature includes zero
              protection for the unwary, and an unsuccessful outcome may
              result in severe filesystem corruption!

       -P     Set the maximum sector count for the drive´s internal
              prefetch mechanism.  Not all drives support this feature,
              and it was dropped from the official spec as of ATA-4.

       --prefer-ata12
              When using the SAT (SCSI ATA Translation) protocol, hdparm
              normally prefers to use the 16-byte command format
              whenever possible.  But some USB drive enclosures don't
              work correctly with 16-byte commands.  This option can be
              used to force use of the smaller 12-byte command format
              with such drives.  hdparm will still revert to 16-byte
              commands for things that cannot be done with the 12-byte
              format (e.g. sector accesses beyond 28-bits).

       -q     Handle the next option quietly, suppressing normal output
              (but not error messages).  This is useful for reducing
              screen clutter when running from system startup scripts.
              Not applicable to the -i or -v or -t or -T options.

       -Q     Get or set the device's command queue_depth, if supported
              by the hardware.  This only works with 2.6.xx (or later)
              kernels, and only with device and driver combinations
              which support changing the queue_depth.  For SATA disks,
              this is the Native Command Queuing (NCQ) queue depth.

       -r     Get/set read-only flag for the device.  When set, Linux
              disallows write operations on the device.

       -R     Get/set Write-Read-Verify feature, if the drive supports
              it.  Usage: -R0 (disable) or -R1 (enable).  This feature
              is intended to have the drive firmware automatically read-
              back any data that is written by software, to verify that
              the data was successfully written.  This is generally
              overkill, and can slow down disk writes by as much as a
              factor of two (or more).

       --read-sector
              Reads from the specified sector number, and dumps the
              contents in hex to standard output.  The sector number
              must be given (base10) after this option.  hdparm will
              issue a low-level read (completely bypassing the usual
              block layer read/write mechanisms) for the specified
              sector.  This can be used to definitively check whether a
              given sector is bad (media error) or not (doing so through
              the usual mechanisms can sometimes give false positives).

       --repair-sector
              This is an alias for the --write-sector option.  VERY
              DANGEROUS.

       -s     Enable/disable the power-on in standby feature, if
              supported by the drive.  VERY DANGEROUS.  Do not use
              unless you are absolutely certain that both the system
              BIOS (or firmware) and the operating system kernel (Linux
              >= 2.6.22) support probing for drives that use this
              feature.  When enabled, the drive is powered-up in the
              standby mode to allow the controller to sequence the spin-
              up of devices, reducing the instantaneous current draw
              burden when many drives share a power supply.  Primarily
              for use in large RAID setups.  This feature is usually
              disabled and the drive is powered-up in the active mode
              (see -C above).  Note that a drive may also allow enabling
              this feature by a jumper.  Some SATA drives support the
              control of this feature by pin 11 of the SATA power
              connector. In these cases, this command may be unsupported
              or may have no effect.

       -S     Put the drive into idle (low-power) mode, and also set the
              standby (spindown) timeout for the drive.  This timeout
              value is used by the drive to determine how long to wait
              (with no disk activity) before turning off the spindle
              motor to save power.  Under such circumstances, the drive
              may take as long as 30 seconds to respond to a subsequent
              disk access, though most drives are much quicker.  The
              encoding of the timeout value is somewhat peculiar.  A
              value of zero means "timeouts are disabled": the device
              will not automatically enter standby mode.  Values from 1
              to 240 specify multiples of 5 seconds, yielding timeouts
              from 5 seconds to 20 minutes.  Values from 241 to 251
              specify from 1 to 11 units of 30 minutes, yielding
              timeouts from 30 minutes to 5.5 hours.  A value of 252
              signifies a timeout of 21 minutes. A value of 253 sets a
              vendor-defined timeout period between 8 and 12 hours, and
              the value 254 is reserved.  255 is interpreted as 21
              minutes plus 15 seconds.  Note that some older drives may
              have very different interpretations of these values.

       -t     Perform timings of device reads for benchmark and
              comparison purposes.  For meaningful results, this
              operation should be repeated 2-3 times on an otherwise
              inactive system (no other active processes) with at least
              a couple of megabytes of free memory.  This displays the
              speed of reading through the buffer cache to the disk
              without any prior caching of data.  This measurement is an
              indication of how fast the drive can sustain sequential
              data reads under Linux, without any filesystem overhead.
              
              To ensure accurate measurements, the buffer cache is
              flushed during the processing of -t using the BLKFLSBUF
              ioctl.

       -T     Perform timings of cache reads for benchmark and
              comparison purposes.  For meaningful results, this
              operation should be repeated 2-3 times on an otherwise
              inactive system (no other active processes) with at least
              a couple of megabytes of free memory.  This displays the
              speed of reading directly from the Linux buffer cache
              without disk access.  This measurement is essentially an
              indication of the throughput of the processor, cache, and
              memory of the system under test.

       --trim-sector-ranges
              For Solid State Drives (SSDs).  EXCEPTIONALLY DANGEROUS.
              DO NOT USE THIS OPTION!!  Tells the drive firmware to
              discard unneeded data sectors, destroying any data that
              may have been present within them.  This makes those
              sectors available for immediate use by the firmware's
              garbage collection mechanism, to improve scheduling for
              wear-leveling of the flash media.  This option expects one
              or more sector range pairs immediately after the option:
              an LBA starting address, a colon, and a sector count (max
              65535), with no intervening spaces.  EXCEPTIONALLY
              DANGEROUS. DO NOT USE THIS OPTION!!

              E.g.  hdparm --trim-sector-ranges 1000:4 7894:16 /dev/sdz

       --trim-sector-ranges-stdin
              Identical to --trim-sector-ranges above, except the list
              of lba:count pairs is read from stdin rather than being
              specified on the command line.  This can be used to avoid
              problems with excessively long command lines.  It also
              permits batching of many more sector ranges into single
              commands to the drive, up to the currently configured
              transfer limit (max_sectors_kb).

       -u     Get/set the interrupt-unmask flag for the drive.  A
              setting of 1 permits the driver to unmask other interrupts
              during processing of a disk interrupt, which greatly
              improves Linux´s responsiveness and eliminates "serial
              port overrun" errors.  Use this feature with caution: some
              drive/controller combinations do not tolerate the
              increased I/O latencies possible when this feature is
              enabled, resulting in massive filesystem corruption.  In
              particular, CMD-640B and RZ1000 (E)IDE interfaces can be
              unreliable (due to a hardware flaw) when this option is
              used with kernel versions earlier than 2.0.13.  Disabling
              the IDE prefetch feature of these interfaces (usually a
              BIOS/CMOS setting) provides a safe fix for the problem for
              use with earlier kernels.

       -v     Display some basic settings, similar to -acdgkmur for IDE.
              This is also the default behaviour when no options are
              specified.

       -V     Display program version and exit immediately.
       
       --verbose
              Display extra diagnostics from some commands.

       -w     Perform a device reset (DANGEROUS).  Do NOT use this
              option.  It exists for unlikely situations where a reboot
              might otherwise be required to get a confused drive back
              into a useable state.

       --write-sector
              Writes zeros to the specified sector number.  VERY
              DANGEROUS.  The sector number must be given (base10) after
              this option.  hdparm will issue a low-level write
              (completely bypassing the usual block layer read/write
              mechanisms) to the specified sector.  This can be used to
              force a drive to repair a bad sector (media error).

       -W     Get/set the IDE/SATA drive´s write-caching feature.

       -X     Set the IDE transfer mode for (E)IDE/ATA drives.  This is
              typically used in combination with -d1 when enabling DMA
              to/from a drive on a supported interface chipset, where -X
              mdma2 is used to select multiword DMA mode2 transfers and
              -X sdma1 is used to select simple mode 1 DMA transfers.
              
              With systems which support UltraDMA burst timings, -X
              udma2 is used to select UltraDMA mode2 transfers (you´ll
              need to prepare the chipset for UltraDMA beforehand).
              Apart from that, use of this option is seldom necessary
              since most/all modern IDE drives default to their fastest
              PIO transfer mode at power-on.  Fiddling with this can be
              both needless and risky.  On drives which support
              alternate transfer modes, -X can be used to switch the
              mode of the drive only.  Prior to changing the transfer
              mode, the IDE interface should be jumpered or programmed
              (see -p option) for the new mode setting to prevent loss
              and/or corruption of data.  Use this with extreme caution!
              For the PIO (Programmed Input/Output) transfer modes used
              by Linux, this value is simply the desired PIO mode number
              plus 8.  Thus, a value of 09 sets PIO mode1, 10 enables
              PIO mode2, and 11 selects PIO mode3.  Setting 00 restores
              the drive´s "default" PIO mode, and 01 disables IORDY.
              For multiword DMA, the value used is the desired DMA mode
              number plus 32.  for UltraDMA, the value is the desired
              UltraDMA mode number plus 64.

       -y     Force an IDE drive to immediately enter the low power
              consumption standby mode, usually causing it to spin down.
              The current power mode status can be checked using the -C
              option.

       -Y     Force an IDE drive to immediately enter the lowest power
              consumption sleep mode, causing it to shut down
              completely.  A hard or soft reset is required before the
              drive can be accessed again (the Linux IDE driver will
              automatically handle issuing a reset if/when needed).  The
              current power mode status can be checked using the -C
              option.

       -z     Force a kernel re-read of the partition table of the
              specified device(s).

       -Z     Disable the automatic power-saving function of certain
              Seagate drives (ST3xxx models?), to prevent them from
              idling/spinning-down at inconvenient times.
```

Una de las opciones de hdparm más útiles (y no peligrosas) es para probar el rendimiento de la unidad. Es mejor utilizar estas pruebas cuando la unidad esté inactiva. Aquí se prueba una unidad de distribución de Ubuntu tanto para lecturas de dispositivo como de caché:

```sh
sudo hdparm -tT /dev/sde\
[sudo] password for christine:

 /dev/sde:
Timing cached reads:   11810 MB in 2.00 seconds=5916.78 MB/sec
Timing buffered disk reads: 1024 MB in 2.69 seconds=380.94 MB/sec

sudo hdparm -tT /dev/sda

 /dev/sda:
Timing cached reads:   10996 MB in 2.00 seconds=5504.82 MB/sec
Timing buffered disk reads: 992 MB in 3.00 seconds=330.43 MB/sec
```

Por supuesto, una sola prueba no le proporcionará datos precisos. Es posible que desee realizar estas pruebas varias veces y promediar sus resultados.
### Usando `sdparm`

A veces se hace referencia a la utilidad `sdparm` como “`hdparm` para SCSI”, pero ese no es el caso. La utilidad `sdparm` es muy diferente de `hdparm` en la forma en que adquiere información y establece varios parámetros.

La utilidad `sdparm` extrae información de las tablas de datos vitales del producto (VPD) de un dispositivo SCSI. La información de VPD incluye elementos como números de pieza, números de serie y conjuntos de códigos.

También puede utilizar la utilidad `sdparm` para controlar el comportamiento de un dispositivo SCSI. Por ejemplo, puede desactivar una unidad SCSI y modificar su caché de reescritura.

Hay muchas opciones disponibles con la utilidad `sdparm` para ver y establecer varias configuraciones de la unidad. 

| **long option format** | **short option format** | **description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --all                  | -a                      | list all known (generic or transport) parameters for given _DEVICE_. When this utility is invoked with no options then only common generic mode parameters are output.                                                                                                                                                                                                                                                                                                                                                        |
| --clear=_STR_          | -c _STR_                | clear (zero) parameter(s) in _STR_. The default action to clear can be overridden, see below.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --command=_CMD_        | -C _CMD_                | perform _CMD_ which is one of: capacity, eject, load, ready, sense, start, stop, sync or unlock                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --dbd                  | -B                      | set the DBD (disable block descriptors) bit in each MODE SENSE cdb                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --defaults             | -D                      | fetch the default values for the given mode page and use them to overwrite the current values. Note that the saved values are not overwritten unless the '--save' option is also given.                                                                                                                                                                                                                                                                                                                                       |
| --dummy                | -d                      | when used with '--set' or '--clear' does all the preparation and sanity checks but bypasses the final stage of sending the changes to the device. [That is, it skips the MODE SELECT command.]                                                                                                                                                                                                                                                                                                                                |
| --enumerate            | -e                      | fetch information from the sdparm's internal tables. If a _DEVICE_ name is given then it will be ignored. May be used in conjunction with '--all', '--inquiry', '--long',  '--page=',  '--transport=' and/or '--vendor='.                                                                                                                                                                                                                                                                                                     |
| --examine              | -E                      | probes all mode or VPD pages. For mode pages only those with known field names are probed when the --all option is given. For VPD pages only those pages listed in "Supported VPD pages page" are decoded. In both cases some pages may be missed.                                                                                                                                                                                                                                                                            |
| --flexible             | -f                      | check mode sense responses for sanity and if broken, try to fix them if possible. Also allows mode pages whose peripheral type mismatches the given _DEVICE_ to be processed.                                                                                                                                                                                                                                                                                                                                                 |
| --get=_STR_            | -g _STR_                | fetch parameter(s) in _STR_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --help                 | -h                      | output a usage message then exits                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --hex                  | -H                      | rather than decode a (mode or VPD) page, it is output in ASCII hex. If used with the '--get' option then the parameter is output in hexadecimal. May be invoked multiple times.                                                                                                                                                                                                                                                                                                                                               |
| --inhex=_FN_           | -I _FN_                 | read ASCII hex from file _FN_ (and ignore _DEVICE)_ and decode as mode or VPD page(s). Reads from stdin if _FN_ is '-'. Treats the contents of _FN_ as binary if '--raw' is also given.                                                                                                                                                                                                                                                                                                                                       |
| --inquiry              | -i                      | fetch a VPD page, decode and output it. If no '--page=' is given then the device identification VPD page is fetched.  Add '-ll' to get standard INQUIRY response data decoded in more detail.                                                                                                                                                                                                                                                                                                                                 |
| --long                 | -l                      | Add extra information to the output. For example a line showing the setting of the WCE parameter will have "Write cache enable" appended to it. Using '-ll' adds information about selected mode parameter values (e.g. MRIE).                                                                                                                                                                                                                                                                                                |
| --num-desc             | -n                      | for a mode page that can have descriptors, the number of descriptors in the given page on DEVICE is output. Otherwise 0 is output.                                                                                                                                                                                                                                                                                                                                                                                            |
| --out-mask=OM          | -o OM                   | the value OM (default decimal) selects whether current (0x1), changeable (0x2), default (0x4) and/or saveable (0x8) values are output. The default is 0xf (i.e. 0x1\|0x2\|0x4\|0x8).                                                                                                                                                                                                                                                                                                                                          |
| --page=_PG_[,_SPG_]    | -p _PG_[,_SPG_]         | page (and optionally subpage) to output or change. Argument may be either an abbreviation, a number or two numbers separated by a comma. If a number is prefixed by "0x" or has a trailing "h" then it is decoded as hexadecimal. When a numeric argument is given, it is assumed to be for a mode page unless the '--inquiry' option is also given. An abbreviation is two or three lower case letters (e.g. "ca" for the caching mode page). An abbreviation may be for a mode page (e.g. "ca")  or a VPD page (e.g. "sp"). |
| --pdt=_DT_             | -P _DT_                 | where _DT_ is the "peripheral device type" value (e.g. 0 for a disk, 1 for a tape drive, etc). Only active when '--inhex=_FN'_ is also used.                                                                                                                                                                                                                                                                                                                                                                                  |
| --quiet                | -q                      | suppress vendor/product/revision strings that are usually the first line of the output. Also abridges the output of the device identification VPD page.                                                                                                                                                                                                                                                                                                                                                                       |
| --raw                  | -R                      | used together with '--inhex=_FN'_. It causes the file _FN_ to be interpreted as binary.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --readonly             | -r                      | override other logic and open DEVICE in read-only mode. This can help with ATA disks especially with commands like '-C stop'. Also works with '--set=' and '--clear='.                                                                                                                                                                                                                                                                                                                                                        |
| --save                 | -S                      | also write changes to corresponding "saved" values mode page. Active when used with '--set=', '--clear=' or '--defaults'. The default action is to only make changes to the current values mode page.                                                                                                                                                                                                                                                                                                                         |
| --set=_STR_            | -s _STR_                | set parameter(s) in _STR_. To set a parameter is to make all its bits one. The default action to set can be overridden, see below.                                                                                                                                                                                                                                                                                                                                                                                            |
| --six                  | -6                      | use 6 byte cdbs for MODE SENSE and MODE SELECT commands for getting and setting mode pages. The default action is to use the 10 byte cdb variants.                                                                                                                                                                                                                                                                                                                                                                            |
| --transport=_TN_       | -t _TN_                 | transport protocol identifier; either a number or an abbreviation (e.g. "fcp", "spi" or "sas") can be given. See [transports](https://sg.danny.cz/sg/sdparm.html#mozTocId808937) section. In the absence of an explicit transport and if a page or field name does not match a generic name then the SAS transport is assumed.                                                                                                                                                                                                |
| --vendor=_VN_          | -M _VN_                 | vendor (manufacturer) identifier; either a number or an abbreviation (e.g. "sea" or "hit") can be given. See [vendors](https://sg.danny.cz/sg/sdparm.html#mozTocId378082) section.                                                                                                                                                                                                                                                                                                                                            |
| --verbose              | -v                      | increase verbosity of output. May be used multiple times to further increase verbosity.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --version              | -V                      | print out the version and the date of last code change then exits                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --wscan                | -w                      | [Windows only] scan for device names, show one device per line. Each device can have multiple device names. If a _DEVICE_ name is given (on the command line) then it will be ignored.                                                                                                                                                                                                                                                                                                                                        |

Asegúrese de leer las páginas de manual de la utilidad `sdparm`. Puede ser una utilidad complicada de usar.
### Usando `sysctl`

La utilidad `sysctl` se utiliza para modificar los parámetros del kernel mientras se ejecuta un sistema. Dentro de estos parámetros se incluyen los asociados con los dispositivos de almacenamiento.

Para ver una lista de parámetros del kernel que se pueden modificar, escriba `sysctl -a` en la línea de comando, usando privilegios de super usuario. Debido a que la lista es larga (hay varios parámetros del kernel), es posible que desee canalizar la salida a un buscapersonas, como less. Para ver parámetros individuales, pase el parámetro como una opción al comando `sysctl`.

Cualquier archivo listado en los directorios y subdirectorios `/proc/sys/` también es un parámetro del kernel que se puede modificar. A continuación se muestra un ejemplo de una distribución de Ubuntu que utiliza `sysctl` y el archivo `/proc/sys/` para ver la configuración de los parámetros del kernel para expulsar automáticamente los discos ópticos cuando se han desmontado:

```sh
sudo sysctl dev.cdrom.autoeject
[sudo] password for christine:

dev.cdrom.autoeject = 0

ls /proc/sys/dev/cdrom/autoeject
/proc/sys/dev/cdrom/autoeject

cat /proc/sys/dev/cdrom/autoeject
0
```

Muchos parámetros del kernel son valores booleanos, lo que significa que 0 indica que la función está desactivada y 1 indica que la función está activada. En el ejemplo anterior, el parámetro `dev.cdrom.autoeject` es booleano y actualmente está desactivado.

Para cambiar la configuración de un parámetro del kernel, puede utilizar la utilidad `sysctl`. En este ejemplo, el parámetro `dev.cdrom.autoeject` está activado, lo que hace que los dispositivos ópticos se expulsen automáticamente cuando se desmontan:

```sh
sudo sysctl -w dev.cdrom.autoeject=1
[sudo] password for christine:

dev.cdrom.autoeject = 1

sudo sysctl dev.cdrom.autoeject
dev.cdrom.autoeject = 1

cat /proc/sys/dev/cdrom/autoeject
1
```

Puede ver que el archivo `/proc/sys/` asociado se actualiza instantáneamente cuando se utiliza la utilidad `sysctl` para modificar el parámetro del kernel. Sin embargo, esta modificación no es persistente. Para que la modificación sea persistente, debe modificar el archivo de configuración `/etc/sysctl.conf`. La siguiente es una lista de archivos recortados en una distribución de Ubuntu:

```sh
cat /etc/sysctl.conf

#/etc/sysctl.conf-Configuration file for setting system variables 
#See /etc/sysctl.d/ for additional system variables.
#See sysctl.conf (5) for information.

[...]
# Do not accept ICMP redirects (prevent MITM attacks)
#net.ipv4.conf.all.accept_redirects = 0
[...]
```

Una vez que haya realizado cambios de configuración en este archivo, puede probarlo emitiendo el comando `sysctl -p` y luego viendo los parámetros modificados.

Se deben modificar relativamente pocos parámetros del kernel para ajustar el acceso y el uso del disco. Sin embargo, estos dos parámetros RAID particulares pueden resultar útiles para ajustar:

```sh
sudo sysctl -a | grep raid
dev.raid.speed_limit_max = 200000 
dev.raid.speed_limit_min = 1000
```

Estos dos parámetros del kernel controlan la velocidad de RAID. Aumentar los límites podría aumentar la velocidad de cualquier reconstrucción o remodelación de una matriz RAID.
### Usando _smartctl_ y _smartd_

No puede restablecer ni modificar los atributos SMART de una unidad porque están configurados en el área protegida de una unidad. Solo puede habilitar/deshabilitar SMART usando la utilidad `smartctl`:

```sh
sudo smartctl -s on /dev/sda
```

Sin embargo, además de las pruebas, comprobaciones y análisis manuales que se muestran en el Capítulo 4 con la utilidad `smartctl` y los dispositivos SMART, puede configurar pruebas de dispositivos programadas con el demonio `smartd` y el archivo de configuración que lo acompaña. Dependiendo de su distribución, el archivo es `/etc/smartd.conf` o `/etc/smartmontools/smartd.conf`.

Si `smartd` se inicia durante la inicialización del sistema, habilitará el monitoreo SMART en cualquier dispositivo ATA que tenga esta capacidad. Después de eso, verificará los dispositivos SMART (incluidas las unidades SCSI) cada 30 minutos y enviará advertencias, mensajes de error y cambios en los elementos SMART al registrador del sistema.

Usted cambia los horarios de las encuestas, las pruebas que se realizan y quién recibe los mensajes a través del archivo de configuración. La palabra clave DEVICESCAN se puede configurar con varias opciones. Por ejemplo, para ejecutar una prueba larga en todos los dispositivos SMART de su sistema los domingos de 1 a.m. a 2 a.m., ingresaría el siguiente registro en el archivo de configuración:

```sh
DEVICESCAN -s L/../../7/01
```

Existe una gran cantidad de documentación excelente en el archivo de configuración de `smartd`. Consulte las páginas de manual del archivo de configuración `smartd` de su distribución, o simplemente busque en el archivo mismo. El archivo de configuración `smartd` suele estar muy documentado con muchos buenos ejemplos.
### Usando `nvme`

Para ajustar y ver registros de SSD con interfaz NVMe, debe utilizar comandos compatibles con el estándar NVMe. La utilidad `nvme` proporciona estos comandos a través de una interfaz de línea de comandos. Se proporciona junto con la documentación a través del paquete `nvme-cli`.

Una vez instalado, vea todos los diversos comandos disponibles para ajustar sus SSD con interfaz NVMe escribiendo `nvme help` en la línea de comando. Aquí se muestra un ejemplo recortado de una distribución de Ubuntu:

```sh
nvme help

[...]The following are all implemented sub-commands:  
 list            List all NVMe devices and namespaces on machine
 id-ctrl         Send NVMe Identify Controller
 id-ns           Send NVMe Identify Namespace, display structure  
 list-ns         Send NVMe Identify List, display structure  
 create-ns       Creates a namespace with the provided parameters  
 delete-ns       Deletes a namespace from the controller  
 attach-ns       Attaches a namespace to requested controller(s)  
 detach-ns       Detaches a namespace from requested controller(s)  
 list-ctrl       Send NVMe Identify Controller List, display structure  
 get-ns-id       Retrieve the namespace ID of opened block device  
 get-log         Generic NVMe get log, returns log in raw format
 fw-log          Retrieve FW Log, show it  
 smart-log       Retrieve SMART Log, show it  
 smart-log-add   Retrieve additional SMART Log, show it
 error-log       Retrieve Error Log, show it  
 get-feature     Get feature and show the resulting value  
 set-feature     Set a feature and show the resulting value  
 format          Format namespace with new block format
 fw-activate     Activate new firmware slot  
 fw-download     Download new firmware
 admin-passthru  Submit arbitrary admin command, return results  
 io-passthru     Submit an arbitrary IO command, return results  
 security-send   Submit a Security Send command, return results  
 security-recv   Submit a Security Receive command, return results  
 resv-acquire    Submit a Reservation Acquire, return results  
 resv-register   Submit a Reservation Register, return results  
 resv-release    Submit a Reservation Release, return results  
 resv-report     Submit a Reservation Report, return results  
 dsm             Submit a Data Set Management command, return results 
 flush           Submit a Flush command, return results  
 compare         Submit a Comapre command, return results  
 read            Submit a read command, return results  
 write           Submit a write command, return results
 show-regs       Shows the controller registers. Requires admin character device
 version         Shows the program version  
 help            Display this help

See 'nvme help <command>' for more information on a specific command.
```

Observe en el ejemplo que se utiliza el término _controlador_. El estándar NVMe también se denomina estándar NVM Host Controller Interface (NVMHCI). Un controlador NVMe es una función PCI Express que implementa especificaciones NVMe (o NVMHCI). Es posible que tenga uno o más controladores que administren los espacios de nombres de un SSD con interfaz NVMe en particular. Como se describió anteriormente en este capítulo, un espacio de nombres NVMe es otra capa de división de unidades, que puede constar de una o más particiones. La utilidad `nvme` facilita considerablemente la gestión, el ajuste y la revisión de los registros de la unidad.

Observe también en el ejemplo anterior que la utilidad `nvme` permite la recuperación de registros SMART. Debido a que el estándar NVMe no viene con una interfaz compatible con AHCI o SCSI, si un SSD tiene capacidad SMART, actualmente no existe una forma de recuperar información SMART a través de la utilidad SMART estándar (`smartctl`).

La utilidad `nvme` es muy útil. Le permite realizar cualquier ajuste o administración necesarios de sus SSD con interfaz NVMe.
### Usando `fstrim`

El comando `fstrim` se puede utilizar periódicamente para evitar problemas de rendimiento en los SSD debido a la fragmentación interna. Sin embargo, antes de intentar utilizar el comando `fstrim`, debe verificar que su SSD sea compatible con TRIM. Puede usar el comando `hdparm` y `grep` para verificar su unidad, como se muestra en una distribución de Ubuntu aquí:

```sh
sudo hdparm -I /dev/sda  | grep TRIM
```

Si no hay respuesta del comando significa que TRIM _no_ es compatible. Si se admite TRIM, puede emplear `fstrim` para implementar comandos TRIM en su SSD. La sintaxis general del comando `fstrim` es la siguiente: 

```
fstrim [opciones] punto de montaje
```

```
OPTIONS    

       The offset, length, and minimum-size arguments may be followed by
       the multiplicative suffixes KiB (=1024), MiB (=1024*1024), and so
       on for GiB, TiB, PiB, EiB, ZiB and YiB (the "iB" is optional,
       e.g., "K" has the same meaning as "KiB") or the suffixes KB
       (=1000), MB (=1000*1000), and so on for GB, TB, PB, EB, ZB and
       YB.

       -A, --fstab
           Trim all mounted filesystems mentioned in /etc/fstab on
           devices that support the discard operation. The root
           filesystem is determined from kernel command line if missing
           in the file. The other supplied options, like --offset,
           --length and --minimum, are applied to all these devices.
           Errors from filesystems that do not support the discard
           operation, read-only devices, autofs and read-only
           filesystems are silently ignored. Filesystems with
           "X-fstrim.notrim" mount option are skipped.

       -a, --all
           Trim all mounted filesystems on devices that support the
           discard operation. The other supplied options, like --offset,
           --length and --minimum, are applied to all these devices.
           Errors from filesystems that do not support the discard
           operation, read-only devices and read-only filesystems are
           silently ignored.

       -n, --dry-run
           This option does everything apart from actually call FITRIM
           ioctl.

       -o, --offset offset
           Byte offset in the filesystem from which to begin searching
           for free blocks to discard. The default value is zero,
           starting at the beginning of the filesystem.

       -l, --length length
           The number of bytes (after the starting point) to search for
           free blocks to discard. If the specified value extends past
           the end of the filesystem, fstrim will stop at the filesystem
           size boundary. The default value extends to the end of the
           filesystem.

       -I, --listed-in list
           Specifies a colon-separated list of files in fstab or kernel
           mountinfo format. All missing or empty files are silently
           ignored. The evaluation of the list stops after first
           non-empty file. For example:
           --listed-in /etc/fstab:/proc/self/mountinfo.
           Filesystems with "X-fstrim.notrim" mount option in fstab are
           skipped.

       -m, --minimum minimum-size
           Minimum contiguous free range to discard, in bytes. (This
           value is internally rounded up to a multiple of the
           filesystem block size.) Free ranges smaller than this will be
           ignored and fstrim will adjust the minimum if it’s smaller
           than the device’s minimum, and report that
           (fstrim_range.minlen) back to userspace. By increasing this
           value, the fstrim operation will complete more quickly for
           filesystems with badly fragmented freespace, although not all
           blocks will be discarded. The default value is zero,
           discarding every free block.

       -t, --types list
           Specifies allowed or forbidden filesystem types when used
           with --all or --fstab. The list is a comma-separated list of
           the filesystem names. The list follows how mount -t evaluates
           type patterns. Only specified filesystem types are allowed.
           All specified types are forbidden if the list is prefixed by
           "no" or each filesystem prefixed by "no" is forbidden. If the
           option is not used, then all filesystems (except "autofs")
           are allowed.

       -v, --verbose
           Verbose execution. With this option fstrim will output the
           number of bytes passed from the filesystem down the block
           stack to the device for potential discard. This number is a
           maximum discard amount from the storage device’s perspective,
           because FITRIM ioctl called repeated will keep sending the
           same sectors for discard repeatedly.
           fstrim will report the same potential discard bytes each
           time, but only sectors which had been written to between the
           discards would actually be discarded by the storage device.
           Further, the kernel block layer reserves the right to adjust
           the discard ranges to fit raid stripe geometry, non-trim
           capable devices in a LVM setup, etc. These reductions would
           not be reflected in fstrim_range.len (the --length option).

       --quiet-unsupported
           Suppress error messages if trim operation (ioctl) is
           unsupported. This option is meant to be used in systemd
           service file or in cron scripts to hide warnings that are
           result of known problems, such as NTFS driver reporting Bad
           file descriptor when device is mounted read-only, or lack of
           file system support for ioctl FITRIM call. This option also
           cleans exit status when unsupported filesystem specified on
           fstrim command line.

       -h, --help
           Display help text and exit.

       -V, --version
           Print version and exit.
```

También puede obtener ayuda sobre la utilidad `fstrim` escribiendo `fstrim` y usando la opción `-h` o `--help`.

Debe utilizar privilegios de superusuario y el SSD debe estar montado. En este ejemplo, el comando `fstrim` se emite usando la opción detallada en una distribución CentOS:

```sh
fstrim -v /home
/home: 1503238553 bytes were trimmed
```

La salida del comando `fstrim` puede ser un poco engañosa. Los bytes mostrados no necesariamente tenían el comando TRIM aplicado sobre ellos. En cambio, estos bytes fueron auditados y, si se consideraba necesario desfragmentarlos, se desfragmentaron.

La mayoría de las unidades, excepto las SSD, nunca necesitarán ser ajustadas. Sin embargo, muchas de las utilidades de esta sección también se pueden utilizar para monitoreo o prueba.

### Implementando iSCSI
Internet Small Computer System Interface (iSCSI) es un protocolo de red (RFC 3720) que permite el transporte de comandos SCSI a través de TCP/IP. En esencia, permite que las unidades ubicadas remotamente (a través de la intranet de una empresa o incluso a través de Internet) aparezcan como si fueran unidades SCSI locales.

Para comprender iSCSI, es importante comprender algunos conceptos básicos de red de área de almacenamiento (SAN). Una SAN consta de dispositivos de almacenamiento conectados a la red, donde varios sistemas y los dispositivos de almacenamiento se comunican entre sí a través de una red. El objetivo principal de una red SAN es permitir esa comunicación y, por lo general, es una red de alta velocidad dedicada únicamente a las comunicaciones SAN.

Hay tres protocolos SAN populares además de iSCSI para explorar. Las siguientes descripciones le ayudarán a comprender varias alternativas de iSCSI.

***Protocolo de canal de fibra*** Una SAN de canal de fibra es una SAN de alta velocidad y altamente confiable, que generalmente funciona con cables de fibra óptica y ofrece velocidades de hasta 32 gigabits por segundo. Esta SAN, costosa de implementar, utiliza el  Fiber Channel Protocol (FCP) para transportar comandos SCSI a través de la red dedicada. 

***Protocolo ATA sobre Ethernet*** ATA sobre Ethernet AoE es un protocolo de transporte de red que no utiliza el protocolo de Internet, sino que se ejecuta en la capa 2 de una red. Con este protocolo, los comandos ATA se transportan a través de una red Ethernet. La red se puede compartir con otros paquetes TCP/IP, lo que hace que la implementación de AoE sea más económica. Debido a que es un protocolo no enrutable, proporciona seguridad heredada y facilidad de implementación de SAN. 

***Fiber Channel Protocol sobre Ethernet*** Para aquellos que no pueden permitirse el gasto de una red de fibra óptica dedicada, el protocolo Fiber Channel sobre Ethernet (FCoE) proporciona una alternativa de menor costo. FCoE encapsula tramas de protocolo Fiber Channel para viajar a través de redes Ethernet.

Al igual que AoE y FCoE, la red de una implementación de SAN iSCSI no está dedicada a la SAN iSCSI, pero se puede compartir con otras comunicaciones TCP/IP.
Una SAN iSCSI es económica en comparación con una SAN Fiber Channel y mucho más sencilla de configurar. Sin embargo, debido a que iSCSI comparte su red con otros protocolos TCP/IP, dependiendo de cómo se implemente, es posible que no alcance las mismas velocidades de transferencia de datos que una SAN Fiber Channel.

Es posible que descubra que iSCSI es adecuado para sus necesidades de SAN. Pero antes de comenzar una implementación iSCSI, es necesario comprender los términos y conceptos importantes del protocolo.
### Entendiendo iSCSI
En una SAN iSCSI, el sistema remoto que ofrece un disco iSCSI se denomina destino. El sistema local que desea utilizar el disco iSCSI ofrecido se denomina iniciador. Por lo tanto, existe una relación de cliente (iniciador) servidor (destino) al ofrecer y acceder a unidades iSCSI.

Un número de unidad lógica (LUN) es un número que se utiliza para identificar un dispositivo SCSI lógico único en el sistema de destino. La numeración de LUN comienza en cero, por lo que al primer dispositivo SCSI que se ofrece a través de iSCSI normalmente se le asigna lun0. Un LUN iSCSI puede tener un nombre de alias de hasta 255 caracteres de longitud, lo que hace que una unidad LUN particular sea más fácil de identificar.

Un nombre calificado iSCSI (IQN) es una dirección única que identifica el servidor de destino iSCSI junto con la unidad iSCSI ofrecida. Un IQN tiene el siguiente formato básico:

```
iqn.fecha-dominio.dominio:nombre-scsi-único
```

La fecha del dominio es la fecha en que su organización registró oficialmente su dominio. El formato es año-mes. El dominio es el dominio de la organización. `Unique-scsi-id` es un nombre único que se le da a la unidad SCSI. Depende de usted cómo identificar cada unidad SCSI de forma única, siempre y cuando los nombres sean únicos para cada unidad SCSI en el servidor de destino. Por ejemplo, un IQN podría verse así:

```
iqn.2016–02.com.ejemplo.servidor07:iscsidisk1
```

En el ejemplo anterior, la fecha del dominio es febrero de 2016 escrita en orden inverso: 2016–02. El dominio es server07.example.com, pero observe que también está escrito en orden inverso. Finalmente, el nombre scsi único es iscsidisk1. Como alternativa, puede utilizar el LUN de la unidad SCSI dentro del nombre SCSI exclusivo, como iscsilun0.

El IQN de una unidad iSCSI es importante porque se utiliza en muchos de los archivos y ajustes de configuración iSCSI para identificar la unidad SCSI ofrecida por el servidor de destino. Por lo tanto, querrá tomarse un tiempo para determinar un nombre scsi único para el IQN. Si tiene una instalación SAN iSCSI grande, debe usar la salida del comando `scsi_id`, o el WWID/WWN del SCSI, para identificar la unidad de forma única. Para cuotas más pequeñas, debería ser suficiente un nombre inventado o el LUN de SCSI.

### Configuración de un disco iSCSI de destino
La herramienta principal para configurar un disco iSCSI en un servidor de destino es la utilidad `targetcli`. Es una interfaz de shell que le permite administrar el subsistema de destino del kernel, Linux IO (LIO). LIO existe desde el kernel de Linux v2.6 y es un subsistema que admite estructuras de almacenamiento. Una estructura de almacenamiento es cualquier hardware que conecta dispositivos de almacenamiento SAN a sistemas. LIO admite estructuras de almacenamiento, como Fiber Channels e iSCSI.

Primero, en su sistema, debe asegurarse de que el subsistema de destino se inicie en el momento del arranque y que el servicio se esté ejecutando. A continuación se muestra un ejemplo de cómo habilitar el subsistema de destino en una distribución CentOS para que se inicie al reiniciar:

```sh
systemctl enable target
ln -s '/usr/lib/systemd/system/target.service'
'/etc/systemd/system/multi-user.target.wants/target.service'
```

Una vez que se asegure de que el subsistema de destino se esté ejecutando, utilizando privilegios de superusuario, ingrese a la utilidad targetcli. Recibirá un mensaje /> cuando haya ingresado a la utilidad. Aquí se muestra un ejemplo:

```sh
targetcli
Warning: Could not load preferences file /root/.targetcli/prefs.bin. 
targetcli shell version 2.1.fb37 
Copyright 2011–2013 by Datera, Inc and others.
For help on commands, type 'help'.

/>
```