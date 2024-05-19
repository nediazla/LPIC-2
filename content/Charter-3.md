# Dominar el Kernel

Si bien normalmente nos referimos al sistema operativo Linux simplemente como Linux, en realidad, bastantes partes conforman un sistema Linux completo. El kernel de Linux es el componente principal que mantiene cosas juntas y ejecutándose en su sistema. Es el corazón del sistema Linux y controla el hardware, la memoria y las aplicaciones en ejecución.
Este capítulo analiza primero las diferentes partes del kernel de Linux y cómo encajan entre sí para controlar la computadora. A continuación, el capítulo examina cómo se instala el kernel de Linux en diferentes distribuciones de Linux y dónde encontrar las diferentes partes del mismo. Después de eso, el capítulo analiza cómo crear un nuevo kernel para admitir nuevo hardware o simplemente para actualizar su sistema Linux a las últimas funciones. Finalmente, el capítulo examina cómo administrar el kernel y los módulos del kernel, junto con cómo solucionar problemas del kernel si algo sale mal.

### ¿Qué es el Kern el?
Un sistema Linux completo consta de cuatro partes principales:
- El núcleo de Linux
- Las utilidades GNU
- Un entorno de escritorio gráfico
- Software de aplicación

Cada una de estas cuatro partes tiene un trabajo específico en el sistema Linux. Si bien cada una de las partes por sí sola no es muy útil, en conjunto crean lo que llamamos Linux. La Figura 3.1 muestra un diagrama básico de cómo encajan estas partes para crear el sistema Linux general.
El núcleo del sistema Linux es el kernel. El kernel controla todo el hardware y software del sistema informático, asigna hardware cuando es necesario y ejecuta software cuando es necesario.
### Las características del núcleo
Si ha estado siguiendo el mundo Linux, sin duda habrá escuchado el nombre Linus Torvalds. Linus es el responsable de crear el primer software del kernel de Linux mientras era estudiante en la Universidad de Helsinki. Su intención era que fuera una copia del sistema Unix, que era un sistema operativo popular utilizado por muchas universidades en ese momento.

Después de desarrollar el kernel de Linux, Linus lo lanzó a la comunidad de Internet y solicitó sugerencias para mejorarlo. Este sencillo proceso inició una revolución en el mundo de los sistemas operativos informáticos. Pronto Linus recibió sugerencias de estudiantes y programadores profesionales de todo el mundo.

Permitir que cualquiera cambie el código de programación en el kernel resultaría en un caos total. Para simplificar las cosas, Linus actuó como punto central para todas las sugerencias de mejora. En última instancia, fue decisión de Linus incorporar o no el código sugerido en el núcleo. Este mismo concepto todavía está vigente con el código del kernel de Linux, excepto que en lugar de que solo Linus controle el código del kernel, un equipo de desarrolladores llamado la Fundación Linux ha asumido la tarea.

El núcleo es el principal responsable de cuatro funciones principales:
- Gestión de la memoria del sistema
- Gestión de programas de software
- Gestión de hardware
- Gestión del sistema de archivos
### Gestión de la memoria del sistema
Una de las funciones principales del kernel del sistema operativo es la gestión de la memoria.
La gestión de la memoria es la capacidad de controlar cómo se ejecutan los programas y utilidades dentro de las estricciones de memoria del sistema. El kernel no sólo administra la memoria física disponible en el servidor, sino que también puede crear y administrar memoria virtual, o memoria que en realidad no existe pero que se crea en el disco duro y se trata como memoria real.

Lo hace utilizando espacio en el disco duro, llamado espacio de intercambio. El kernel intercambia el contenido de las ubicaciones de la memoria virtual desde el espacio de intercambio a la memoria física real. Esto permite que el sistema piense que hay más memoria disponible de la que existe físicamente, como se muestra en la Figura 3.2.

![](img/3.2.png)

Las ubicaciones de la memoria se agrupan en bloques llamados páginas de memoria. El kernel ubica cada página de memoria en la memoria física o en el espacio de intercambio. Luego, el núcleo mantiene una tabla de las páginas de memoria que indica qué páginas están en la memoria física y cuáles se intercambian en el disco.

El kernel realiza un seguimiento de qué páginas de memoria están en uso y copia automáticamente las páginas de memoria a las que no se ha accedido durante un período de tiempo al área de espacio de intercambio (esto se llama intercambio), incluso si hay otra memoria disponible. Cuando un programa quiere acceder a una página de memoria que ha sido intercambiada, el núcleo debe dejarle espacio en la memoria física intercambiando una página de memoria diferente e intercambiando la página requerida desde el espacio de intercambio. Obviamente, este proceso lleva tiempo y puede ralentizar un proceso en ejecución. El proceso de intercambio de páginas de memoria para ejecutar aplicaciones continúa mientras el sistema Linux esté en ejecución.
Puede ver el estado actual de la memoria virtual en su sistema Linux viendo el archivo especial `/proc/meminfo`. El Listado 3.1 muestra un ejemplo de una entrada `/proc/meminfo` de muestra.

```sh
cat /proc/meminfo
MemTotal:        1908188 kB
MemFree:          408188 kB
MemAvailable:     855432 kB
Buffers:           32544 kB
Cached:           514140 kB
SwapCached:            0 kB
Active:          1033464 kB
Inactive:         341712 kB
Active(anon):     829016 kB
Inactive(anon):     1120 kB
Active(file):     204448 kB
Inactive(file):   340592 kB
Unevictable:          16 kB
Mlocked:              16 kB
SwapTotal:       1165308 kB
SwapFree:        1165308 kB
Dirty:              2112 kB
Writeback:             0 kB
AnonPages:        828536 kB
Mapped:           199596 kB
Shmem:              1660 kB
Slab:              61352 kB
SReclaimable:      29656 kB
SUnreclaim:        31696 kB
KernelStack:        5680 kB
PageTables:        31972 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     2119400 kB
Committed_AS:    2673804 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       30256 kB
VmallocChunk:   34359699448 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       58748 kB
DirectMap2M:     1894400 kB
```

Las líneas `MemTotal` y `MemFree` muestran que este servidor Linux tiene 2 GB de memoria física, pero que actualmente sólo unos 408 MB no están en uso (gratuitos). El resultado también muestra que hay aproximadamente 1 GB de memoria de espacio de intercambio disponible en este sistema.
De forma predeterminada, cada proceso que se ejecuta en el sistema Linux tiene sus propias páginas de memoria privadas. Un proceso no puede acceder a las páginas de memoria que utiliza otro proceso. El kernel mantiene sus propias áreas de memoria. Por motivos de seguridad, ningún proceso puede acceder a la memoria utilizada por los procesos del kernel.

Para facilitar el intercambio de datos, puede crear páginas de memoria compartida. Múltiples procesos pueden leer y escribir desde y hacia un área de memoria compartida común. El kernel mantiene y administra las áreas de memoria compartida y permite que los procesos individuales accedan al área compartida.

El comando especial `ipcs` le permite ver las páginas de memoria compartida actuales en el sistema. Aquí está el resultado de un comando `ipcs` de muestra:

```sh
ipcs -m
———Shared Memory Segments————

key        shmid      owner      perms      bytes      nattch     status
0xcf124bdc 0          root       600        1000       6
0x0b234bfc 32769      root       600        8          6
0x07021999 65538      root       644        1704       2
0x00000000 163843     rich       600        4194304    2          dest 
0x00000000 262148     rich       600        1048576    2          dest
```

Cada segmento de memoria compartida tiene un propietario que creó el segmento. Cada segmento también tiene una configuración de permisos estándar de Linux que establece la disponibilidad del segmento para otros usuarios. El valor clave se utiliza para permitir que otros usuarios obtengan acceso al segmento de memoria compartida.
### Gestión de programas de software
El sistema operativo Linux llama proceso a un programa en ejecución. Un proceso puede ejecutarse en primer plano, mostrando el resultado en una pantalla, o puede ejecutarse en segundo plano detrás de escena. El kernel controla cómo el sistema Linux gestiona todos los procesos que se ejecutan en el sistema.

El kernel crea el primer proceso, llamado `init`, para iniciar todos los demás procesos del sistema. Cuando se inicia el kernel, carga el proceso de inicio en la memoria virtual. A medida que el kernel inicia cada proceso adicional, le proporciona un área única en la memoria virtual para almacenar los datos y el código que utiliza el proceso.

Algunas implementaciones de Linux contienen una tabla de procesos que se inician automáticamente al iniciar. En sistemas Linux, esta tabla normalmente se encuentra en el archivo especial `/etc/inittab`.

Como se analizó en el Capítulo 1, “Inicio de un sistema”, el sistema operativo Linux utiliza un sistema de inicio que utiliza niveles de ejecución (para el método de inicio `SysV`) o destinos (para el método `systemd`) que determinan qué procesos se inician. Hay siete niveles de ejecución inicial en el sistema operativo Linux.

En el nivel de ejecución 1, solo se inician los procesos básicos del sistema, junto con un proceso de terminal de consola. Esto se llama modo de usuario único. El modo de usuario único se utiliza con mayor frecuencia para el mantenimiento de emergencia del sistema de archivos cuando algo falla. Obviamente, en este modo sólo una persona (normalmente el administrador) puede iniciar sesión en el sistema para manipular datos.

Para la mayoría de las distribuciones de Linux, el nivel de ejecución de inicio estándar es 3. En este nivel de ejecución, se inicia la mayoría del software de aplicación, como el software de soporte de red. Otro nivel de ejecución popular en Linux es el nivel de ejecución 5. Este es el nivel de ejecución donde el sistema inicia el software gráfico X Window y le permite iniciar sesión utilizando una ventana gráfica del escritorio.

El sistema Linux puede controlar la funcionalidad general del sistema controlando el nivel de ejecución inicial. Por ejemplo, al cambiar el nivel de ejecución de 3 a 5, el sistema puede cambiar de un sistema basado en consola a un sistema X Window gráfico avanzado.
El comando `ps` le permite ver los procesos que se ejecutan actualmente en el sistema Linux. El Listado 3.2 muestra un ejemplo de lo que verá usando el comando `ps`.

```sh
ps ax
   PID TTY      STAT   TIME COMMAND
	1    ?        S      0:03 init
	2    ?        SW     0:00 [kflushd]
	3    ?        SW     0:00 [kupdate]
	4    ?        SW     0:00 [kpiod]
	5    ?        SW     0:00 [kswapd]
   243   ?        SW     0:00 [portmap]
   295   ?        S      0:00 syslogd
   305   ?        S      0:00 klogd
   320   ?        S      0:00 /usr/sbin/atd
   335   ?        S      0:00 crond
   350   ?        S      0:00 inetd
   365   ?        SW     0:00 [lpd]
   403   ttyS0    S      0:00 gpm -t ms
   418   ?        S      0:00 httpd
   423   ?        S      0:00 httpd
424    ?        SW     0:00 [httpd]
425    ?        SW     0:00 [httpd]
426    ?        SW     0:00 [httpd]
427    ?        SW     0:00 [httpd]
428    ?        SW     0:00 [httpd]
429    ?        SW     0:00 [httpd]
430    ?        SW     0:00 [httpd]
436    ?        SW     0:00 [httpd]
437    ?        SW     0:00 [httpd]
438    ?        SW     0:00 [httpd]
   470 ?        S      0:02 xfs -port -1
   485 ?        SW     0:00 [smbd]
   495 ?        S      0:00 nmbd -D
   533 ?        SW     0:00 [postmaster]
538    tty1     SW     0:00 [mingetty]
539    tty2     SW     0:00 [mingetty]
540    tty3     SW     0:00 [mingetty]
541    tty4     SW     0:00 [mingetty]
542    tty5     SW     0:00 [mingetty]
543    tty6     SW     0:00 [mingetty]
544    ?        SW     0:00 [prefdm]
   549 ?        SW     0:00 [prefdm]
   559 ?        S      0:02 [kwm]
   585 ?        S      0:06 kikbd
594    ?        S      0:00 kwmsound
595    ?        S      0:03 kpanel
596    ?        S      0:02 kfm
597    ?        S      0:00 krootwm
598    ?        S      0:01 kbgndwm
   611 ?        S      0:00 kcmlaptop -daemon
   666 ?        S      0:00 /usr/libexec/postfix/master
   668 ?        S      0:00 qmgr -l -t fifo -u
   787 ?        S      0:00 pickup -l -t fifo
790    ?        S      0:00 telnetd: 192.168.1.2 [vt100]
791    pts/0    S      0:00 login—rich
792    pts/0    S      0:00 -bash
   805 pts/0    R      0:00 ps ax
```

La primera columna del resultado muestra el ID del proceso (PID) del proceso. Observe que el primer proceso es nuestro amigo, el proceso de init, y el sistema Linux le asigna el PID 1. A todos los demás procesos que comienzan después del proceso de inicio se les asignan PID en orden numérico. No hay dos procesos que puedan tener el mismo PID.

La tercera columna muestra el estado actual del proceso (S para dormir, SW para dormir y esperar y R para ejecutar). El nombre del proceso se muestra en la última columna. Los procesos que están entre paréntesis se han intercambiado desde la memoria al espacio de intercambio del disco debido a la inactividad. Puede ver que algunos de los procesos se han intercambiado, pero la mayoría de los procesos en ejecución no.
### Gestión de hardware
Otra responsabilidad más del núcleo es la gestión del hardware. Cualquier dispositivo con el que el sistema Linux deba comunicarse necesita un código de controlador insertado dentro del código del kernel. El código del controlador permite que el kernel pase datos de ida y vuelta al dispositivo, actuando como intermediario entre las aplicaciones y el hardware. Hay dos métodos utilizados para insertar el código del controlador del dispositivo en el kernel de Linux: 
- Controladores compilados en el kernel
- Módulos de controlador agregados al kernel

Anteriormente, la única forma de insertar el código del controlador del dispositivo era recompilar el kernel.

Cada vez que agregaba un nuevo dispositivo al sistema, tenía que recompilar el código del kernel. Este proceso se volvió aún más ineficiente a medida que los kernels de Linux admitían más hardware. Afortunadamente, los desarrolladores de Linux idearon un método mejor para insertar el código del controlador en el kernel en ejecución.

Los programadores desarrollaron el concepto de módulos del kernel para permitirle insertar el código del controlador del dispositivo en un kernel en ejecución sin tener que volver a compilar el kernel. Un módulo es un archivo de biblioteca de controladores autónomo que se puede vincular y desvincular dinámicamente con el kernel. Esto significa que puede eliminar un módulo del kernel cuando haya terminado de usar el dispositivo, algo que no puede hacer con los controladores del kernel compilados. Esto se simplificó y amplió enormemente utilizando hardware con Linux.

El sistema Linux identifica los dispositivos de hardware como archivos especiales, llamados archivos de dispositivo. Hay tres clasificaciones de archivos de dispositivos:
- Carácter
- Bloquear
- Red

Los archivos de dispositivo de caracteres son para dispositivos que pueden manejar datos de solo un carácter a la vez. La mayoría de los tipos de módems y terminales se crean como archivos de caracteres. Los archivos de dispositivos de bloque son para dispositivos que pueden manejar datos en bloques grandes a la vez, como unidades de disco.

Los tipos de archivos de dispositivos de red se utilizan para dispositivos que utilizan paquetes para enviar y recibir datos. Estos incluyen tarjetas de red y un dispositivo de bucle invertido especial que permite que el sistema Linux se comunique consigo mismo mediante protocolos de programación de red comunes.

Linux crea archivos especiales, llamados nodos, para cada dispositivo del sistema. Toda la comunicación con el dispositivo se realiza a través del nodo del dispositivo. Cada nodo tiene un par de números único que lo identifica ante el kernel de Linux. El par de números incluye un número de dispositivo mayor y otro menor. Los dispositivos similares se agrupan en el mismo número de dispositivo principal. El número de dispositivo menor se utiliza para identificar un dispositivo específico dentro del grupo de dispositivos principal. El Listado 3.3 muestra un ejemplo de algunos archivos de dispositivo en un servidor Linux.

```sh
cd /dev
ls -al sda* ttyS*
brw-rw----.   1 root   disk    8,    0   Sep 10 16:27   sda 
brw-rw----.   1 root   disk    8,    1   Sep 10 16:27   sda1 
brw-rw----.   1 root   disk    8,    2   Sep 10 16:27   sda2 
brw-rw----.   1 root   disk    8,    3   Sep 10 16:27   sda3 
brw-rw----.   1 root   disk    8,    4   Sep 10 16:27   sda4 
crw-rw----.   1 root   dialout 4,   64   Sep 10 16:27   ttyS0 
crw-rw----.   1 root   dialout 4,   65   Sep 10 16:27   ttyS1 
crw-rw----.   1 root   dialout 4,   66   Sep 10 16:27   ttyS2 
crw-rw----.   1 root   dialout 4,   67   Sep 10 16:27   ttyS3
```

Diferentes distribuciones de Linux manejan dispositivos con diferentes nombres de dispositivo. En esta distribución, el dispositivo sda es el primer disco duro SCSI y los dispositivos ttyS son los puertos COM estándar de IBM PC. El Listado 3.3 muestra todos los dispositivos sda que se crearon en el sistema Linux de muestra. En realidad no todos se utilizan, pero se crean en caso de que el administrador los necesite. Del mismo modo, el listado muestra todos los dispositivos ttyS creados.
La quinta columna es el número de nodo del dispositivo principal. Observe que todos los dispositivos sda tienen el mismo nodo de dispositivo principal, 8, mientras que todos los dispositivos ttyS usan 4. La sexta columna es el número de nodo del dispositivo menor. Cada dispositivo dentro de un número mayor tiene su propio número de nodo de dispositivo menor único.
La primera columna indica los permisos para el archivo del dispositivo. El primer carácter de los permisos indica el tipo de archivo. Observe que todos los archivos del disco duro SCSI están marcados como dispositivos de bloque (b), mientras que los archivos de dispositivos del puerto COM están marcados como dispositivos de caracteres (c).
### Gestión del sistema de archivos
Un sistema de archivos define cómo el sistema operativo almacena datos en dispositivos de almacenamiento. A diferencia de otros sistemas operativos, el kernel de Linux puede admitir diferentes tipos de sistemas de archivos para leer y escribir datos desde y hacia discos duros, dispositivos de CD o DVD y unidades flash USB. Además de tener más de una docena de sistemas de archivos propios, Linux puede leer y escribir desde y hacia sistemas de archivos utilizados por otros sistemas operativos, como Microsoft Windows. El kernel debe compilarse con soporte para todos los tipos de sistemas de archivos que utilizará el sistema. La Tabla 3.1 enumera los sistemas de archivos estándar que un sistema Linux puede usar para leer y escribir datos.


| filesystem | Description                                                        |
| ---------- | ------------------------------------------------------------------ |
| ext        | Extended filesystem—the original Linux filesystem                  |
| ext2       | Second extended filesystem, provided advanced features over ext    |
| ext3       | Third extended filesystem, supports journaling                     |
| ext4       | Fourth extended filesystem, supports advanced journaling           |
| HPFS       | OS/2 high-performance filesystem                                   |
| JFS        | IBM’s journaling filesystem                                        |
| ISO 9660   | ISO 9660 filesystem (CD-ROMs                                       |
| MINIX      | MINIX filesystem                                                   |
| msdos      | Microsoft FAT16                                                    |
| NCP        | NetWare filesystem                                                 |
| NFS        | Network File System                                                |
| NTFS       | Microsoft NT filesystem                                            |
| procfs     | Access to system information                                       |
| ReiserFS   | Advanced Linux filesystem for better performance and disk recovery |
| SMB        | Samba SMB filesystem for network access                            |
| sysv       | Older Unix filesystem                                              |
| UFS        | BSD filesystem                                                     |
| umsdos     | Unix-like filesystem that resides on top of MS-DOS                 |
| VFAT       | Windows 95 filesystem (FAT32)                                      |
| XFS        | High-performance 64-bit journaling filesystem                      |

Cualquier disco duro al que acceda un servidor Linux debe formatearse utilizando uno de los tipos de sistemas de archivos enumerados en la Tabla 3.1.

El kernel de Linux interactúa con cada sistema de archivos mediante el sistema de archivos virtual (VFS). Esto proporciona una interfaz estándar para que el kernel se comunique con cualquier tipo de sistema de archivos. VFS almacena información en caché en la memoria a medida que se monta y utiliza cada sistema de archivos.
### Partes Kernel
Al instalar un nuevo kernel (o actualizar un kernel existente), hay varios componentes disponibles para instalar. Esta sección analiza cada uno de estos componentes y describe lo que contribuyen al entorno del kernel en su sistema Linux.
### Kernel binario
El archivo binario del kernel es el programa del kernel en sí. Esto es lo que el programa del gestor de arranque carga en la memoria, por lo que debe estar presente en el sistema Linux para que el sistema arranque e inicie.

El archivo binario del kernel puede ser algo grande, dependiendo de cuántos controladores estén compilados en el kernel de forma predeterminada. Por eso, el archivo binario del kernel generalmente se comprime para ahorrar espacio en la memoria cuando se carga el kernel. El nombre del archivo del kernel depende de cómo se comprimió el archivo binario del kernel. La Tabla 3.2 enumera los diferentes nombres de archivos binarios del kernel que se utilizan en las distribuciones de Linux.

| Filename | Description                                                                    |
| -------- | ------------------------------------------------------------------------------ |
| bzImage  | A larger kernel binary file compressed using the GNU zip utility               |
| Kernel   | A generic name for an uncompressed kernel binary file                          |
| vmlinux  | An uncompressed kernel binary file, not usually used as the final boot version |
| vmlinuz  | A generic compressed kernel binary filename                                    |
| zImage   | A small kernel binary file compressed using the GNU zip utility                |

El formato de archivo bzImage es el más popular. Sin embargo, muchas distribuciones de Linux copian ese archivo al nombre de archivo vmlinuz. Cuando busque el archivo binario del kernel en su sistema Linux, a menudo verá el nombre del archivo binario principal con la versión del kernel adjunta, como vmlinuz-4.3.3. Este método le permite mantener más de un kernel en su sistema y arrancar usando una versión de kernel diferente para diferentes situaciones.
El archivo binario del kernel debe ser accesible para el programa de arranque, que es lo que carga el kernel en la memoria en el momento del arranque. Debido a esto, los archivos binarios del kernel normalmente se almacenan en la estructura del directorio `/boot` en el sistema de archivos, aunque algunas distribuciones de Linux mantienen los archivos binarios del kernel directamente en el directorio raíz (`/`).

La mayoría de las distribuciones de Linux incluyen el archivo binario del kernel como un paquete que puede instalar fácilmente utilizando un sistema de administración de paquetes común (como Debian `apt-get` o Red Hat `yum`). El paquete instala el archivo binario del kernel en la ubicación correcta y realiza las modificaciones necesarias en el menú del gestor de arranque GRUB para arrancar usando el nuevo kernel. Esto hace que la instalación de un nuevo kernel sea casi sencilla.
### Módulos del Kernel
El kernel de Linux necesita controladores de dispositivos para comunicarse con los dispositivos de hardware instalados en su sistema Linux. Sin embargo, compilar controladores de dispositivos para todos los dispositivos de hardware conocidos en el kernel generaría un archivo binario del kernel extremadamente grande.

Para evitar esa situación, el kernel de Linux utiliza módulos del kernel, que son archivos de controladores de hardware individuales que se pueden vincular al kernel en tiempo de ejecución. De esa manera, el sistema puede vincular solo los módulos necesarios para el hardware presente en su sistema.

Si el kernel está configurado para cargar módulos de dispositivos de hardware, los archivos de los módulos individuales también deben estar disponibles en el sistema. Si está compilando un nuevo kernel de Linux, también deberá compilar los módulos de hardware junto con el nuevo kernel.
Los archivos de módulo se pueden distribuir como código fuente que debe compilarse o como archivos de objetos binarios en el sistema Linux que están listos para vincularse dinámicamente al programa binario del núcleo principal. Si los archivos del módulo se distribuyen como archivos de código fuente, debe compilarlos para crear el archivo de objeto binario. La extensión de archivo `.ko` se utiliza para identificar los archivos de objetos del módulo.

La ubicación estándar para almacenar archivos de objetos de módulo es el directorio `/lib/modules`. Aquí es donde las utilidades del módulo de Linux (como `insmod` y `modprobe`) buscan archivos de biblioteca de objetos del módulo de forma predeterminada.
### Fuente del Kernel
Si planea recompilar el archivo binario del kernel usted mismo, necesitará tener los archivos de código fuente originales para el kernel de Linux. Puede obtener los archivos de código fuente del kernel de Linux utilizando dos métodos diferentes:
- Descargue el código fuente del kernel desde el repositorio principal de desarrollo del kernel de Linux.
- Instale el código fuente del kernel desde el repositorio de software para su distribución de Linux específica.

El sitio web www.kernel.org mantiene el repositorio oficial de las versiones del kernel de Linux. El repositorio mantiene la versión estable actual del kernel, que se recomienda para uso en producción, además de la última versión de desarrollo. Si está buscando el código fuente del kernel más reciente, este es el lugar al que debe acudir.

Como parte de los requisitos de código abierto, las distribuciones individuales de Linux también publican el código fuente del kernel de Linux como paquetes de distribución, disponibles para su instalación desde sus sitios de repositorio de software individuales. Esta es la forma más segura de instalar el kernel de Linux, porque cada distribución de Linux pone a disposición sólo el código fuente del kernel de Linux que se sabe que funciona correctamente en el entorno de la distribución.
Ya sea que descargue un paquete de código fuente de Linux desde el sitio web www.kernel.org o lo instale desde el repositorio de su distribución, debe extraer los archivos de código fuente en `/usr/src/linux`.
### Parches del Kernel
Las versiones del kernel de Linux tienen versiones incrementales para correcciones de errores y parches de seguridad (como pasar de la versión 4.3.0 a la 4.3.1). Si bien puede recompilar un nuevo kernel descargando el código fuente completo para la versión incremental, si ya tiene el código fuente para la versión original, existe una forma más sencilla de actualizar a la nueva versión.

Una versión de parche es un paquete de código fuente especial que contiene solo los cambios aplicados a la versión principal del código fuente del kernel para llegar a la versión incremental (por ejemplo, actualizar desde la versión 4.3.0 del kernel a la versión de parche 4.3.1). Simplemente descargue el paquete de código fuente del parche, use el comando de parche de Linux para aplicar las actualizaciones del parche a los archivos de código fuente del kernel existentes en su sistema y luego vuelva a compilar el kernel.

Al trabajar con parches para versiones incrementales posteriores (como actualizar 4.3.1 a
4.3.2), primero debe desinstalar el parche anterior (4.3.1) para volver a la versión original (4.3.0) y luego aplicar el parche para la versión incremental 4.3.2, porque cada versión de parche se basa en la actualización. el código de lanzamiento original. La desinstalación de parches también se realiza mediante el comando `patch` utilizando la opción `-R`.
### Encabezados del núcleo
El kernel de Linux está escrito principalmente utilizando el lenguaje de programación C. Parte del lenguaje de programación C es una característica llamada archivos de encabezado. Los archivos de encabezado le dicen al compilador de C qué archivos de biblioteca se requieren para compilar el código fuente del kernel. Estos mismos archivos de biblioteca también son vitales para compilar cualquier archivo de código fuente de módulo.

Si solo necesita compilar módulos a partir del código fuente, no necesita descargar los archivos completos del código fuente del kernel de Linux, solo los archivos de encabezado del kernel. Afortunadamente, la mayoría de las distribuciones de Linux incluyen paquetes solo para los archivos de encabezado del kernel relacionados con la versión del kernel instalada. Esto facilita la compilación de módulos si está experimentando con hardware nuevo.

Los archivos de encabezado del kernel normalmente se instalan en la estructura de directorios `/usr/src/linux/` en distribuciones basadas en Debian o en la estructura de directorios `/usr/src/kernels` en distribuciones basadas en Red Hat, y usan la extensión de archivo `.h`.
###  Documentación del Kernel
Otra parte importante de los archivos del kernel de Linux es la documentación del kernel. La documentación del kernel está dividida en muchos archivos de texto separados, detallando qué hace cada archivo de código fuente dentro de la estructura del kernel. Si planea trabajar con el código fuente del kernel de Linux, es una buena idea tener a mano los archivos de documentación del kernel.

Debido al tamaño de los archivos, los archivos de documentación del kernel a menudo se instalan por separado del paquete de código fuente del kernel en las versiones de distribución, pero si descarga el código fuente del kernel desde el sitio web www.kernel.org, se incluyen. Los archivos de documentación del kernel generalmente se instalan en la estructura de directorios `/usr/src/linux/Documentation`, pero pueden estar en la estructura de directorios `/usr/src/kernels` para sistemas basados en Red Hat.
### Versiones del Kernel
Una de las partes más confusas de trabajar con el kernel de Linux es el sistema de versiones. A lo largo de la historia del kernel de Linux se han implementado seis versiones diferentes del sistema. Esta sección analiza los diferentes números de versión del kernel y describe cómo interpretar lo que significa cada uno.
### Historial de versiones del kernel de Linux

En abril de 1991, Linus Torvalds, de 21 años, empezó a trabajar en unas simples ideas para un núcleo de un sistema operativo. Comenzó intentando obtener un núcleo de sistema operativo gratuito similar a Unix que funcionara con microprocesadores Intel 80386. Para ello tomó como base al sistema Minix (un clon de Unix) e hizo un núcleo monolítico compatible que inicialmente requería software de Minix para funcionar.​ El 26 de agosto de 1991 Torvalds escribió en el grupo de noticias comp.os.minix:

```
"Estoy haciendo un sistema operativo (gratuito, solo un pasatiempo, no será nada grande ni profesional como GNU para clones AT 386(486). Llevo en ello desde abril y está empezando a estar listo. Me gustaría saber su opinión sobre las cosas que les gustan o disgustan en minix, ya que mi SO tiene algún parecido con él. Actualmente he portado bash(1.08) y gcc(1.40), y parece que las cosas funcionan. Esto implica que tendré algo práctico dentro de unos meses..."
```

Tras dicho mensaje, muchas personas ayudaron con el código. En septiembre de 1991 se lanzó la versión 0.01 de Linux. Tenía 10.239 líneas de código. En octubre de ese año (1991), salió la versión 0.02 de Linux; luego, en diciembre se lanzó la versión 0.11(1991). Esta versión fue la primera en ser self-hosted (autoalbergada). Es decir, Linux 0.11 podía ser compilado por una computadora que ejecutase Linux 0.11, mientras que las versiones anteriores de Linux se compilaban usando otros sistemas operativos. Cuando lanzó la siguiente versión, Torvalds adoptó la GPL como su propio boceto de licencia, la cual no permite su redistribución con otra licencia que no sea GPL. Antes de este cambio, se impedía el cobro por la distribución del código fuente.

Se inició un grupo de noticias llamado alt.os.linux y el 19 de enero de 1992 se publicó en ese grupo la primera publicación (post). El 31 de marzo, alt.os.linux se convirtió en comp.os.linux. XFree86, una implementación del X Window System, fue portada a Linux, la versión del núcleo 0.95 fue la primera en ser capaz de ejecutarla. Este gran salto de versiones (de 0.1x a 0.9x) fue por la sensación de que una versión 1.0 acabada no parecía estar lejos. Sin embargo, estas previsiones resultaron ser un poco optimistas: desde 1993 hasta principios de 1994 se desarrollaron 15 versiones diferentes de 0.99 (llegando a la versión 0.99r15).

El 14 de marzo de 1994, salió Linux 1.0.0, que constaba de 176.250 líneas de código. En marzo de 1995 se lanzó Linux 1.2.0, que ya estaba compuesto de 310.950 líneas de código.
### Cronología 
***1991***: El núcleo de Linux es anunciado públicamente el 25 de agosto por el estudiante finlandés de 21 años Linus Benedict Torvalds.16​ La versión 0.01 es lanzada públicamente el 17 de septiembre.
***1992***: El núcleo de Linux cambia de licencia a la GPL de GNU. Se crean las primeras distribuciones de Linux.
***1993***: Más de 100 desarrolladores trabajan en el núcleo de Linux. Con su ayuda, el núcleo se adapta al entorno GNU, lo que crea un amplio espectro de tipos de aplicaciones para Linux. Se lanza por primera vez la distribución de Linux más antigua que existe actualmente, Slackware. Más tarde en el mismo año, se establece el proyecto Debian. Hoy en día es la distribución comunitaria más grande.
***1994***: Torvalds considera que todos los componentes del núcleo están completamente maduros: lanza la versión 1.0 de Linux. El proyecto XFree86 contribuye con una interfaz gráfica de usuario (GUI). Los fabricantes comerciales de distribuciones de Linux, como Red Hat y SUSE, publican la versión 1.0 de sus distribuciones de Linux.
***1995***: Linux se porta a la arquitectura DEC Alpha y a la Sun SPARC. En los años siguientes se porta a un número cada vez mayor de plataformas.
***1996***: Se lanza la versión 2.0 del núcleo de Linux. El núcleo ahora puede servir a varios procesadores al mismo tiempo utilizando multiprocesamiento simétrico (SMP), convirtiéndose así en una alternativa seria para muchas empresas.
***1998***: Muchas empresas importantes como IBM, Compaq y Oracle anuncian su apoyo a Linux. La catedral y el bazar se publica por primera vez como un ensayo (más tarde como un libro), lo que resulta en que Netscape publique públicamente el código fuente de su suite de navegadores web Netscape Communicator. Las acciones de Netscape y la referencia al ensayo18​ llaman la atención del popular prensa técnica sobre el modelo de desarrollo de código abierto de Linux. Además, un grupo de programadores comienza a desarrollar la interfaz gráfica de usuario KDE. Linux aparece por primera vez en la lista TOP500 de supercomputadoras más rápidas.​ El puerto ARM (iniciado en 199420​21​) se fusiona.
***1998***: David A. Bader inventa el primer supercomputador basado en Linux utilizando piezas de consumo.
***1999***: Un grupo de desarrolladores comienza a trabajar en el entorno gráfico GNOME, destinado a convertirse en un reemplazo gratuito de KDE, que en ese momento dependía del entonces propietario kit de herramientas Qt. Durante el año, IBM anuncia un extenso proyecto para el soporte de Linux. Se lanza la versión 2.2 del núcleo de Linux.
***2000***: Dell anuncia que ahora es el segundo proveedor mundial de sistemas basados en Linux y el primer fabricante importante en ofrecer Linux en toda su línea de productos.
***2001***: Se lanza la versión 2.4 del núcleo de Linux.
***2002***: Los medios de comunicación informan que "Microsoft mató a Dell Linux"
***2003***: Se lanza la versión 2.6 del núcleo de Linux.
***2004***: El equipo de XFree86 se divide y se une al organismo existente de estándares X para formar la Fundación X.Org, lo que resulta en un desarrollo sustancialmente más rápido del servidor X para Linux.
***2005***: El proyecto openSUSE comienza una distribución gratuita de la comunidad de Novell. También el proyecto OpenOffice.org introduce la versión 2.0 que luego comenzó a admitir los estándares OASIS OpenDocument.
***2006***: Oracle lanza su propia distribución de Red Hat Enterprise Linux. Novell y Microsoft anuncian cooperación para una mejor interoperabilidad y protección mutua de patentes.
***2007***: Dell comienza a distribuir laptops con Ubuntu preinstalado.
***2009***: La capitalización de mercado de Red Hat iguala a la de Sun, interpretada como un momento simbólico para la "economía basada en Linux".
***2011***: Se lanza la versión 3.0 del núcleo de Linux.
***2012***: Los ingresos agregados del mercado de servidores Linux superan los del resto del mercado de Unix.
***2013***: El sistema operativo basado en Linux de Google, Android, reclama el 75% del mercado de teléfonos inteligentes, en términos de la cantidad de teléfonos enviados.
***2014***: Ubuntu alcanza 22.000.000 de usuarios.
***2015***: Se lanza la versión 4.0 del núcleo de Linux.
***2017***: Todos los sistemas de la lista TOP500 de supercomputadoras más rápidas ejecutan Linux.19​
***2019***: Se lanza la versión 5.0 del núcleo de Linux.
***2022***: Se lanza la versión 6.0 del núcleo de Linux.
### Compilando un kernel
En la mayoría de los entornos Linux normales, nunca tendrá que preocuparse por compilar un nuevo kernel. Todas las principales distribuciones de Linux hacen eso por usted y lanzan los nuevos núcleos como paquetes de software en sus repositorios. La actualización del kernel suele ser automática y se realiza mediante el proceso de actualización automática de software de la distribución.

Sin embargo, puede haber ocasiones en las que desee experimentar con un nuevo kernel, como al implementar nuevo hardware o probar nuevas funciones del kernel. Si decide emprender la tarea de compilar su propio kernel de Linux, el proceso implica cinco pasos:

1. Obtención del código fuente
2. Crear un archivo de configuración basado en el hardware del sistema.
3. Compilando el código fuente
4. Compilación e instalación de archivos de módulo.
5. Instalación del nuevo archivo binario del kernel
### Obtención del código fuente
Como se menciona en la sección "Fuente del kernel", hay dos formas de obtener el código fuente del kernel de Linux. Puede descargar la versión más reciente directamente desde el sitio web oficial www.kernel.org, o puede obtenerla con la mayoría de las distribuciones de Linux, que incluyen un paquete de software que contiene el código fuente del kernel para la versión del kernel instalada más recientemente.

Si simplemente está experimentando con diferentes funciones del kernel en su distribución de Linux específica, le recomendamos que instale solo el paquete de software del kernel desde el repositorio de su distribución. Esto garantiza que está trabajando con un kernel que sabe que funciona en su entorno Linux. Sin embargo, la mayoría de las distribuciones de Linux están algo atrasadas en mantenerse al día con las últimas versiones del kernel. Si está intentando trabajar con las últimas funciones de hardware o kernel, es posible que deba descargar e instalar el código fuente actual estable o de desarrollo directamente desde el sitio web www.kernel.org.

Cuando vaya al sitio web www.kernel.org, verá una matriz de diferentes versiones del kernel disponibles, junto con diferentes opciones de descarga (como descargar solo el parche incremental o el código fuente completo). La versión de producción más reciente del kernel está etiquetada como estable. Las versiones anteriores del kernel están etiquetadas como de largo plazo, mientras que la versión de desarrollo más reciente está etiquetada como principal.
Los paquetes de código fuente se empaquetan usando la utilidad de archivo tar y se comprimen usando la utilidad de compresión `xz`. Necesitará ambas utilidades instaladas en su sistema para poder extraer los archivos del código fuente.

Para descargar un paquete completo de código fuente del kernel, haga clic en el enlace `tar.xz` para obtener la versión que necesita. El nombre del archivo de descarga tendrá el formato `linux-version.tar.xz` donde versión es la versión del kernel. Para extraer el archivo de código fuente, utilice el siguiente comando:

```sh
tar xvf linux-version.tar.xz
```

El comando tar extraerá todos los archivos de código fuente en una carpeta llamada `linuxversion`, creando automáticamente las subcarpetas necesarias contenidas en el paquete.

Puede extraer los archivos del código fuente del kernel en una carpeta debajo de su directorio de inicio si solo desea examinar los archivos y la documentación. Sin embargo, si planea compilar e instalar el kernel en su sistema Linux, es mejor extraer los archivos del código fuente en la estructura de carpetas `/usr/src/`. No coloque los nuevos archivos de código fuente directamente en la carpeta `/usr/src/linux`; en su lugar, cree un enlace entre la carpeta `/usr/src/linux` y la carpeta del código fuente que creó al extraer los archivos:

```sh
ln /usr/src/linux-4.3.3 /usr/src/linux
```

### Creando el archivo de configuración
Antes de poder compilar el nuevo kernel a partir del código fuente, necesita determinar qué características del kernel desea incluir en su nuevo archivo binario del kernel. Esto se hace usando un archivo de configuración del kernel.

El archivo de configuración del kernel es un archivo de texto que contiene líneas separadas para cada característica del kernel, que muestra el nombre de la característica y su configuración. El archivo de configuración del kernel se almacena en el archivo `/usr/src/linux/.config`. Si ya tiene instalado el código fuente del kernel, puede consultar este archivo para ver qué funciones están disponibles para la configuración. El Listado 3.4 muestra un pequeño fragmento de un archivo .config de un sistema Ubuntu.

```sh
CONFIG_64BIT=y
CONFIG_X86_64=y
CONFIG_X86=y
CONFIG_INSTRUCTION_DECODER=y
CONFIG_PERF_EVENTS_INTEL_UNCORE=y
CONFIG_OUTPUT_FORMAT="elf64-x86–64"
CONFIG_ARCH_DEFCONFIG="arch/x86/configs/x86_64_defconfig"
CONFIG_LOCKDEP_SUPPORT=y
CONFIG_STACKTRACE_SUPPORT=y
CONFIG_HAVE_LATENCYTOP_SUPPORT=y
CONFIG_MMU=y
CONFIG_NEED_DMA_MAP_STATE=y
CONFIG_NEED_SG_DMA_LENGTH=y
CONFIG_GENERIC_ISA_DMA=y
CONFIG_GENERIC_BUG=y
CONFIG_GENERIC_BUG_RELATIVE_POINTERS=y
CONFIG_GENERIC_HWEIGHT=y
CONFIG_ARCH_MAY_HAVE_PC_FDC=y
CONFIG_RWSEM_XCHGADD_ALGORITHM=y ...
```

Necesita establecer muchas opciones de configuración para el kernel. Para crear el archivo `.config`, no es necesario ejecutar cada línea manualmente. En su lugar, puede utilizar un script automatizado que haga preguntas para cada función y cree el archivo `.config` en función de sus respuestas a las preguntas.

La utilidad `make` ejecuta el script contenido en el código fuente. La utilidad `make` utiliza objetivos `make` para determinar qué script ejecutar. Hay muchos objetivos diferentes que puedes utilizar.
El destino `make config` es el script básico que se ejecutará para crear el archivo de configuración.

Hace muchas preguntas sobre cada característica que puede incluir en el kernel. El Listado 3.5 muestra algunas de las preguntas que se formulan.

```sh
make config 
...
*
* Linux/x86 4.3.3 Kernel Configuration
*
64-bit kernel (64BIT) [Y/n/?] y
*
*   General setup
*
Cross-compiler tool prefix (CROSS_COMPILE) []
Compile also drivers which will not load (COMPILE_TEST) [N/y/?]
Local version—append to kernel release (LOCALVERSION) []
Automatically append version information to the version string (LOCALVERSION_
AUTO) [N/y/?]
Kernel compression mode
> 1. Gzip (KERNEL_GZIP)
  2. Bzip2 (KERNEL_BZIP2)
  3. LZMA (KERNEL_LZMA)
  4. XZ (KERNEL_XZ)
  5. LZO (KERNEL_LZO)
  6. LZ4 (KERNEL_LZ4)choice[1–6?]:
Default hostname (DEFAULT_HOSTNAME) [(none)]
Support for paging of anonymous memory (swap) (SWAP) [Y/n/?]
System V IPC (SYSVIPC) [Y/n/?]
POSIX Message Queues (POSIX_MQUEUE) [Y/n/?]
Enable process_vm_readv/writev syscalls (CROSS_MEMORY_ATTACH) [Y/n/?]
open by fhandle syscalls (FHANDLE) [Y/n/?] uselib syscall (USELIB) [Y/n/?] (NEW)
Auditing support (AUDIT) [Y/?] y
Enable system-call auditing support (AUDITSYSCALL) [Y/n/?]
...
```

Si bien la mayoría de las preguntas tienen respuestas predeterminadas que normalmente puedes usar, revisar tantas preguntas no es una forma eficiente de crear el archivo de configuración. Afortunadamente, puedes utilizar algunos scripts de acceso directo adicionales especificando diferentes objetivos:
- defconfig: crea un archivo de configuración predeterminado según el tipo de sistema detectado
- oldconfig: actualiza un archivo de configuración existente solo con las nuevas funciones
- menuconfig: utiliza un sistema de menú basado en texto que le permite seleccionar qué funciones incluir
- xconfig: crea un menú gráfico que le permite seleccionar qué funciones incluir
- gconfig: utiliza el menú gráfico GTK que le permite seleccionar qué funciones incluir

El objetivo xconfig produce un menú fácil de usar para el sistema de escritorio GNOME o KDE, como se muestra en la Figura 3.3.

Los menús de configuración gráfica son útiles porque dividen la multitud de preguntas en categorías para ayudar a que los cambios sean más manejables. El panel izquierdo muestra las principales categorías de ajustes de configuración, como memoria, sistema de archivos y funciones de red. Cuando haces clic en el tema de una categoría principal, el panel superior derecho muestra las subopciones disponibles dentro de la categoría. Cuando hace clic en una subopción, aparece una explicación de la opción en el panel inferior derecho.

![](img/3.3.png)

Cuando haya terminado de completar la configuración de categorías y subopciones, guarde la configuración haciendo clic en el icono del disco en la barra de herramientas en la parte superior de la ventana. Una vez que hayas creado el archivo `/usr/src/linux/.config`, está listo para comenzar a compilar el nuevo kernel.
### Compilación e instalación del kernel
Una vez que haya creado el archivo de configuración para el kernel, estará listo para comenzar el proceso de compilación. Gracias a la utilidad make, este paso es muy sencillo.
Primero, si hizo algún intento previo de compilar el kernel, querrá eliminar los archivos objeto antiguos creados usando el objetivo limpio:

```sh
make clean
```

Luego, si desea crear un archivo binario del kernel sin comprimir, simplemente ingrese el comando

```sh
make
```

Luego, el script se hará cargo y compilará todo el código del kernel para producir el nuevo kernel. (Esté preparado; este proceso llevará mucho tiempo). Si prefiere crear un archivo de kernel comprimido, simplemente use el destino `bzImage`:

```sh
make bzImage
```

A medida que funciona el proceso de compilación, verá muchos mensajes pasar por la consola, como estos:

```sh
  CC      lib/list_sort.o
  CC      lib/uuid.o
  CC      lib/flex_array.o
  CC      lib/iov_iter.o
  CC      lib/clz_ctz.o
  CC      lib/bsearch.o
  CC      lib/find_bit.o
  CC      lib/llist.o
  CC      lib/memweight.o
```

Las líneas `CC` indican archivos de código objeto que se están creando. Las líneas `LD` indican archivos de código objeto que se están vinculando para crear el archivo ejecutable. Cuando se complete el proceso, el archivo binario final del kernel debe estar en la carpeta `/usr/src/linux/arch/x86/boot` como `bzImage`.
Una vez que se complete el proceso de compilación, estará listo para instalar el nuevo archivo binario del kernel.

Puede instalar manualmente el archivo binario del kernel simplemente copiando el archivo `bzImage` en la carpeta `/boot` de su sistema. Querrá agregar el número de versión al archivo para poder distinguirlo de los otros archivos binarios del kernel. Nómbralo usando el nombre de archivo `vmlinuz`, que es reconocido por la mayoría de las distribuciones de Linux:

```sh
cp /usr/src/linux/arch/x86/boot/bzImage /boot/vmlinuz-4.3.3
```

Además del archivo binario del kernel, también hay un archivo `System.map` en la carpeta `/usr/src/linux` asociado con el archivo binario del kernel generado. El archivo `System.map` se utiliza para depurar el kernel, por lo que no es necesario, pero también puede ser útil copiarlo en la carpeta `/boot`. Al igual que con el archivo binario del kernel, querrás agregar la versión del kernel al final del nombre del archivo `System.map`:

```sh
cp /usr/src/linux/System.map /boot/System.map-4.3.3
```

Como probablemente puedas adivinar, también hay un destino de script `make` para instalar automáticamente los archivos binarios del kernel y `System.map`:

```sh
make install
```

Esto copia automáticamente el nuevo binario del kernel desde la carpeta `/usr/src/linux` a la ubicación adecuada en la carpeta `/boot` de su gestor de arranque. Sin embargo, aún necesitará cambiar el nombre del nuevo archivo binario del kernel para agregarle la versión del kernel, separándolo de los archivos del kernel más antiguos instalados.
### Compilación e instalación de módulos
Después de compilar e instalar el kernel, querrás compilar e instalar la versión más nueva de los módulos necesarios para tu sistema. Al igual que con la compilación del kernel, utiliza la utilidad `make` para crear e instalar los nuevos archivos de la biblioteca de objetos del módulo.
Primero, deberá crear los archivos de la biblioteca de objetos del módulo utilizando el destino del módulo:

```sh
make modules
```

Una vez que se complete, puede instalarlos usando el destino de instalación `make_modules`:

```sh
make modules_install
```

Este script instala los módulos en la carpeta `/lib/modules/kernel-version/`, donde la versión coincide con la versión del kernel. El kernel buscará en esta carpeta de forma predeterminada cuando
necesita cargar módulos. Esto también se aplica a cualquier comando de línea de comandos utilizado para cargar módulos manualmente. 
### Crear un disco RAM inicial
Una desventaja de utilizar módulos del kernel es que el kernel debe cargar cada uno de los módulos en el momento del arranque para acceder a los dispositivos de hardware. Sin embargo, si hay módulos que controlan cómo el kernel lee el disco duro (como con un sistema RAID) o módulos para leer un sistema de archivos específico (como ReiserFS), esa situación causará un problema. (¿Cómo puede el kernel cargar un módulo necesario para leer el sistema de archivos en el que está almacenado el módulo?)

Para resolver ese problema, los desarrolladores de Linux crearon la idea de un disco RAM inicial (también llamado `initrd`). El disco RAM inicial es un sistema de archivos contenido en un archivo que el kernel carga en la memoria en el momento del arranque como un disco. El kernel puede leer y cargar cualquier archivo contenido en el disco RAM inicial mientras arranca. Todo lo que necesita hacer es crear un archivo de disco RAM inicial que contenga los archivos del módulo necesarios para iniciar el sistema. Una vez que se inicia el sistema, el disco RAM inicial se elimina de la memoria para liberar espacio en la memoria.

Hay dos utilidades comunes que se utilizan para crear un archivo de disco RAM inicial, según la distribución de Linux que utilice. 
### La utilidad `mkinitrd`
Las distribuciones de Linux basadas en Red Hat (como Red Hat Enterprise Linux, Fedora y CentOS) utilizan la utilidad `mkinitrd` para generar un archivo de disco RAM inicial y copiar los archivos del módulo en él. El formato general del comando es:

```sh
mkinitrd outputfile version
```

donde archivo de salida es el nombre del archivo de disco RAM inicial que se creará y versión es la versión del kernel para la cual se crea el archivo. Hay algunas opciones de línea de comandos que puede utilizar para el comando `mkinitrd`. Se muestran en la Tabla 3.3.


| Option                | Description                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------- |
| `--builtin=module`    | Assume the module is built into the kernel, even if it’s not.                             |
| `--force`             | Allow the output file to be overwritten if it already exists                              |
| `--fstab=filename`    | Determine what filesystem support is required to read the specified filename              |
| `--image-version`     | Add the kernel version to the generated initial RAM disk image file                       |
| `--nocompress`        | Force the image file to be uncompressed. The default is to create a compressed image file |
| `--omit-lvm-modules`  | Omit logical volume manager modules from the image                                        |
| `--omit-raid-modules` | Omit RAID disk modules from the image                                                     |
| `--omit-scsi-modules` | Omit SCSI disk modules from the image.                                                    |
| `--preload=module`    | Load the specified module before the SCSI modules are loaded.                             |
| `--verbose`           | Display verbose information as each module is loaded                                      |
| `--version`           | Display the version of the mkinitrd program                                               |
| `--with=module`       | Load the specified module before the SCSI modules are loaded                              |

En la mayoría de las situaciones, puede ejecutar el comando `mkinitrd` sin ninguna opción para generar el archivo de imagen de disco RAM inicial:

```sh
mkinitrd /boot/initrd.img-4.3.3 4.3.3
```

Debido a que el archivo de disco RAM inicial se utiliza en el momento del arranque, la mayoría de las distribuciones de Linux lo almacenan en la misma carpeta donde se encuentra el archivo binario del kernel, generalmente la carpeta `/boot`.
### La utilidad `mkinitramfs`
Las distribuciones de Linux basadas en Debian (como Debian y Ubuntu) utilizan la utilidad `mkinitramfs` para generar el archivo de disco RAM inicial. El formato general del comando es:

```sh
mkinitramfs –o outputfile version
```

donde archivo de salida es el archivo de imagen a crear y versión es la versión del kernel. La Tabla 3.4 enumera las opciones que están disponibles.


| Option                                | Description                                                                  |
| ------------------------------------- | ---------------------------------------------------------------------------- |
| `-c`                                  | Create a compressed image file.                                              |
| `-d` `confdir`                        | Set the configuration directory.                                             |
| `-k`                                  | Retain the temporary directory created to build the initial RAM disk file.   |
| `-o` `outputfile`                     | Define the output image filename.                                            |
| `-r` `root`                           | Set the root partition used by the bootloader.                               |
| `--supported-host-version=hversion`   | Determine if it can create an image for the specified running kernel version |
| `--supported-target-version=tversion` | Determine if it can create an image for the specified kernel version.        |

En la mayoría de las situaciones, puedes usar la opción `-o` para especificar el archivo de imagen de salida:

```sh
mkinitramfs –o /boot/initramfs-4.3.3.img 4.3.3
```

La mayoría de las distribuciones de Debian Linux también almacenan el archivo del disco RAM inicial en la misma carpeta que el archivo binario del kernel, la carpeta `/boot`.
### Arrancando el nuevo kernel
Una vez que haya compilado e instalado los archivos binarios del kernel y de imagen de disco RAM inicial, estará listo para usarlos para iniciar su sistema Linux. Hoy en día, la mayoría de las distribuciones de Linux utilizan el programa de arranque GRUB Legacy o GRUB2 para iniciar el sistema. Si su distribución de Linux utiliza el gestor de arranque GRUB Legacy, debe actualizar manualmente el archivo de configuración de GRUB `/boot/grub/menu.lst` o `/boot/grub/grub.conf` para agregar una nueva sección de arranque para el nuevo kernel. La nueva sección de inicio debe comenzar con un título e incluir el nuevo archivo binario del kernel y los archivos de imagen del disco RAM inicial:

```sh
title Test (4.3.3)    
	root (hd0,0)
	kernel /vmlinuz-4.3.3 ro root=/dev/sda1
	initrd /initrd.img-4.3.3
```

Si su distribución de Linux usa el gestor de arranque GRUB2, después de instalar el nuevo binario del kernel en el menú de inicio, solo necesita ejecutar el comando `update-grub`:

```sh
update-grub
```

El comando `update-grub` escanea la carpeta `/boot` y agrega automáticamente el nuevo binario del kernel al menú de inicio de GRUB. También actualiza el archivo de configuración `grub.cfg` para incluir el nuevo archivo de disco RAM inicial que creó e instaló.

Si por alguna razón el comando `update-grub` no detecta automáticamente el nuevo archivo binario del kernel, tendrá que agregar una entrada manualmente a uno de los archivos de opciones de arranque en la carpeta `/etc/grub.d`. Puede elegir uno de los archivos de opciones de arranque personalizados, como el archivo `40_custom`. Simplemente agregue la nueva entrada que apunta al nuevo kernel al final de las entradas existentes:

```sh
menuentry "Test (4.3.3)"    
	set root=(hd0,1)
	linux /vmlinuz-4.3.3 ro root=/dev/sda1    
	initrd /initrd-4.3.3
```

Después de agregar la nueva entrada, guarde el archivo y luego ejecute el comando `update-grub`. Debería agregar la nueva opción del kernel al archivo de configuración `/boot/grub/grub.cfg`.

Cuando reinicie su sistema Linux, debería ver la nueva opción binaria del kernel en las opciones de arranque. Si está utilizando una distribución de Linux que oculta el menú de inicio de GRUB de forma predeterminada, mantenga presionada la tecla Shift cuando inicie y debería aparecer. En la distribución Ubuntu Linux, también deberá seleccionar la entrada del menú Opciones avanzadas para Ubuntu para ver la lista de kernels disponibles para arrancar; luego simplemente seleccione su nueva opción de kernel.
### Creando un paquete de kernel
Si se encuentra en un entorno que admite muchas estaciones de trabajo Linux, intentar compilar y copiar un nuevo binario del kernel en todas las estaciones de trabajo puede resultar algo tedioso. Afortunadamente, el código fuente del kernel proporciona algunos objetivos de creación que pueden ayudar:
- `rpm-pkg`: crea paquetes RPM de origen y binarios.
- `binrpm-pkg`: crea un paquete RPM binario
- `deb-pkg`: crea un paquete DEB binario

Después de ejecutar el comando `make` con el destino apropiado, el archivo binario del kernel se incluirá como parte del paquete generado. Luego puede utilizar la herramienta de administración de paquetes de software estándar (`rpm` para Red Hat o `dpkg` para Debian) para instalar el nuevo paquete binario del kernel en cada estación de trabajo.
### Mantenimiento del núcleo
Una vez que tenga instalado un kernel de Linux, hay algunos pasos que puede seguir para asegurarse de que todo funcione correctamente. Esta sección lo guía a través de los comandos de la línea de comandos que debe conocer para monitorear el funcionamiento del kernel, incluido el seguimiento de los módulos instalados, la detección de dispositivos de hardware y la resolución de problemas del kernel.
### Trabajar con archivos de módulo
Debería estar familiarizado con algunos archivos diferentes cuando trabaje con módulos. Ya has visto que los módulos necesarios para soportar un kernel se almacenan en la carpeta `/lib/modules`. Cada kernel tiene su propia carpeta para sus propios módulos (como `/lib/modules/4.3.3`), lo que le permite crear módulos separados para cada versión del kernel en el sistema si es necesario.
Los módulos que el kernel cargará en el momento del arranque se enumeran en el archivo `/etc/modules` en sistemas Debian o en archivos de texto separados en la carpeta `/etc/modules-load.d` para sistemas basados en Red Hat. La mayoría de los módulos de hardware se pueden cargar dinámicamente, porque el sistema detecta automáticamente los dispositivos de hardware, por lo que es posible que este archivo no contenga muchos módulos.

Si es necesario, puede personalizar un módulo del kernel para definir los parámetros únicos necesarios, como la configuración de hardware necesaria para que funcione el dispositivo. Las configuraciones del módulo del kernel se almacenan en el archivo de configuración `/etc/conf.modules`.

Finalmente, algunos módulos pueden depender de que otros módulos se carguen primero para funcionar correctamente. Estas relaciones se definen en el archivo `module.dep` y se almacenan en la carpeta `/lib/modules/version/`, donde versión es la versión del kernel. El formato para cada entrada es `modulefilename`: `dependencyfilename1` `dependencyfilename2...`

Cuando utiliza el destino `module_install` para instalar los módulos, llama a la utilidad `depmod`, que determina las dependencias del módulo y genera el archivo `module.dep` automáticamente. Si modifica o agrega algún módulo después de eso, debe ejecutar manualmente el comando `depmod` para actualizar el archivo `module.dep`.

Si compila sus propios módulos fuera de los módulos estándar del kernel, tiene otro problema que considerar. Dado que los módulos se compilan para un kernel específico, cada vez que el sistema actualiza el kernel, debe volver a compilar sus módulos personalizados.

Una solución a este problema es la compatibilidad con módulos de kernel dinámicos (DKMS). El sistema DKMS proporciona una manera de registrar sus módulos personalizados y proporcionar instrucciones sobre cómo compilarlos e instalarlos cada vez que se instala un nuevo kernel. El programa `dkms` monitorea la versión del kernel y ejecuta automáticamente scripts para recompilar e instalar módulos cuando cambia la versión del kernel.
### Comando `module`
Puede utilizar una gran cantidad de comandos de línea de comandos para ayudarle a solucionar y solucionar problemas del módulo del kernel. Esta sección lo guiará a través de los diferentes comandos de módulo que están disponibles para ayudarlo con cualquier problema que pueda surgir con el módulo.
### Listado de Módulos
El primer comando es `lsmod`, que enumera todos los módulos instalados en su sistema. El Listado 3.6 muestra un ejemplo del uso del comando `lsmod` en un sistema Ubuntu.

```sh
lsmod

Module                  Size  Used by 
vboxsf                 39706  1 
snd_intel8x0           38153  2 
snd_ac97_codec        130285  1 snd_intel8x0 
ac97_bus               12730  1 snd_ac97_codec 
snd_pcm               102099  2 snd_ac97_codec,snd_intel8x0 
snd_page_alloc         18710  2 snd_intel8x0,snd_pcm
snd_seq_midi           13324  0 
snd_seq_midi_event     14899  1 snd_seq_midi 
snd_rawmidi            30144  1 snd_seq_midi
snd_seq                61560  2 snd_seq_midi_event,snd_seq_midi snd_seq_device         14497  3 snd_seq,snd_rawmidi,snd_seq_midi
snd_timer              29482  2 snd_pcm,snd_seq
rfcomm                 69160  0 
hid_multitouch         17407  0 
joydev                 17381  0 
snd                    69322  12
snd_ac97_codec,snd_intel8x0,snd_timer,snd_pcm,snd_seq,snd_rawmidi,snd_seq_ device,snd_seq_midi 
bnep                   19624  2 
bluetooth             391136  10 bnep,rfcomm
serio_raw              13462  0 
vboxvideo              12658  1 
drm                   303102  2 vboxvideo 
vboxguest             276728  7 vboxsf 
i2c_piix4              22155  0 
soundcore              12680  1 snd 
video                  19476  0 
mac_hid                13205  0 
parport_pc             32701  0 
ppdev                  17671  0 
lp                     17759  0
parport                42348  3 lp,ppdev,parport_pc
hid_generic            12548  0
usbhid                 52659  0
hid                   106148  3 hid_multitouch,hid_generic,usbhid
psmouse               106692  0 
ahci                   34091  3 
libahci                32716  1 ahci 
e1000                 145227  0 
pata_acpi              13038  0 
```

Observe que el comando `lsmod` también muestra qué módulos utilizan otros módulos.

Esta puede ser información crucial al intentar solucionar problemas de hardware.
### Obtener información del módulo
Si necesita más información sobre un módulo específico, use el comando `modinfo`, como se muestra en el Listado 3.7.

```sh
$ modinfo bluetooth
filename:       /lib/modules/3.13.0–63-generic/kernel/net/bluetooth/bluetooth.ko
alias:          net-pf-31 
license:        GPL version:        2.17
description:    Bluetooth Core ver 2.17 
author:         Marcel Holtmann <marcel@holtmann.org>
srcversion:     071210642A004CFE1860F30 
depends: 
intree:         Y
vermagic:       3.13.0–63-generic SMP mod_unload modversions
signer:         Magrathea: Glacier signing key
sig_key:        E2:53:28:1F:E2:65:EE:3C:EA:FC:AA:3F:29:2E:21:2B:95:F0:35:9A
sig_hashalgo:   sha512
parm:           disable_esco:Disable eSCO connection creation (bool) 
parm:           disable_ertm:Disable enhanced retransmission mode (bool)
```

El comando `modinfo` le muestra exactamente qué archivo de módulo se utiliza para admitir el módulo, junto con información detallada sobre de dónde proviene el módulo.
### Instalación de nuevos módulos
Si necesita instalar un nuevo módulo manualmente, hay dos comandos que lo ayudarán:
- `insmod`
- `modprobe`

El comando `insmod` es el más básico y requiere que especifiques el archivo de módulo exacto que deseas cargar. Como ha visto, los archivos del módulo del kernel se almacenan en la estructura de carpetas `/lib/modules`, y cada versión del kernel tiene su propia carpeta. Si busca en esa carpeta en su sistema Linux, verá una estructura de árbol de carpetas para los diferentes tipos de hardware.

Por ejemplo, los sistemas de escritorio Ubuntu Linux tienen la siguiente carpeta para los controladores de hardware Bluetooth:

```sh
/lib/modules/3.13.0–63-generic/kernel/drivers/bluetooth
```

Esta carpeta es para el kernel de Linux actualmente instalado en el sistema: 3.13.0–63. Dentro de esa carpeta hay muchos archivos de módulos de controladores de dispositivos diferentes para varios tipos de sistemas Bluetooth:

```sh
ls -l total 420
-rw-r--r--1 root root 23220 Aug 14 19:07 ath3k.ko
-rw-r--r--1 root root 14028 Aug 14 19:07 bcm203x.ko
-rw-r--r--1 root root 26332 Aug 14 19:07 bfusb.ko
-rw-r--r--1 root root 18404 Aug 14 19:07 bluecard_cs.ko
-rw-r--r--1 root root 19124 Aug 14 19:07 bpa10x.ko
-rw-r--r--1 root root 16964 Aug 14 19:07 bt3c_cs.ko
-rw-r--r--1 root root 38148 Aug 14 19:07 btmrvl.ko
-rw-r--r--1 root root 34204 Aug 14 19:07 btmrvl_sdio.ko
-rw-r--r--1 root root 17524 Aug 14 19:07 btsdio.ko
-rw-r--r--1 root root 14524 Aug 14 19:07 btuart_cs.ko
-rw-r--r--1 root root 53964 Aug 14 19:07 btusb.ko
-rw-r--r--1 root root 14188 Aug 14 19:07 btwilink.ko
-rw-r--r--1 root root 15572 Aug 14 19:07 dtl1_cs.ko
-rw-r--r--1 root root 74772 Aug 14 19:07 hci_uart.ko
-rw-r--r--1 root root 15156 Aug 14 19:07 hci_vhci.ko
```

Cada archivo `.ko` es un archivo de módulo de controlador de dispositivo independiente que puede instalar en el kernel 3.13.0–63. Para instalar el módulo, simplemente especifique el nombre del archivo en la línea de comando de `insmod`. Algunos módulos también requieren parámetros, que también debes especificar en la línea de comando:

```sh
sudo insmod /lib/modules/3.13.0–49-generic/kernel/drivers/bluetooth/
btusb.ko 
password:
```

La desventaja de usar el programa `insmod` es que puede encontrarse con módulos que dependen de otros módulos, y el programa `insmod` fallará si esos otros módulos aún no están instalados. Para facilitar el proceso, el comando `modprobe` le ayuda a resolver las dependencias de los módulos.

Otra característica interesante del comando `modprobe` es que comprende los nombres de los módulos y buscará en la biblioteca del módulo el archivo del módulo que proporciona el controlador para el nombre del módulo.

Debido a esta versatilidad, hay muchas opciones disponibles para el comando `modprobe`. La Tabla 3.5 muestra las opciones de línea de comandos que puede utilizar.

`-a`, `--all` 
		Insert all module names on the command line.
`-b`, `--use-blacklist`
		This option causes `modprobe` to apply the **blacklist** commands
		in the configuration files (if any) to module names as well.
		It is usually used by udev.
`-C`, `--config`
	    This option overrides the default configuration directory
	    (`/etc/modprobe.d`).
`-c`, `--showconfig`
	     Dump out the effective configuration from the config
	    directory and exit.
`--dump-modversions`
	    Print out a list of module versioning information required by
	    a module. This option is commonly used by distributions in
	    order to package up a Linux kernel module using module
	    versioning deps.
`-d`, `--dirname`
	    Root directory for modules, / by default.
`--first-time`
           Normally, `modprobe` will succeed (and do nothing) if told to
           insert a module which is already present or to remove a
           module which isn't present. This is ideal for simple scripts;
           however, more complicated scripts often want to know whether
           `modprobe` really did something: this option makes modprobe
           fail in the case that it actually didn't do anything.
`--force-vermagic`
           Every module contains a small string containing important
           information, such as the kernel and compiler versions. If a
           module fails to load and the kernel complains that the
           "version magic" doesn't match, you can use this option to
           remove it. Naturally, this check is there for your
           protection, so using this option is dangerous unless you know
           what you're doing.
`--force-modversion`
           When modules are compiled with CONFIG_MODVERSIONS set, a
           section detailing the versions of every interfaced used by
           (or supplied by) the module is created. If a module fails to
           load and the kernel complains that the module disagrees about
           a version of some interface, you can use "--force-modversion"
           to remove the version information altogether. Naturally, this
           check is there for your protection, so using this option is
           dangerous unless you know what you're doing.
`-f`, `--force`
           Try to strip any versioning information from the module which
           might otherwise stop it from loading: this is the same as
           using both **--force-vermagic** and **--force-modversion**.
           Naturally, these checks are there for your protection, so
           using this option is dangerous unless you know what you are
           doing.
`-i`, `--ignore-install`, `--ignore-remove`
           This option causes `modprobe` to ignore **install** and **remove**
           commands in the configuration file (if any) for the module
           specified on the command line (any dependent modules are
           still subject to commands set for them in the configuration
           file). Both **install** and **remove** commands will currently be
           ignored when this option is used regardless of whether the
           request was more specifically made with only one or other
           (and not both) of **--ignore-install** or **--ignore-remove**.
`-n`, `--dry-run`, `--show`
           This option does everything but actually insert or delete the
           modules (or run the install or remove commands). Combined
           with **-v**, it is useful for debugging problems. For historical
           reasons both **--dry-run** and **--show** actually mean the same
           thing and are interchangeable.
`-q`, `--quiet`
           With this flag, `modprobe` won't print an error message if you
           try to remove or insert a module it can't find (and isn't an
           alias or **install**/**remove** command). However, it will still
           return with a non-zero exit status. The kernel uses this to
           opportunistically probe for modules which might exist using
           request_module.
`-R`, `--resolve-alias`
           Print all module names matching an alias. This can be useful
           for debugging module alias problems.
`-r`, `--remove`
           This option causes `modprobe` to remove rather than insert a
           module. If the modules it depends on are also unused,
           `modprobe` will try to remove them too. Unlike insertion, more
           than one module can be specified on the command line (it does
           not make sense to specify module parameters when removing
           modules).
`-w`, `--wait=TIMEOUT_MSEC`
           This option causes **modprobe -r** to continue trying to remove a
           module if it fails due to the module being busy, i.e. its
           refcount is not 0 at the time the call is made. Modprobe
           tries to remove the module with an incremental sleep time
           between each tentative up until the maximum wait time in
           milliseconds passed in this option.
`-S`, `--set-version`
           Set the kernel version, rather than using [uname(2)](https://www.man7.org/linux/man-pages/man2/uname.2.html) to decide
           on the kernel version (which dictates where to find the
           modules).
`--show-depends`
           List the dependencies of a module (or alias), including the
           module itself. This produces a (possibly empty) set of module
           filenames, one per line, each starting with "insmod" and is
           typically used by distributions to determine which modules to
           include when generating initrd/initramfs images.  **Install**
           commands which apply are shown prefixed by "install". It does
           not run any of the install commands. Note that [modinfo(8)](https://www.man7.org/linux/man-pages/man8/modinfo.8.html) can
           be used to extract dependencies of a module from the module
           itself, but knows nothing of aliases or install commands.
`-s`, `--syslog`
           This option causes any error messages to go through the
           syslog mechanism (as LOG_DAEMON with level LOG_NOTICE) rather
           than to standard error. This is also automatically enabled
           when stderr is unavailable.
`-V, `--version`
           Show version of program and exit.
`-v`, `--verbose`
           Print messages about what the program is doing. Usually
           `modprobe` only prints messages if something goes wrong.

Como puede ver, el comando `modprobe` es una herramienta con todas las funciones en sí misma. Quizás la característica más útil es que le permite instalar módulos según el nombre del módulo y no tener que enumerar el nombre de archivo completo del módulo:

```sh
sudo modprobe -iv btusb
insmod /lib/modules/3.13.0–63-generic/kernel/drivers/bluetooth/btusb.ko
```

Tenga en cuenta que al agregar la opción `–v` para el modo detallado, el resultado muestra el comando `insmod` generado automáticamente por el comando `modprobe`. El comando `insmod` muestra el archivo del módulo específico utilizado para instalar el módulo.
### Quitar módulos
Normalmente, no hace daño instalar un módulo en el sistema si el dispositivo de hardware no está presente. El kernel simplemente ignora los módulos no utilizados. Sin embargo, algunos administradores de Linux prefieren mantener el kernel lo más ligero posible. Por lo tanto, los desarrolladores de Linux crearon un método para eliminar módulos innecesarios: el comando `rmmod`. El comando `rmmod` elimina un módulo especificando el nombre del módulo.

Sin embargo, su amigo el comando `modprobe` también puede eliminar módulos por usted, por lo que realmente no necesita memorizar otro comando. En su lugar, simplemente use la opción `–r` con el comando `modprobe`:

```sh
sudo modprobe -rv btusb
rmmod btusb
```

El comando `modprobe –r` invoca el comando `rmmod` automáticamente, eliminando el módulo por su nombre. Puede verificar que el módulo se haya eliminado utilizando el comando `lsmod`.
### Trabajar con hardware
Por supuesto, los módulos funcionan sólo cuando hay hardware conectado al sistema. A veces, puede tener problemas al hacer coincidir el módulo correcto con el dispositivo de hardware correcto.

Hay algunos comandos que puede utilizar para consultar los dispositivos de hardware en su sistema Linux. 
### Trabajar con tarjetas PCI
La interfaz de componentes periféricos (PCI) es un antiguo estándar de PC compatible con IBM para conectar placas de hardware a placas base de PC. El estándar se ha actualizado varias veces para adaptarse a velocidades de interfaz más rápidas, así como para aumentar el tamaño del bus de datos en las placas base. El estándar PCI Express (PCIe) se utiliza actualmente en la mayoría de los servidores y estaciones de trabajo de escritorio para proporcionar una interfaz común para tarjetas de hardware externas, como Fast Ethernet y compatibilidad con unidades SCSI externas.

El kernel de Linux admite los estándares PCI y PCIe y, por lo general, puede detectar e interactuar con una placa PCI o PCIe cuando se carga el módulo de controlador adecuado.
El comando `lspci` le permite ver las tarjetas PCI y PCIe actualmente instaladas y reconocidas en el sistema Linux. Puede incluir varias opciones de línea de comandos con el comando `lspci` para mostrar información diversa sobre las tarjetas PCI y PCIe instaladas en el sistema. La Tabla 3.6 muestra las opciones más comunes que resultan útiles.

```
**Basic display modes**
       **-m**     Dump PCI device data in a backward-compatible machine
              readable form.  See below for details.

       **-mm**    Dump PCI device data in a machine readable form for easy
              parsing by scripts.  See below for details.

       **-t**     Show a tree-like diagram containing all buses, bridges,
              devices and connections between them.

   **Display options**
       **-v**     Be verbose and display detailed information about all
              devices.

       **-vv**    Be very verbose and display more details. This level
              includes everything deemed useful.

       **-vvv**   Be even more verbose and display everything we are able to
              parse, even if it doesn't look interesting at all (e.g.,
              undefined memory regions).

       **-k**     Show kernel drivers handling each device and also kernel
              modules capable of handling it.  Turned on by default when
              **-v** is given in the normal mode of output.  (Currently
              works only on Linux with kernel 2.6 or newer.)

       **-x**     Show hexadecimal dump of the standard part of the
              configuration space (the first 64 bytes or 128 bytes for
              CardBus bridges).

       **-xxx**   Show hexadecimal dump of the whole PCI configuration
              space. It is available only to root as several PCI devices
              **crash** when you try to read some parts of the config space
              (this behavior probably doesn't violate the PCI standard,
              but it's at least very stupid). However, such devices are
              rare, so you needn't worry much.

       **-xxxx**  Show hexadecimal dump of the extended (4096-byte) PCI
              configuration space available on PCI-X 2.0 and PCI Express
              buses.

       **-b**     Bus-centric view. Show all IRQ numbers and addresses as
              seen by the cards on the PCI bus instead of as seen by the
              kernel.

       **-D**     Always show PCI domain numbers. By default, lspci
              suppresses them on machines which have only domain 0.

       **-P**     Identify PCI devices by path through each bridge, instead
              of by bus number.

       **-PP**    Identify PCI devices by path through each bridge, showing
              the bus number as well as the device number.

   **Options to control resolving ID's to names**
       **-n**     Show PCI vendor and device codes as numbers instead of
              looking them up in the PCI ID list.

       **-nn**    Show PCI vendor and device codes as both numbers and
              names.

       **-q**     Use DNS to query the central PCI ID database if a device
              is not found in the local **pci.ids** file. If the DNS query
              succeeds, the result is cached in **~/.pciids-cache** and it
              is recognized in subsequent runs even if **-q** is not given
              any more. Please use this switch inside automated scripts
              only with caution to avoid overloading the database
              servers.

       **-qq**    Same as **-q**, but the local cache is reset.

       **-Q**     Query the central database even for entries which are
              recognized locally.  Use this if you suspect that the
              displayed entry is wrong.

   **Options for selection of devices**
       **-s [[[[<domain>]:]<bus>]:][<device>][.[<func>]]**
              Show only devices in the specified domain (in case your
              machine has several host bridges, they can either share a
              common bus number space or each of them can address a PCI
              domain of its own; domains are numbered from 0 to ffff),
              bus (0 to ff), device (0 to 1f) and function (0 to 7).
              Each component of the device address can be omitted or set
              to "*", both meaning "any value". All numbers are
              hexadecimal.  E.g., "0:" means all devices on bus 0, "0"
              means all functions of device 0 on any bus, "0.3" selects
              third function of device 0 on all buses and ".4" shows
              only the fourth function of each device.

       **-d [<vendor>]:[<device>][:<class>[:<prog-if>]]**
              Show only devices with specified vendor, device, class ID,
              and programming interface.  The ID's are given in
              hexadecimal and may be omitted or given as "*", both
              meaning "any value". The class ID can contain "x"
              characters which stand for "any digit".

   **Other options**
       **-i <file>**
              Use **<file>** as the PCI ID list instead of
              /usr/local/share/pci.ids.

       **-p <file>**
              Use **<file>** as the map of PCI ID's handled by kernel
              modules. By default, lspci uses
              /lib/modules/_kernel_version_/modules.pcimap.  Applies only
              to Linux systems with recent enough module tools.

       **-M**     Invoke bus mapping mode which performs a thorough scan of
              all PCI devices, including those behind misconfigured
              bridges, etc. This option gives meaningful results only
              with a direct hardware access mode, which usually requires
              root privileges.  By default, the bus mapper scans domain.
              You can use the **-s** option to select a different domain.

       **--version**
              Shows _lspci_ version. This option should be used stand-
              alone.

   **PCI access options**
       The PCI utilities use the PCI library to talk to PCI devices (see
       [pcilib(7)](https://man7.org/linux/man-pages/man7/pcilib.7.html) for details). You can use the following options to
       influence its behavior:

       **-A <method>**
              The library supports a variety of methods to access the
              PCI hardware.  By default, it uses the first access method
              available, but you can use this option to override this
              decision. See **-A help** for a list of available methods and
              their descriptions.

       **-O <param>=<value>**
              The behavior of the library is controlled by several named
              parameters.  This option allows one to set the value of
              any of the parameters. Use **-O help** for a list of known
              parameters and their default values.

       **-H1**    Use direct hardware access via Intel configuration
              mechanism 1.  (This is a shorthand for **-A intel-conf1**.)

       **-H2**    Use direct hardware access via Intel configuration
              mechanism 2.  (This is a shorthand for **-A intel-conf2**.)

       **-F <file>**
              Instead of accessing real hardware, read the list of
              devices and values of their configuration registers from
              the given file produced by an earlier run of lspci -x.
              This is very useful for analysis of user-supplied bug
              reports, because you can display the hardware
              configuration in any way you want without disturbing the
              user with requests for more dumps.

       **-G**     Increase debug level of the library.
```