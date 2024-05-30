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

```
fed1:0000:0000:08d3:1319:8a2e:0370:7334
```

Si uno o más grupos de cuatro dígitos son 0000, ese grupo o esos grupos pueden omitirse, dejando dos dos puntos:

```
fed1::08d3:1319:8a2e:0370:7334
```

Sin embargo, de esta manera sólo se puede comprimir un conjunto de ceros consecutivos. IPv6 también proporciona dos tipos diferentes de direcciones de host:
- Link Local Addresses
- Global Addresses

El software IPv6 en un dispositivo host asigna automáticamente la dirección local del enlace. La dirección local del enlace utiliza una dirección de red predeterminada de `fe80::`; luego deriva la parte del host de la dirección de la dirección de control de acceso a medios (MAC) integrada en la tarjeta de red. Esto garantiza que cualquier dispositivo IPv6 pueda comunicarse automáticamente con cualquier otro dispositivo IPv6 en una red local sin ninguna configuración.

La dirección global IPv6 funciona de manera similar a la versión IP original: a cada red se le asigna una dirección de red única y cada host de la red debe tener una dirección de host única.

