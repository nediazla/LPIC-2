# Mantenimiento de sistema

Mantener un sistema Linux en funcionamiento implica muchas tareas de mantenimiento básicas importantes, como la copia de seguridad de los datos y la planificación de la capacidad. En este grupo de tareas se incluye la instalación de software y el mantenimiento de información a la comunidad de usuarios del sistema.
Este capítulo comienza explorando los medios y métodos para notificar a los usuarios sobre problemas actuales del sistema. A continuación, cubre temas de respaldo, enfocándose en las diversas herramientas estándar disponibles para realizar esta tarea. Luego se aborda la compilación e instalación de una aplicación a partir del código fuente, seguido del trabajo, a veces complicado, de planificación de la capacidad y resolución de problemas del uso de recursos.
### Mantener informados a los usuarios
Una comunicación adecuada con los usuarios del sistema, ya sean administradores de sistemas, programadores, clientes, etc., puede ser de gran ayuda para establecer buenas relaciones. Con suerte, su empresa ha establecido políticas estándar para mantener informados a los usuarios del sistema. Si es así, puede utilizar esas políticas para guiar sus métodos de comunicación manuales y automatizados con el usuario final.
Además de los viejos recursos del correo electrónico, la mensajería de texto automatizada y las páginas web de la intranet de la empresa, un sistema Linux ofrece las siguientes utilidades y archivos adicionales para ayudar con la comunicación:
-  `/etc/issue`
- `/etc/issue.net`
- `/etc/motd`
- `/sbin/shutdown`
- `/bin/usr/notify-send (/usr/bin/notify-send)`
- `/bin/wall (/usr/bin/wall)`
### Mirando la mensajería fluida
La mensajería fluida implica informar a los usuarios activos del sistema sobre eventos actuales, como el apagado del sistema, a medida que ocurren. Estos métodos están destinados a utilizarse con fines de emergencia o como comunicación complementaria para una situación planificada.
### Usando el comando `wall`
El comando `/usr/bin/wall` envía mensajes simples a ciertos usuarios del sistema. Sólo los usuarios que cumplan las siguientes condiciones recibirán estos mensajes:
- Usuarios que actualmente están conectados a una terminal (tty#) o un emulador de terminal (pts/#)
- Usuarios que tienen su estado de mensaje establecido en "sí"
El comando `/bin/mesg` o `/usr/bin/mesg` le permite ver y configurar el estado de su mensaje. El comando `mesg` se demuestra aquí:

```
$ mesg 
is n
$
$ mesg y
$
$ mesg
is y
$
$ mesg n
$
$ mesg*
is n 
$
```

Observe en el ejemplo anterior que el comando `mesg` usado por sí solo simplemente muestra el estado actual del mensaje. Al ejecutar el comando `mesg` y se activa la mensajería y al emitir `mesg n` se desactiva.
La sintaxis general del comando de escritura se muestra aquí:

```
write username terminal_id
```

En la Figura 2.1 y la Figura 2.2 se muestra un ejemplo del comando de escritura en uso.

![](img/2.1.png)

Observe en la Figura 2.1 que el comando `who -T` se usa primero. Este comando muestra el estado actual del acceso de escritura de cada usuario que ha iniciado sesión. Un signo más (+) entre el nombre de usuario y la identificación del terminal indica que se concede acceso de escritura, mientras que un signo menos (-) indica que no se ha concedido acceso de escritura. Un signo de interrogación (?) indica un usuario que ha iniciado sesión en la GUI. Para que un usuario de GUI reciba un mensaje de comando de escritura, se debe abrir un emulador de terminal GUI, designado por un tipo de terminal pts/#, y se debe otorgar acceso de escritura. La identificación del terminal pts/0 en la Figura 2.1 indica que el usuario rico tiene una aplicación de emulador de terminal ejecutándose en su GUI. Sin embargo, el terminal aún debe tener acceso de escritura otorgado (+) para poder recibir mensajes de comando de escritura, lo cual hace.

En la Figura 2.1, después de utilizar el comando `who -T`, se emplea el comando de escritura. Para utilizar el comando de escritura, se deben incluir dos opciones: el nombre de usuario del usuario, quién recibirá el mensaje y la identificación del terminal de ese usuario. En la Figura 2.1, el nombre de usuario del usuario es chris y la identificación del terminal es tty2. Una vez que se emite el comando de escritura, espera su mensaje a través de la entrada estándar. Sin embargo, no hay ningún mensaje que indique esto. Simplemente escriba su mensaje y presione Ctrl+D cuando haya terminado. El mensaje se envía automáticamente y se muestra en el terminal del usuario receptor, como se muestra en la Figura 2.2.

![](img/2.2.png)

Puede utilizar la utilidad `/bin/wall` o `/usr/bin/wall` para transmitir un mensaje a todos los terminales con acceso de escritura otorgado. Por lo tanto, puede ser una utilidad útil para la comunicación estándar.

La sintaxis general del comando de muro es mensaje de muro.
La Figura 2.3 y la Figura 2.4 muestran el comando de pared en acción. Observe en la Figura 2.3 que el mensaje se escribe después de que se emite el comando de pared. El comando de pared es similar al comando de escritura en el sentido de que puede aceptar el mensaje mediante entrada estándar. En la Figura 2.3, se escribe el mensaje y se presiona Ctrl+D para enviarlo.

![](img/2.3.png)

El mensaje del muro es disruptivo porque se mostrará en medio de lo que sea que el usuario esté haciendo actualmente en la terminal, como se muestra en la Figura 2.4. Sin embargo, el usuario que recibe el mensaje puede simplemente presionar Enter para recibir el mensaje $. figura 2.4 Salida de comando de pared receptora

![](img/2.4.png)

### Usando el comando notificar-enviar
El comando `wall` es útil, pero si un usuario no ha iniciado sesión en una terminal de consola o no tiene un emulador de terminal GUI abierto, no podrá enviar mensajes a ese usuario. La utilidad `/bin/notify-send` o `/usr/bin/notify-send` puede remediar esta situación y es una buena herramienta para usar junto con el comando `wall`.
Puede probar el comando `notify-send`r enviándose mensajes a sí mismo en la GUI.
La sintaxis general de notificación y envío se ve así:

```
notify-send "Title" "Message"
```

La Figura 2.5 muestra el comando `notify-send` en acción en una distribución CentOS. El comando se emite dentro de un emulador de terminal GUI. Observe que el mensaje se muestra en la parte inferior del escritorio. Diferentes entornos de escritorio Linux mostrarán estos mensajes de notificación en diferentes ubicaciones de visualización del escritorio.

![](img/2.5.png)

Para enviar mensajes de notificación y envío a usuarios de GUI además de usted, necesita privilegios de super usuario. Además, necesita ciertas variables de entorno, dependiendo de cómo implemente la utilidad de notificación y envío y qué distribución esté utilizando.
En la Figura 2.6, el envío de notificación lo emplea un usuario con privilegios de super usuario que ha iniciado sesión en una terminal de consola virtual de distribución de Ubuntu. Tenga en cuenta que se necesita la variable de entorno DISPLAY

![](img/2.6.png)

La variable de entorno DISPLAY en la Figura 2.6 se establece en el valor de la columna tty del comando w para el usuario kevin. Esto es necesario para que la utilidad `notify-send` sepa dónde enviar su salida. Observe que también se utiliza el comando `sudo`. Es necesario para que el comando `su -c` pueda usarse para emitir el comando `notify-send` cuando el usuario inicia sesión en la GUI; En este caso, ese es Kevin. Las barras invertidas (\) delante de las comillas (") que rodean tanto el título como el mensaje del comando `notify-send` también son necesarias. Porque el comando, enviado como una opción con `su -c`, debe estar entre comillas , las barras invertidas permiten que las opciones de notificación y envío tengan las comillas dobles necesarias (") y no interfieran con la operación del comando `su -c`. El último parámetro del comando largo de la Figura 2.6 es el nombre de usuario kevin. Esta es una opción para el comando `su -c`, de modo que el usuario kevin ejecutará el comando `notify-send`. Los resultados de todo este trabajo se muestran en la Figura 2.7.

![](img/2.7.png)

La Figura 2.7 muestra el mensaje de prueba enviado. En esta distribución de Ubuntu, el mensaje de notificación y envío recibido se muestra cerca del área superior izquierda del escritorio de Unity.
En otras distribuciones, como CentOS, al enviar mensajes a otros usuarios de GUI, se necesitan aún más variables de entorno. En la Figura 2.8, observe que antes de usar el comando `notify-send`, la variable de entorno `DBUS_SESSION_BUS_ADDRESS` debe configurarse en la configuración actual del usuario de la GUI para esa variable y luego exportarse. Esta variable de entorno suele ser necesaria cuando se crea un trabajo cron para automatizar dicha comunicación.

![](img/2.8.png)

La Figura 2.8 utiliza los comandos grep y sed para extraer la configuración de la variable de entorno `DBUS_SESSION_BUS_ADDRESS` actual necesaria del archivo `/proc/proc_ID/environ`. `proc_ID` es el ID del proceso para el proceso gnome-Shell del usuario.
El comando `notify-send` tiene varias opciones adicionales que pueden resultar útiles. Desafortunadamente, en algunas distribuciones, las páginas de manual para esta utilidad en particular no existen o, en el mejor de los casos, son escasas. Si necesita más información, utilice su motor de búsqueda favorito para buscar documentación adicional de `notify-send`.