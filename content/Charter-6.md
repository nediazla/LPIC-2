![](img/sudo.png)
# Navegación por servicios de red

Hoy en día, es necesario tener su sistema Linux conectado a algún tipo de red. Ya sea por la necesidad de compartir archivos e impresoras en una red local o porque a pesar de la necesidad de conectarse a Internet para descargar actualizaciones y parches de seguridad, la mayoría de los sistemas Linux cuentan con algún tipo de conexión de red.

Este capítulo analiza cómo configurar su sistema Linux para conectarse a una red, así como también cómo solucionar problemas de conexiones de red si algo sale mal. Primero, cubre los conceptos básicos de las redes para asegurarse de que esté familiarizado con todos los términos y elementos de configuración necesarios para hablar con otros dispositivos en la red. A continuación, el capítulo examina cómo establecer esos valores de configuración en entornos de red tanto cableados como inalámbricos. Después de eso, el capítulo muestra algunas técnicas simples de solución de problemas que puede utilizar para encontrar el problema si algo sale mal.
### Conceptos básicos de redes
Antes de ver cómo Linux maneja la conectividad de red, será útil repasar los conceptos básicos de las redes de computadoras. Las redes de computadoras son la forma en que pasamos datos de un sistema informático a otro. Para ayudar a simplificar las cosas, las redes informáticas a menudo se describen como un sistema en capas. Diferentes capas desempeñan diferentes roles en el proceso de pasar los datos de un dispositivo de red a otro.

Sin embargo, existe mucho debate sobre cuál es la mejor manera de dividir las capas de red. Si bien el modelo de red OSI estándar utiliza siete capas, utilizaremos un enfoque simplificado de cuatro capas para describir las funciones de la red:
- La capa física
- La capa de red
- La capa de transporte
- La capa de aplicación
Las siguientes secciones detallan las partes contenidas en cada una de estas cuatro capas.
### La capa física
La capa física consta del hardware necesario para conectar su sistema Linux a la red. Si alguna vez ha conectado una computadora a una red doméstica o de oficina, ya está familiarizado con los dos métodos principales utilizados para conectar dispositivos de red: conexiones de red inalámbricas y por cable.

Las conexiones de red por cable utilizan una serie de conmutadores de red para conectar dispositivos de red mediante cables Ethernet especiales. El conmutador de red acepta paquetes de datos del dispositivo de red y luego envía los paquetes de datos al dispositivo de destino correcto en la red. Para instalaciones de redes de oficinas grandes, los conmutadores generalmente se conectan en un diseño en cascada para ayudar a reducir la carga de tráfico en la red. Los conmutadores se pueden interconectar para ayudar a segmentar el tráfico de la red en áreas más pequeñas. La Figura 6.1 muestra un diseño común para una red cableada.

![](img/6.1.png)

Si bien el término cableado puede hacerle pensar en cables de cobre, también puede aplicarse a conexiones de red que utilizan cables de fibra óptica. Los cables de fibra óptica utilizan luz para transmitir datos a través de un fino hilo de vidrio, logrando velocidades más rápidas y cubriendo distancias más largas que las conexiones de cobre convencionales. Aunque las redes por cable pueden ser engorrosas, proporcionan las velocidades de red más rápidas (actualmente hasta 100 gigabits por segundo). Por ese motivo, las redes por cable siguen siendo populares en entornos de servidores Linux donde es imprescindible un alto rendimiento.

Sin embargo, hoy en día, la mayoría de las redes domésticas y de pequeñas oficinas utilizan redes inalámbricas. En lugar de utilizar cables físicos o cables de fibra para conectar dispositivos, las redes inalámbricas utilizan señales de radio para transmitir datos entre el dispositivo de red y un punto de acceso a la red. El punto de acceso funciona de manera similar al conmutador, en el sentido de que controla cómo se envían los datos a cada dispositivo de red que se comunica con él.

Cada punto de acceso utiliza un Identificador de conjunto de servicios (SSID) único para identificarlo de otros puntos de acceso, que puede ser un nombre o un número. Simplemente le dice a su sistema Linux a qué punto de acceso debe conectarse especificando el valor SSID correcto. La Figura 6.2 muestra un diseño de red inalámbrica común.

![](img/6.2.png)

La desventaja de las redes inalámbricas es que no se puede controlar hacia dónde viajan las señales de radio. Es posible que alguien fuera de su casa intercepte las señales de su punto de acceso e intente conectarse con ellas. Por eso, es importante implementar algún tipo de seguridad de cifrado en su punto de acceso. Sólo los dispositivos que utilicen la clave de cifrado correcta pueden conectarse al punto de acceso inalámbrico. Las técnicas de cifrado inalámbrico comunes son Privacidad equivalente a cables (WEP), Acceso protegido Wi-Fi (WPA) y Acceso protegido Wi-Fi versión 2 (WPA2).
### La capa de red
La capa de red controla cómo se envían los datos entre los dispositivos de red conectados, tanto en su red local como a través de Internet. Para que los datos lleguen al dispositivo de destino correcto, debe haber algún tipo de esquema de direccionamiento de red para identificar cada dispositivo de red de forma única. Para conectar su sistema Linux a una red IP, necesitará cuatro datos:
- Una dirección IP
- Un nombre de host
- Un enrutador predeterminado
- Un valor de máscara de red

Las siguientes secciones explican lo que representa cada uno de estos valores.
### La dirección IP
En una red IP, a cada dispositivo de red se le asigna una dirección única de 32 bits. El software de capa de red incorpora las direcciones IP de origen y destino en el paquete de datos para que los dispositivos de red sepan cómo manejar el paquete de datos y el sistema Linux sepa qué paquetes leer y cuáles ignorar.

Para que a los humanos les resulte más fácil reconocer la dirección, las direcciones IP se dividen en cuatro valores de 8 bits, representados por números decimales, con un punto entre cada valor. Este formato se llama notación decimal con puntos. Por ejemplo, una dirección IP estándar en notación decimal con puntos parece 192.168.1.10.

Las direcciones IP se dividen en dos secciones. Una parte de la dirección IP representa la dirección de red. Todos los dispositivos en la misma red física tienen la misma parte de dirección de red en su dirección IP. Por ejemplo, si a su red doméstica se le asigna la dirección de red 192.168.1.0, todos los dispositivos de red deben comenzar con la dirección IP 192.168.1.

La segunda parte representa la dirección del host. Cada dispositivo en la misma red debe tener una dirección de host única. La Figura 6.3 muestra la asignación de direcciones IP únicas a dispositivos en una red local.

![](img/6.3.png)

Para complicar aún más las cosas, se ha vuelto popular un protocolo de red IP más nuevo llamado Protocolo de Internet versión 6 (IPv6). El esquema de red IPv6 utiliza direcciones de 128 bits en lugar de las direcciones de 32 bits utilizadas por IP, lo que permite identificar de forma única muchos más dispositivos de red en Internet.

El método IPv6 utiliza números hexadecimales para identificar direcciones. La dirección de 128 bits se divide en ocho grupos de cuatro dígitos hexadecimales separados por dos puntos, como este:

```shell-session
fed1:0000:0000:08d3:1319:8a2e:0370:7334
```

Si uno o más grupos de cuatro dígitos son 0000, ese grupo o esos grupos pueden omitirse, dejando dos dos puntos:

```shell-session
fed1::08d3:1319:8a2e:0370:7334
```

Sin embargo, de esta manera sólo se puede comprimir un conjunto de ceros consecutivos. IPv6 también proporciona dos tipos diferentes de direcciones de host:
- Link Local Addresses
- Global Addresses

El software IPv6 en un dispositivo host asigna automáticamente la dirección local del enlace. La dirección local del enlace utiliza una dirección de red predeterminada de `fe80::`; luego deriva la parte del host de la dirección de la dirección de control de acceso a medios (MAC) integrada en la tarjeta de red. Esto garantiza que cualquier dispositivo IPv6 pueda comunicarse automáticamente con cualquier otro dispositivo IPv6 en una red local sin ninguna configuración.

La dirección global IPv6 funciona de manera similar a la versión IP original: a cada red se le asigna una dirección de red única y cada host de la red debe tener una dirección de host única.

### Default Router
Con IP e IPv6, los dispositivos sólo pueden comunicarse directamente con otros dispositivos en la misma red física. Para conectar diferentes redes físicas, se utiliza un enrutador. Un enrutador pasa datos de una red a otra red. Los dispositivos que necesitan enviar paquetes a hosts en redes remotas deben utilizar el enrutador como intermediario. Por lo general, una red contendrá un único enrutador para reenviar paquetes a una red de nivel superior. Esto se denomina enrutador predeterminado (o, a veces, puerta de enlace predeterminada).
Por lo tanto, para que un dispositivo se comunique en una red IP, debe conocer tres datos distintos:
- Su propia dirección de host en la red
- La dirección de red de la red física local
- La dirección de un enrutador local utilizado para enviar paquetes a redes remotas

Ya ha visto cómo especificar direcciones de host utilizando la notación decimal con puntos (como 192.168.1.10). La dirección de red se especifica mediante una dirección de máscara de red, que se trata en la siguiente sección.

### Dirección de máscara de red
La dirección de máscara de red distingue entre las partes de la dirección de red y de host en la dirección IP usando 1 bit para mostrar qué bits de la dirección IP de 32 bits son utilizados por la red y 0 bits para mostrar qué bits representan la dirección de host. Como a la mayoría de las personas no les gusta trabajar con números binarios, la dirección de la máscara de red generalmente se muestra en formato decimal con puntos. Por ejemplo, la dirección de máscara de red 255.255.255.0 indica que los primeros tres números decimales de la dirección IP representan la dirección de red y el último número decimal representa la dirección del host.

Como se mencionó, para conectar su sistema Linux a una red, debe especificar tres valores. Aquí hay un ejemplo de lo que necesitaría:
- Dirección de host: 192.168.20.5
- Dirección de máscara de red: 255.255.255.0
- Puerta de enlace predeterminada: 192.168.20.1

Con estos tres valores en la mano, está casi listo para configurar su sistema Linux para que funcione en Internet. Sólo hay una pieza más del rompecabezas de la que deberá preocuparse y la veremos en la siguiente sección.
### Nombres de host
Con todas estas direcciones IP, puede resultar imposible recordar qué servidores tienen qué direcciones. Afortunadamente para nosotros, existe otro estándar de red que puede ayudarnos. El Sistema de nombres de dominio (DNS) asigna un nombre a los hosts de la red.

Con DNS, a cada dirección de red se le asigna un nombre de dominio (como linux.org) que identifica de manera única la red, y a cada host en esa red se le asigna un nombre de host, que se agrega al nombre de dominio para identificar de manera única al host en la red. .

Por lo tanto, para encontrar el host shadrach en el dominio ejemplo.org, usaría el nombre DNS shadrach.example.org. El sistema DNS utiliza servidores para asignar nombres de dominio y host a las direcciones de red específicas necesarias para comunicarse con ese servidor. Los servidores responsables de definir la red y los nombres de host para una red local interoperan con servidores DNS de nivel superior para resolver nombres de host remotos.

Para usar DNS en sus aplicaciones de red, todo lo que necesita configurar es la dirección del servidor DNS que da servicio a su red local. Desde allí, su servidor DNS local puede encontrar la dirección de cualquier nombre de host en cualquier lugar de Internet.
### Dynamic Host Configuration Protocol
Necesitamos analizar una característica más de la capa de red antes de pasar a configurar el sistema Linux. Intentar realizar un seguimiento de las direcciones de host de todos los dispositivos en una red grande puede resultar engorroso. Mantener las asignaciones de direcciones IP individuales en orden puede ser un desafío y, a menudo, se encontrará con la situación en la que a dos o más dispositivos se les asigna accidentalmente la misma dirección IP.

El Protocolo de configuración dinámica de host (DHCP) se creó para facilitar la configuración de las estaciones de trabajo de los clientes, que no necesariamente necesitan usar la misma dirección IP todo el tiempo. Con DHCP, el cliente se comunica con un servidor DHCP en la red mediante una dirección temporal. Luego, el servidor DHCP le dice al cliente exactamente qué dirección IP, dirección de máscara de red, puerta de enlace predeterminada e incluso servidor DNS usar. Cada vez que el cliente se reinicia, puede recibir una dirección IP diferente, pero eso no importa siempre que sea única en la red.

La mayoría de los enrutadores de redes domésticas incluyen una función de servidor DHCP, por lo que todo lo que necesita hacer es configurar su cliente Linux para que use DHCP y listo. No necesita conocer ninguno de los detalles "entre bastidores" de las direcciones de red.

### La capa de transporte
La _capa de transporte_ a menudo puede ser la parte más confusa de la red. Mientras que la capa de red ayuda a llevar datos a un host específico en la red, la capa de transporte ayuda a llevar los datos a la aplicación correcta contenida en el host. Lo hace mediante el uso de _puertos_.

Los puertos son como números de apartamentos. A cada aplicación que se ejecuta en un servidor de red se le asigna su propio número de puerto, del mismo modo que a cada apartamento del mismo edificio se le asigna un número de apartamento único. Para enviar datos a una aplicación específica en un servidor, el software cliente necesita conocer tanto la dirección IP del servidor (como la dirección del edificio de apartamentos) como el número de puerto de la capa de transporte (como el número de apartamento).

Hay dos protocolos de transporte comunes que se utilizan en el mundo de las redes IP:

- Protocolo de control de transmisión
- Protocolo de datagramas de usuario

El _Protocolo de control de transmisión (TCP)_ envía datos utilizando un método de entrega garantizado. Garantiza que el servidor reciba cada porción de datos que envía la computadora cliente y viceversa. La desventaja de esto es que se requiere una gran cantidad de gastos generales para rastrear y verificar todos los datos enviados, lo que puede disminuir la velocidad de transferencia de datos.

Para los datos que son sensibles a la velocidad de transferencia (como datos en tiempo real como voz y video), esto puede causar retrasos no deseados. La alternativa a esto es el _Protocolo de datagramas de usuario (UDP)_. UDP no se molesta en garantizar la entrega de cada parte de los datos; ¡simplemente envía los datos a la red y espera que lleguen al servidor!

Si bien la pérdida de datos puede parecer algo malo, para algunas aplicaciones (como voz y video) es perfectamente aceptable. Los paquetes de audio o vídeo que faltan simplemente aparecen como interrupciones y cortes en el resultado final de audio o vídeo. Mientras lleguen la mayoría de los paquetes de datos, el audio y el vídeo serán comprensibles.
### La capa de aplicación
La capa de aplicación es donde ocurre toda la acción. Aquí es donde los programas de red procesan los datos enviados a través de la red y luego devuelven un resultado. La mayoría de las aplicaciones de red se comportan utilizando el paradigma cliente/servidor. Con el paradigma cliente/servidor, un dispositivo de red actúa como servidor, ofreciendo algún tipo de servicio a múltiples clientes de la red (como un servidor web que ofrece contenido a través de páginas web). El servidor escucha conexiones entrantes en puertos de capa de transporte específicos asignados a la aplicación. Los clientes deben saber qué puerto de la capa de transporte utilizar para enviar solicitudes a la aplicación del servidor.

Para simplificar ese proceso, tanto TCP como UDP utilizan puertos conocidos para representar aplicaciones comunes. Estos números de puerto están reservados para que los clientes de la red sepan utilizarlos cuando busquen hosts de aplicaciones específicas en la red. La Tabla 6.1 muestra algunos de los puertos de aplicaciones más comunes y conocidos.

| **Port** | **Protocol** | **Application**                         |
| -------- | ------------ | --------------------------------------- |
| 22       | TCP          | Secure Shell Protocol (SSH)             |
| 23       | TCP          | Telnet (interactive command lines)      |
| 25       | TCP          | SMTP (Simple Mail Transport Protocol)   |
| 53       | UDP          | DNS (Dynamic Name System)               |
| 80       | TCP          | HTTP (Hypertext Transport Protocol)     |
| 143      | TCP          | IMAP (Internet Message Access Protocol) |
| 443      | TCP          | HTTPS (Secure HTTP)                     |

Ahora que ha visto los conceptos básicos de cómo Linux utiliza las redes para transferir datos entre sistemas, la siguiente sección profundiza en los detalles sobre cómo configurar estas funciones en su sistema Linux.
### Configuración de funciones de red
Como vio en la sección anterior, necesitará configurar cinco piezas principales de información en su sistema Linux para interactuar en una red:
- La dirección del host
- La dirección de red
- El enrutador predeterminado (a veces llamado puerta de enlace)
- El nombre de host del sistema
- Una dirección de servidor DNS para resolver nombres de host

Hay tres formas diferentes de configurar esta información en sistemas Linux:
- Edición manual de archivos de configuración de red
- Utilizar una herramienta gráfica
- Uso de herramientas de línea de comandos

Las siguientes secciones lo guiarán a través de cada uno de estos métodos.
### Archivos de configuración de red
Cada distribución de Linux utiliza archivos de configuración de red para definir las configuraciones de red necesarias para comunicarse en la red. Desafortunadamente, sin embargo, no existe un único archivo de configuración estándar que utilicen todas las distribuciones. En cambio, diferentes distribuciones utilizan diferentes archivos de configuración para definir la configuración de red.

| **Distribution** | **Network Configuration Location**       |
| ---------------- | ---------------------------------------- |
| Debian-based     | /etc/network/interfaces file             |
| Red Hat–based    | /etc/sysconfig/network-scripts directory |
| OpenSUSE         | /etc/sysconfig/network file              |

Si bien cada una de las distribuciones de Linux utiliza un método diferente para definir la configuración de red, todas tienen características similares. La mayoría de los archivos de configuración definen cada una de las configuraciones de red requeridas como valores separados en el archivo de configuración. Ejemplo de un sistema Linux basado en Debian.

```shell-session
auto eth0
iface eth0 inet static    
	address 192.168.1.77    
	netmask 255.255.255.0    
	gateway 192.168.1.254

iface eth0 inet6 static    
address 2003:aef0::23d1::0a10:00a1
   netmask 64
   gateway 2003:aef0::23d1::0a10:0001
```

El ejemplo asigna una dirección IP y una dirección IPv6 a la interfaz de red cableada designada como eth0.

Ejemplo de configuración de DHCP de red Debian `auto eth0 iface eth0`

```shell-session
inet dhcp iface eth0 inet6 dhcp
```

Si solo desea asignar una dirección local de enlace IPv6 y no recuperar una dirección IPv6 de un servidor DHCP, reemplace la línea inet6 con esto:

```shell-session
iface eth0 inet6 auto
```

El atributo auto le dice a Linux que asigne la dirección local del enlace, lo que permite que el sistema Linux se comunique con cualquier otro dispositivo IPv6 en la red local pero no con una dirección global.

Para los sistemas basados ​​en Red Hat, deberá configurar la configuración de red en dos archivos separados. El primer archivo define las direcciones de red y máscara de red en un archivo que lleva el nombre del nombre de la interfaz de red (como `ifcfg-eth0`). Ejemplo de un sistema CentOS Linux.

```shell-session
DEVICE="eth0"
NM_CONTROLLED="no"
ONBOOT=yes
TYPE=Ethernet
BOOTPROTO=static
NAME="System eth0"
IPADDR=192.168.1.77
NETMASK=255.255.255.0
IPV6INIT=yes
IPV6ADDR=2003:aef0::23d1::0a10:00a1/64
```

El segundo archivo requerido en los sistemas basados ​​en Red Hat es el archivo de red, que define el nombre de host y la puerta de enlace predeterminada.

Ejemplos de configuración de archivos de red CentOS

```shell-session
NETWORKING=yes
HOSTNAME=mysystem
GATEWAY=192.168.1.254
IPV6FORWARDING=yes
IPV6_AUTOCONF=no
IPV6_AUTOTUNNEL=no
IPV6_DEFAULTGW=2003:aef0::23d1::0a10:0001
IPV6_DEFAULTDEV=eth0
```

Observe que el archivo de configuración de red de Red Hat también define el nombre de host asignado al sistema Linux. Para otros tipos de sistemas Linux, almacenar el nombre de host en el archivo `/etc/hostname` se ha convertido en una especie de estándar de facto. Sin embargo, algunas distribuciones de Linux utilizan `/etc/HOSTNAME` en su lugar.

También deberá definir un servidor DNS para que el sistema pueda usar nombres de host DNS. Afortunadamente, todos los sistemas Linux siguen este estándar y se maneja en el archivo de configuración `/etc/resolv.conf`:

```shell-session
domain mydomain.com 
search mytest.com 
nameserver 192.168.1.1
```

La entrada de dominio define el nombre de dominio asignado a la red. De forma predeterminada, el sistema agregará este nombre de dominio a cualquier nombre de host que especifique. La entrada de búsqueda define cualquier dominio adicional utilizado para buscar nombres de host. La entrada del servidor de nombres es donde especifica el servidor DNS asignado a su red. Algunas redes pueden tener más de un servidor DNS; simplemente agregue varias entradas de servidor de nombres en el archivo.
### Herramientas gráficas
La herramienta Network Manager es un programa popular utilizado por muchas distribuciones de Linux para proporcionar una interfaz gráfica para definir conexiones de red. Network Manager se inicia automáticamente en el momento del arranque y aparece en el área de la bandeja del sistema del escritorio como un icono.

Si su sistema detecta una conexión de red por cable, el icono aparece como dos flechas que apuntan en direcciones opuestas. Si su sistema detecta una conexión de red inalámbrica, el icono aparece como una señal de radio vacía. Cuando hace clic en el icono, verá una lista de las redes inalámbricas disponibles detectadas por la tarjeta de red, como se muestra en la Figura 6.4.

![](img/6.4.png)

Haga clic en su punto de acceso para seleccionarlo de la lista. Si su punto de acceso está cifrado, se le pedirá que ingrese la contraseña para acceder a la red.
Una vez que su sistema esté conectado a un punto de acceso inalámbrico, el ícono aparece como una señal de radio. Haga clic en el icono y luego seleccione Editar conexiones para editar la configuración de conexión de red para el sistema, como se muestra en la Figura 6.5.

![](img/6.5.png)

