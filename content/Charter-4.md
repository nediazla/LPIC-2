![](img/sudo.png)
# Administrar el Sistema de Archivos

Los datos se guardan como unos y ceros en los medios de almacenamiento, como unidades de disco y DVD. Un sistema de archivos cierra la brecha entre los unos y los ceros almacenados en los medios y los archivos con los que trabaja.

La gestión de un sistema de archivos incluye proporcionar acceso a los datos almacenados, así como ajustar, monitorear y reparar los sistemas de archivos para mejorar los tiempos de acceso y proteger los datos. Este capítulo cubre todos estos temas para que pueda administrar adecuadamente sus sistemas de archivos Linux.
### Operando el sistema de archivos Linux
Para administrar y controlar un sistema de archivos Linux, necesita saber más que una definición general del sistema de archivos. Debe conocer las estructuras básicas del sistema de archivos. También es importante comprender los distintos tipos de sistemas de archivos que determinan cómo se manejan los archivos en los medios de almacenamiento. Comprender estos tipos de sistemas de archivos y sus esquemas le ayudará a elegir el tipo de sistema de archivos adecuado para sus necesidades de datos.

Además de comprender los tipos de sistemas de archivos, debe saber cómo adjuntar un sistema de archivos a la estructura de directorios de Linux. Los sistemas de archivos se pueden adjuntar temporal o persistentemente a la estructura del directorio. 
### Comprender las estructuras del sistema de archivos
Las unidades de disco duro y otros medios de almacenamiento normalmente vienen con el formato de bajo nivel aplicado por el fabricante. Sin embargo, para muchos dispositivos de medios de almacenamiento no ópticos, como los discos, aún se requieren particiones y formateo de alto nivel.
La partición de los medios de almacenamiento, que se aborda en la certificación LPIC-1, es necesaria antes del formateo de alto nivel. Normalmente, la partición consiste en dividir lógicamente un dispositivo de medios de almacenamiento en secciones individuales llamadas particiones. Sin embargo, tenga en cuenta que una única partición puede abarcar un dispositivo completo, así como varios dispositivos. 

El formateo de alto nivel a menudo se denomina simplemente formatear o crear el sistema de archivos. Este formateo se logra mediante utilidades como `mkfs` y se abordó en la certificación LPIC-1.

Cuando se formatea una partición o un volumen, se colocan varias estructuras, según el tipo de sistema de archivos seleccionado. Un área de partición contiene los datos del archivo real. Las otras áreas contienen estructuras que contienen elementos como metadatos del sistema de archivos, metadatos de archivos, archivos de diario, etc.

Los metadatos del archivo se almacenan en una tabla de inodo. Cuando se crea un archivo en la partición o volumen, se crea una nueva entrada en la tabla de inodos. La tabla de inodos es una tabla de números índice, llamados inodos. Normalmente, un inodo es un número asignado de forma exclusiva a un archivo cuando se crea. (Hay excepciones a esto, como cuando se crea un vínculo físico a un archivo. El archivo de vínculo físico y el archivo original comparten un número de inodo). El inodo y los metadatos de su archivo asignado, como permisos, propiedad y punteros a Las distintas ubicaciones de datos de archivos se almacenan en la tabla de inodos.

Cada partición o volumen puede tener un tipo de sistema de archivos diferente. Esto permite una gran flexibilidad para abordar sus necesidades de datos particulares.
### Comprender los tipos de sistemas de archivos
Un sistema de archivos determina cómo se manejan los archivos en los medios físicos. Cada tipo tiene sus propios métodos únicos para acceder, actualizar y proteger la integridad de los datos. Por lo tanto, la elección del tipo de sistema de archivos es una selección importante.

Los sistemas de archivos se pueden clasificar de muchas maneras diferentes, por ejemplo, según cómo protegen la integridad de los datos, el medio físico en el que se pueden utilizar, su sistema operativo de destino original, etc. Para nuestros propósitos aquí, se dividen en sistemas de archivos nativos de Linux y sistemas de archivos no nativos.
### Mirando los sistemas de archivos nativos de Linux
Un sistema de archivos nativo de Linux es aquel que fue diseñado originalmente para usarse en Linux.

```
      btrfs   es un moderno Sistema de archivos para Linux Copy-on-Write (CoW)
              enfocado en implementar características avanzadas al mismo tiempo
              que se centra en la tolerancia a los errores, reparación y fácil
              administración.
	  
	  erofs  is the Enhanced Read-Only File System, stable since Linux
              5.4.
       ext    is an elaborate extension of the minix filesystem.  It has
              been completely superseded by the second version of the
              extended filesystem (ext2) and has been removed from the
              kernel (in Linux 2.1.21).

       ext2   is a disk filesystem that was used by Linux for fixed
              disks as well as removable media.  The second extended
              filesystem was designed as an extension of the extended
              filesystem (ext).
              
       ext3   is a journaling version of the ext2 filesystem.  It is
              easy to switch back and forth between ext2 and ext3.  

       ext4   is a set of upgrades to ext3 including substantial
              performance and reliability enhancements, plus large
              increases in volume, file, and directory size limits.  

       hpfs   is the High Performance Filesystem, used in OS/2.  This
              filesystem is read-only under Linux due to the lack of
              available documentation.

       iso9660

              is a CD-ROM filesystem type conforming to the ISO 9660
              standard.

              High Sierra
                     Linux supports High Sierra, the precursor to the
                     ISO 9660 standard for CD-ROM filesystems.  It is
                     automatically recognized within the iso9660
                     filesystem support under Linux.

              Rock Ridge
                     Linux also supports the System Use Sharing Protocol
                     records specified by the Rock Ridge Interchange
                     Protocol.  They are used to further describe the
                     files in the iso9660 filesystem to a UNIX host, and
                     provide information such as long filenames,
                     UID/GID, POSIX permissions, and devices.  It is
                     automatically recognized within the iso9660
                     filesystem support under Linux.

       JFS    is a journaling filesystem, developed by IBM, that was
              integrated into Linux 2.4.24.

       minix  is the filesystem used in the Minix operating system, the
              first to run under Linux.  It has a number of
              shortcomings, including a 64 MB partition size limit,
              short filenames, and a single timestamp.  It remains
              useful for floppies and RAM disks.

       msdos  is the filesystem used by DOS, Windows, and some OS/2
              computers.  msdos filenames can be no longer than 8
              characters, followed by an optional period and 3 character
              extension.

       ncpfs  is a network filesystem that supports the NCP protocol,
              used by Novell NetWare.  It was removed from the kernel in
              Linux 4.17.

       nfs    is the network filesystem used to access disks located on
              remote computers.

       ntfs   is the filesystem native to Microsoft Windows NT,
              supporting features like ACLs, journaling, encryption, and
              so on.

       proc   is a pseudo filesystem which is used as an interface to
              kernel data structures rather than reading and
              interpreting _/dev/kmem_.  In particular, its files do not
              take disk space.  

       Reiserfs
              is a journaling filesystem, designed by Hans Reiser, that
              was integrated into Linux 2.4.1.

       smb    is a network filesystem that supports the SMB protocol,
              used by Windows.  

       sysv   is an implementation of the System V/Coherent filesystem
              for Linux.  It implements all of Xenix FS, System V/386
              FS, and Coherent FS.

       umsdos is an extended DOS filesystem used by Linux.  It adds
              capability for long filenames, UID/GID, POSIX permissions,
              DOS filesystem, without sacrificing compatibility with
              DOS.

       tmpfs  is a filesystem whose contents reside in virtual memory.
              Since the files on such filesystems typically reside in
              RAM, file access is extremely fast.  

       vfat   is an extended FAT filesystem used by Microsoft Windows95
              and Windows NT.  vfat adds the capability to use long
              filenames under the MSDOS filesystem.

       XFS    is a journaling filesystem, developed by SGI, that was
              integrated into Linux 2.4.20.

       xiafs  was designed and implemented to be a stable, safe
              filesystem by extending the Minix filesystem code.  It
              provides the basic most requested features without undue
              complexity.  The xiafs filesystem is no longer actively
              developed or maintained.  It was removed from the kernel
              in Linux 2.1.21.
```

Notarás que la mayoría de los sistemas de archivos modernos usan el registro en diario, mientras que `Btrfs` usa COW en su lugar. La diferencia entre estas dos características de integridad de datos es la siguiente. El registro en diario es un método que rastrea los cambios de datos no confirmados (metadatos de archivos aún no actualizados) en un archivo de registro, llamado diario. Si el proceso de confirmación de datos se interrumpe, por ejemplo, por una falla del sistema, el diario se utiliza para confirmar los cambios de datos previstos. Este método proporciona una protección de datos eficaz en caso de interrupción del sistema.

COW significa Copiar en escritura y es otro método utilizado para proteger los datos. Para comprenderlo, primero debe comprender cómo se manejan los archivos en sistemas de archivos que no son COW. Cuando se crea un archivo, se escribe en el espacio libre del medio de almacenamiento y los metadatos se crean apuntando a la ubicación de los datos del archivo. En un sistema de archivos que no es COW, cuando se modifican los datos de ese archivo, los datos antiguos se sobrescriben con los datos nuevos.

En un sistema de archivos COW, la creación de archivos se maneja de manera similar. Sin embargo, la modificación de datos de archivos se maneja de manera diferente. Para un sistema de archivos COW, cuando se modifican los datos de un archivo, los nuevos datos se escriben en el espacio libre del medio de almacenamiento; Los metadatos del archivo se actualizan para apuntar a los nuevos datos. Por lo tanto, si el proceso de compromiso de datos se interrumpe, digamos por una falla del sistema, los datos originales aún existen y no se pierden.
### Mirando sistemas de archivos Linux no nativos
Hay sistemas de archivos adicionales a considerar además de los sistemas de archivos nativos de Linux. Estos son sistemas de archivos no nativos, que no se crearon originalmente para Linux pero que pueden ser manejados por Linux.

| Name | MAx File Size | Max Filesysten Size | Journaling | Description/Features                                                                                                                                                        |
| ---- | ------------- | ------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ntfs | 2TB           | 256TB               | Yes        | Read access is supported on Linux, but software to do so may not be installed by default. For write access, additional software may also be needed. Developed by Microsoft. |
| vfat | 4GB           | 2TB                 | No         | Typically used on USB flash drives. Developed by Microsoft.                                                                                                                 |
| XFS  | 8EB           | 8EB                 | Yes        | High-performance filesystem that supports large file and filesystem sizes. Developed by Silicon Graphics.                                                                   |
| ZFS  | 16EB          | 256ZB               | COW        | ZFS on Linux (ZoL) is a high-performance filesystem often compared to Btrfs. Developed by Sun Microsystems (now part of Oracle).                                            |

Como puede ver, puede elegir entre una amplia variedad de sistemas de archivos para usar en su sistema Linux. 

Un sistema de archivos no nativo relativamente nuevo creado para sistemas Windows es ReFS (Resilient File System). Actualmente tiene una implementación limitada, pero es posible que sea compatible con Linux en el futuro.
### Hacer un sistema de archivos
Una vez que haya creado una partición o volumen y haya elegido un sistema de archivos para él, estará listo para formatear (crear) un sistema de archivos. Como se mencionó anteriormente, esto configura varias estructuras en la partición (volumen) para una gestión adecuada de los datos.

La herramienta principal para formatear un sistema de archivos es `mkfs` y necesita privilegios de super usuario para utilizarla. La utilidad `mkfs` es en realidad una interfaz para varias otras utilidades utilizadas para cada tipo de sistema de archivos.

El tipo de sistema de archivos deseado se puede elegir mediante el comando `mkfs.fstype` o `mkfs -t fstype`. El `fstype` es un código especial que representa el tipo de sistema de archivos que se selecciona. Por ejemplo, ext4 es el código de tipo para seleccionar un tipo de sistema de archivos ext4 (`ext4fs`).

El siguiente es un ejemplo del uso de la utilidad `mkfs` para formatear una partición al tipo de sistema de archivos ext4. Se completó en una distribución de Ubuntu. Por lo tanto, `sudo` se utiliza para obtener los privilegios de super usuario necesarios.

```sh
sudo mkfs.ext4 /dev/sdb1
[sudo] password for christine: mke2fs 1.42.9 (4-Feb-2014)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
131072 inodes, 524288 blocks
26214 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=536870912
16 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group 
Superblock backups stored on blocks:
     32768, 98304, 163840, 229376, 294912
Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information:  0/1done
```

Observe en el resultado del ejemplo anterior que se configuraron varias estructuras mientras se procesaba el formateo de la partición `/dev/sdb1`. Estas estructuras incluyen inodos, tablas de inodos y un diario. Recuerde que anteriormente en este capítulo cada tipo de sistema de archivos tendrá estructuras comunes y únicas creadas durante el formateo para administrar el sistema de archivos. Cada tipo de sistema de archivos tiene sus propios métodos únicos para acceder, actualizar y proteger la integridad de los datos.

Puede verificar el tipo de sistema de archivos creado usando la utilidad separada y los privilegios de super usuario, como se muestra en este ejemplo recortado en un sistema Ubuntu:

```sh
sudo parted -l
[...]
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 4295MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Number  Start   End     Size    Type     File system  Flags  
1      1049kB  2149MB  2147MB  primary  ext4
```

El sistema de archivos en `/dev/sdb1` es de hecho un sistema de archivos ext4. Esta es una manera práctica de verificar el formato `mkfs`.
También puedes usar la utilidad `blkid` para verificar el tipo de sistema de archivos, como se muestra en este ejemplo recortado de un sistema Ubuntu:

```sh
sudo blkid
/dev/sda1: [...] TYPE="ext4"
/dev/sda5: [...] TYPE="swap"
/dev/sdb1: [...] TYPE="ext4"
```

Este resultado también muestra que el sistema de archivos en `/dev/sdb1` es un sistema de archivos ext4. Ni la utilidad `blkid` ni la `parted` requieren que la partición esté adjunta al sistema de directorio de Linux para mostrar su tipo de sistema de archivos.
### Adjuntar un sistema de archivos
Una vez que haya creado su sistema de archivos, es importante saber cómo adjuntar el sistema de archivos a la estructura de directorios de Linux. Linux utiliza un método para almacenar archivos dentro de una única estructura de directorio llamada directorio virtual. En la base de este directorio virtual se encuentra el directorio raíz (`/`), y los directorios y archivos debajo del directorio raíz se enumeran según la ruta del directorio. Puede adjuntar sistemas de archivos a la estructura del directorio virtual de forma temporal o persistente, según sus necesidades actuales. Después de haber adjuntado un sistema de archivos a la estructura del directorio virtual, puede almacenar y acceder a datos en ese sistema de archivos.
### Adjuntar un sistema de archivos temporalmente
Adjuntar un sistema de archivos al directorio virtual de Linux se llama montaje y el montaje temporal se realiza mediante el comando mount. Para montar un sistema de archivos, debe tener privilegios de super usuario (aunque hay excepciones, como leerá más adelante). El comando básico para montar un sistema de archivos es `mount -t fstype dispositivo punto_montaje`

El `fstype` es el tipo de sistema de archivos que está montando. Aquí se utilizan los mismos códigos `fstype` utilizados en el comando `mkfs`, como `xfs`. El `fstype` debe ser compatible con el kernel de Linux de su distribución para poder montarse.

El dispositivo es un nombre de ruta absoluta a la partición o volumen que contiene este sistema de archivos, como `/dev/sdb1`. 
El punto de montaje en el comando de montaje es la ubicación dentro del directorio virtual donde residirá el sistema de archivos, como `/home/christine/Temp`. El siguiente ejemplo demuestra cómo montar un sistema de archivos en una distribución de Ubuntu:

```sh
mkdir /home/christine/Temp

sudo mount -t ext4 /dev/sdb1 /home/christine/Temp 
[sudo] password for christine:

ls -F /home/christine/Temp 
lost+found/
```

Una vez montado el sistema de archivos, puede almacenar, modificar y acceder a datos utilizando el punto de montaje como referencia. A continuación se muestra un ejemplo utilizando el sistema de archivos previamente montado:

```sh
touch /home/christine/Temp/a_file.txt

ls -F /home/christine/Temp a_file.txt  
lost+found/
```

Observe que cuando se montó el sistema de archivos, ya existía un directorio `lost+found` en el directorio `mount_point`. El directorio `lost+found` se utiliza para recuperar archivos en los sistemas de archivos ext2, ext3 y ext4. Si un archivo que reside en este sistema de archivos no se cierra correctamente, como cuando se produce un fallo del sistema o se encuentra un error de software, se almacena en este directorio. Además, el comando `fsck`, almacena los archivos recuperados en el directorio `lost+found`. Tenga en cuenta que es posible que un archivo ubicado aquí no esté completamente intacto, según el problema que encuentre.

El comando `mount`, cuando se usa sin opciones ni parámetros, extrae los datos que muestra directamente del archivo `/etc/mtab`. El archivo `/etc/mtab` contiene una lista de todos los sistemas de archivos actualmente montados. Por lo tanto, puede verificar fácilmente que su sistema de archivos se montó correctamente en la ubicación deseada usando el comando `mount`. A continuación se muestra un ejemplo con el resultado recortado que se muestra en la distribución de Ubuntu utilizada anteriormente:

```sh
mount 
/dev/sda1 on / type ext4 (rw,errors=remount-ro)
[...]
/dev/sdb1 on /home/christine/Temp type ext4 (rw)
```

El resultado del ejemplo muestra que la partición `/dev/sdb1` está montada en el punto de montaje `/home/christine/Temp`. También muestra que el tipo de sistema de archivos es ext4.

El comando `mount` tiene varias opciones útiles.

```
Command line options available for the mount command:

-V, --version
Output version.

-h, --help
Print a help message.

-v, --verbose
Verbose mode.

-a, --all
Mount all filesystems (of the given types) mentioned in _fstab_.

-F, --fork
(Usado junto con -a.) Bifurque una nueva encarnación de montaje para cada dispositivo. Esto hará los montajes en diferentes dispositivos o diferentes servidores NFS en paralelo. Esto tiene la ventaja de que es más rápido; También los tiempos de espera de NFS van en paralelo. Una desventaja es que las monturas se realizan en orden indefinido. Por lo tanto, no puede usar esta opción si desea montar tanto _/usr_ como _/usr/spool_.

-f, --fake
Causes everything to be done except for the actual system call; if it's not obvious, this ''fakes'' mounting the filesystem. This option is useful in conjunction with the -v flag to determine what the mount command is trying to do. It can also be used to add entries for devices that were mounted earlier with the -n option. The -f option checks for existing record in /etc/mtab and fails when the record already exists (with regular non-fake mount, this check is done by kernel).

-i, --internal-only
Don't call the /sbin/mount.<filesystem> helper even if it exists.

-l
Add the labels in the mount output. Mount must have permission to read the disk device (e.g. be suid root) for this to work. One can set such a label for ext2, ext3 or ext4 using the [e2label](https://linux.die.net/man/8/e2label)(8) utility, or for XFS using [xfs_admin](https://linux.die.net/man/8/xfs_admin)(8), or for reiserfs using reiserfstune(8).

-n, --no-mtab
Mount without writing in _/etc/mtab_. This is necessary for example when _/etc_ is on a read-only filesystem.

--no-canonicalize
Don't canonicalize paths. The mount command canonicalizes all paths (from command line or fstab) and stores canonicalized paths to the _/etc/mtab_ file. This option can be used together with the -f flag for already canonicalized absolut paths.

-p, --pass-fd _num_
In case of a loop mount with encryption, read the passphrase from file descriptor _num_ instead of from the terminal.

-s
Tolerate sloppy mount options rather than failing. This will ignore mount options not supported by a filesystem type. Not all filesystems support this option. This option exists for support of the Linux autofs-based automounter.

-r, --read-only
Mount the filesystem read-only. A synonym is -o ro.

Note that, depending on the filesystem type, state and kernel behavior, the system may still write to the device. For example, Ext3 or ext4 will replay its journal if the filesystem is dirty. To prevent this kind of write access, you may want to mount ext3 or ext4 filesystem with "ro,noload" mount options or set the block device to read-only mode, see command [blockdev](https://linux.die.net/man/8/blockdev)(8).

-w, --rw
Mount the filesystem read/write. This is the default. A synonym is -o rw.

-L _label_
Mount the partition that has the specified _label_.

-U _uuid_
Mount the partition that has the specified _uuid_. These two options require the file _/proc/partitions_ (present since Linux 2.1.116) to exist.

-t, --types _vfstype_
The argument following the -t is used to indicate the filesystem type. The filesystem types which are currently supported include: _adfs_, _affs_, _autofs_, _cifs_, _coda_, _coherent_, _cramfs_, _debugfs_, _devpts_, _efs_, _ext_, _ext2_, _ext3_, _ext4_, _hfs_, _hfsplus_, _hpfs_, _iso9660_, _jfs_, _minix_, _msdos_, _ncpfs_, _nfs_, _nfs4_, _ntfs_, _proc_, _qnx4_, _ramfs_, _reiserfs_, _romfs_, _squashfs_, _smbfs_, _sysv_, _tmpfs_, _ubifs_, _udf_, _ufs_, _umsdos_, _usbfs_, _vfat_, _xenix_, _xfs_, _xiafs_. Note that coherent, sysv and xenix are equivalent and that _xenix_ and _coherent_ will be removed at some point in the future - use _sysv_ instead. Since kernel version 2.1.21 the types _ext_ and _xiafs_ do not exist anymore. Earlier, _usbfs_ was known as _usbdevfs_. Note, the real list of all supported filesystems depends on your kernel.

The programs mount and umount support filesystem subtypes. The subtype is defined by '.subtype' suffix. For example 'fuse.sshfs'. It's recommended to use subtype notation rather than add any prefix to the mount source (for example 'sshfs#example.com' is depreacated).

For most types all the mount program has to do is issue a simple [mount](https://linux.die.net/man/2/mount)(2) system call, and no detailed knowledge of the filesystem type is required. For a few types however (like nfs, nfs4, cifs, smbfs, ncpfs) ad hoc code is necessary. The nfs, nfs4, cifs, smbfs, and ncpfs filesystems have a separate mount program. In order to make it possible to treat all types in a uniform way, mount will execute the program /sbin/mount._TYPE_ (if that exists) when called with type _TYPE_. Since various versions of the smbmount program have different calling conventions, /sbin/mount.smbfs may have to be a shell script that sets up the desired call.

If no -t option is given, or if the auto type is specified, mount will try to guess the desired type. Mount uses the blkid or volume_id library for guessing the filesystem type; if that does not turn up anything that looks familiar, mount will try to read the file _/etc/filesystems_, or, if that does not exist, _/proc/filesystems_. All of the filesystem types listed there will be tried, except for those that are labeled "nodev" (e.g., _devpts_, _proc_ and _nfs_). If _/etc/filesystems_ ends in a line with a single * only, mount will read _/proc/filesystems_ afterwards.

The auto type may be useful for user-mounted floppies. Creating a file _/etc/filesystems_ can be useful to change the probe order (e.g., to try vfat before msdos or ext3 before ext2) or if you use a kernel module autoloader. Warning: the probing uses a heuristic (the presence of appropriate 'magic'), and could recognize the wrong filesystem type, possibly with catastrophic consequences. If your data is valuable, don't ask mount to guess.

More than one type may be specified in a comma separated list. The list of filesystem types can be prefixed with no to specify the filesystem types on which no action should be taken. (This can be meaningful with the -a option.) For example, the command:

mount -a -t nomsdos,ext

mounts all filesystems except those of type _msdos_ and _ext_.

-O, --test-opts _opts_
Used in conjunction with -a, to limit the set of filesystems to which the -a is applied. Like -t in this regard except that it is useless except in the context of -a. For example, the command:

mount -a -O no_netdev

mounts all filesystems except those which have the option __netdev_ specified in the options field in the _/etc/fstab_ file.

It is different from -t in that each option is matched exactly; a leading no at the beginning of one option does not negate the rest.

The -t and -O options are cumulative in effect; that is, the command

mount -a -t ext2 -O _netdev

mounts all ext2 filesystems with the _netdev option, not all filesystems that are either ext2 or have the _netdev option specified.

-o, --options _opts_
Options are specified with a -o flag followed by a comma separated string of options. For example:

mount LABEL=mydisk -o noatime,nouser

For more details, see FILESYSTEM INDEPENDENT MOUNT OPTIONS and FILESYSTEM SPECIFIC MOUNT OPTIONS sections.

-B, --bind
Remount a subtree somewhere else (so that its contents are available in both places). See above.

-R, --rbind
Remount a subtree and all possible submounts somewhere else (so that its contents are available in both places). See above.

-M, --move
Move a subtree to some other place. See above
```

La opción `-o` le permite montar el sistema de archivos con una o más opciones separadas por comas. Las opciones se enumeran aquí:

```
Filesystem Independent Mount Options

Some of these options are only useful when they appear in the _/etc/fstab_ file.

Some of these options could be enabled or disabled by default in the system kernel. To check the current setting see the options in /proc/mounts.

The following options apply to any filesystem that is being mounted (but not every filesystem actually honors them - e.g., the sync option today has effect only for ext2, ext3, fat, vfat and ufs):

async
All I/O to the filesystem should be done asynchronously. (See also the sync option.)

atime
Do not use noatime feature, then the inode access time is controlled by kernel defaults. See also the description for strictatime and relatime mount options.

noatime
Do not update inode access times on this filesystem (e.g, for faster access on the news spool to speed up news servers).

auto
Can be mounted with the -a option.

noauto
Can only be mounted explicitly (i.e., the -a option will not cause the filesystem to be mounted).

context=_context_, fscontext=_context_, defcontext=_context_ and rootcontext=_context_

The context= option is useful when mounting filesystems that do not support extended attributes, such as a floppy or hard disk formatted with VFAT, or systems that are not normally running under SELinux, such as an ext3 formatted disk from a non-SELinux workstation. You can also use context= on filesystems you do not trust, such as a floppy. It also helps in compatibility with xattr-supporting filesystems on earlier 2.4.<x> kernel versions. Even where xattrs are supported, you can save time not having to label every file by assigning the entire disk one security context.

A commonly used option for removable media is context=system_u:object_r:removable_t.

Two other options are fscontext= and defcontext=, both of which are mutually exclusive of the context option. This means you can use fscontext and defcontext with each other, but neither can be used with context.

The fscontext= option works for all filesystems, regardless of their xattr support. The fscontext option sets the overarching filesystem label to a specific security context. This filesystem label is separate from the individual labels on the files. It represents the entire filesystem for certain kinds of permission checks, such as during mount or file creation. Individual file labels are still obtained from the xattrs on the files themselves. The context option actually sets the aggregate context that fscontext provides, in addition to supplying the same label for individual files.

You can set the default security context for unlabeled files using defcontext= option. This overrides the value set for unlabeled files in the policy and requires a filesystem that supports xattr labeling.

The rootcontext= option allows you to explicitly label the root inode of a FS being mounted before that FS or inode because visable to userspace. This was found to be useful for things like stateless linux.

For more details, see [selinux](https://linux.die.net/man/8/selinux)(8)

defaults
Use default options: rw, suid, dev, exec, auto, nouser, async, and relatime.

dev
Interpret character or block special devices on the filesystem.

nodev
Do not interpret character or block special devices on the file system.

diratime
Update directory inode access times on this filesystem. This is the default.

nodiratime
Do not update directory inode access times on this filesystem.

dirsync
All directory updates within the filesystem should be done synchronously. This affects the following system calls: creat, link, unlink, symlink, mkdir, rmdir, mknod and rename.

exec
Permit execution of binaries.

noexec
Do not allow direct execution of any binaries on the mounted filesystem. (Until recently it was possible to run binaries anyway using a command like /lib/ld*.so /mnt/binary. This trick fails since Linux 2.4.25 / 2.6.0.)

group
Allow an ordinary (i.e., non-root) user to mount the filesystem if one of his groups matches the group of the device. This option implies the options nosuid and nodev (unless overridden by subsequent options, as in the option line group,dev,suid).

iversion
Every time the inode is modified, the i_version field will be incremented.

noiversion
Do not increment the i_version inode field.

mand
Allow mandatory locks on this filesystem. See [fcntl](https://linux.die.net/man/2/fcntl)(2).

nomand
Do not allow mandatory locks on this filesystem.

_netdev

The filesystem resides on a device that requires network access (used to prevent the system from attempting to mount these filesystems until the network has been enabled on the system).

nofail
Do not report errors for this device if it does not exist.

relatime
Update inode access times relative to modify or change time. Access time is only updated if the previous access time was earlier than the current modify or change time. (Similar to noatime, but doesn't break mutt or other applications that need to know if a file has been read since the last time it was modified.)

norelatime
Do not use relatime feature. See also the strictatime mount option.

strictatime
Allows to explicitly requesting full atime updates. This makes it possible for kernel to defaults to relatime or noatime but still allow userspace to override it. For more details about the default system mount options see /proc/mounts.

nostrictatime
Use the kernel's default behaviour for inode access time updates.

suid
Allow set-user-identifier or set-group-identifier bits to take effect.

nosuid
Do not allow set-user-identifier or set-group-identifier bits to take effect. (This seems safe, but is in fact rather unsafe if you have suidperl(1) installed.)

owner
Allow an ordinary (i.e., non-root) user to mount the filesystem if he is the owner of the device. This option implies the options nosuid and nodev (unless overridden by subsequent options, as in the option line owner,dev,suid).

remount
Attempt to remount an already-mounted filesystem. This is commonly used to change the mount flags for a filesystem, especially to make a readonly filesystem writeable. It does not change device or mount point.

The remount functionality follows the standard way how the mount command works with options from fstab. It means the mount command doesn't read fstab (or mtab) only when a _device_ and _dir_ are fully specified.

mount -o remount,rw /dev/foo /dir

After this call all old mount options are replaced and arbitrary stuff from fstab is ignored, except the loop= option which is internally generated and maintained by the mount command.

mount -o remount,rw /dir
After this call mount reads fstab (or mtab) and merges these options with options from command line ( -o ).

ro
Mount the filesystem read-only.

_rnetdev
Like _netdev, except "fsck -a" checks this filesystem during rc.sysinit.

rw
Mount the filesystem read-write.

sync
All I/O to the filesystem should be done synchronously. In case of media with limited number of write cycles (e.g. some flash drives) "sync" may cause life-cycle shortening.

user
Allow an ordinary user to mount the filesystem. The name of the mounting user is written to mtab so that he can unmount the filesystem again. This option implies the options noexec, nosuid, and nodev (unless overridden by subsequent options, as in the option line user,exec,dev,suid).

nouser
Forbid an ordinary (i.e., non-root) user to mount the filesystem. This is the default.

users
Allow every user to mount and unmount the filesystem. This option implies the options noexec, nosuid, and nodev (unless overridden by subsequent options, as in the option line users,exec,dev,suid).
```
### Desconectar un sistema de archivos
Puede desconectar un sistema de archivos de la estructura de directorio virtual de Linux con el comando `umount`. ¡Cuidado aquí! No hay una `n` en el comando `umount` y necesitarás privilegios de super usuario para usarlo, como se muestra en este sistema Ubuntu:

```sh
ls -F /home/christine/Temp 
a_file.txt  lost+found/

sudo umount /home/christine/Temp [sudo] 
password for christine:

ls -F /home/christine/Temp
```

Observe en el directorio anterior que el punto de montaje del directorio, `/home/christine/Temp`, se usa con el comando `umount` en lugar del nombre de archivo del dispositivo, `/dev/sdb1`. Si bien puede utilizar el nombre de archivo del dispositivo, se recomienda utilizar el punto de montaje del directorio en caso de que el dispositivo esté montado en varias ubicaciones.

Tenga en cuenta que si el sistema de archivos que desea desmontar está siendo utilizado por un proceso o tiene archivos abiertos, no puede separarlo de la estructura de directorios. El siguiente ejemplo muestra un sistema de archivos montado en un sistema Ubuntu que no se puede desmontar porque el sistema de archivos está en uso:

```sh
sudo mount -t ext4 /dev/sdb1 Temp 
[sudo] password for christine:

sudo umount Temp 
umount: /home/christine/Temp: device is busy.
        (In some cases useful info about processes that use          
        the device is found by lsof(8) or fuser(1)) $
```

Afortunadamente, el comando `umount` ofrece algunos consejos útiles. Puede utilizar el comando `lsof` o `fuser` para determinar qué mantiene ocupado el sistema de archivos, como se muestra aquí:

```sh
lsof Temp
COMMAND PID USER       FD   TYPE DEVICE SIZE/OFF NODE NAME 
bash    1580 christine cwd  DIR  8,17   4096     2    Temp 
nano    5008 christine cwd  DIR  8,17   4096     2    Temp

fuser Temp
/home/christine/Temp:  1580c  5008c
```

En el ejemplo anterior, el comando `lsof` muestra los detalles de los procesos que actualmente utilizan el directorio Temp. Los detalles indican que la usuaria Christine está usando el editor de texto `nano` en un archivo dentro del directorio Temp. El fusor tiene una breve salida que muestra los PID del proceso y un código (c) que indica que el directorio actual del proceso es `/home/christine/Temp`. Puede encontrar una descripción completa de varios códigos de fusor escribiendo man fuser en la línea de comando. Una vez que estos procesos ya no mantienen ocupado el directorio, el sistema de archivos se puede desconectar exitosamente del directorio Temp.
### Adjuntar medios extraíbles manualmente
Muchas distribuciones detectan y montan automáticamente medios extraíbles. Sin embargo, hay ocasiones en las que el sistema no monta automáticamente los medios extraíbles o usted no desea que los medios se monten en los puntos de montaje predeterminados. En estos casos, puede montar manualmente los medios extraíbles.

Para montar medios extraíbles manualmente, el comando no es diferente del comando que usa para montar temporalmente un sistema de archivos. Sólo asegúrese de que el punto de montaje exista previamente y utilice el tipo de sistema de archivos correcto como se muestra aquí:

```sh
sudo mount -t vfat /dev/sdd1 Temp 
[sudo] password for christine:

ls Temp
AAA_Work_ToDo              peazip-5.9.0.LINUX.GTK2.tgz
curl-7.46.0.tar.gz         Shell_Scripts
[...]
```

Las unidades flash a menudo se formatean como VFAT o NTFS. El sistema de archivos EXT2 también es popular para las unidades flash. El almacenamiento óptico tiene diferentes sistemas de archivos, como se cubre más adelante en este capítulo.

Si no conoce el tipo de sistema de archivos o el nombre del dispositivo para sus medios extraíbles, puede usar el comando `DMESG` o `BLKID` (o ambos). Aquí se muestra un ejemplo de estos dos comandos en acción:

```sh
dmesg
[...]
[ 3882.584572]  sdd: sdd1
[ 3882.635207] sd 6:0:0:0: [sdd] No Caching mode page found
[ 3882.635211] sd 6:0:0:0: [sdd] Assuming drive cache: write through
[ 3882.635213] sd 6:0:0:0: [sdd] Attached SCSI removable disk
[...]

sudo blkid
[...]
/dev/sdd1**: SEC_TYPE="msdos" LABEL="TRAVELDRIVE" UUID="65AA-9655"
 TYPE="vfat"
```

El uso de estos comandos le permite encontrar que el nombre de archivo del dispositivo de unidad flash es `/dev/sdd1` y que está formateado como un tipo de sistema de archivos VFAT. Observe que el comando `BLKID` también proporciona información de UUID y etiqueta para los medios extraíbles.
Una útil utilidad para usar con medios extraíbles es el comando `Sync`. El comando `Sync` le permite "descargar" los buffers del sistema de archivos. En otras palabras, las actualizaciones de metadatos del sistema de archivos que residen en la memoria se escriben en las estructuras del sistema de archivos en los medios. La utilidad `sync` obliga al proceso de compromiso de datos a tener lugar de inmediato. Esto le permite separar los medios extraíbles de manera segura de la estructura del directorio sin preocuparse por la corrupción. Aquí se muestra un ejemplo de usar sincronización:

```sh
cp Documents/Listing_c04_Ubuntu_mount-t.odt Temp/

sync 
echo $?
0
sudo umount Temp 
[sudo] password for christine:
```

En el ejemplo anterior, se copia un archivo a la unidad flash USB montada manualmente en TEMP. El comando `Sync` se usa para enjuagar los buffers del sistema de archivos. La utilidad `sync` proporciona un estado de salida, que puede ver utilizando el `Echo $?`. Un cero (0) indica que todo está bien, mientras que uno (1) indica que ha ocurrido un problema. Debido a que no hubo errores reportados por `Sync`, la unidad flash se desmoronó de forma segura utilizando el comando `Umount`.
### Adjuntar un sistema de archivos de manera persistente
En lugar de adjuntar manualmente sus sistemas de archivos después de cada reinicio del sistema, puede tenerlos adjuntos por el sistema cuando se inicia. Esto se realiza a través de un registro colocado en el archivo `/etc/fstab`, que se llama apropiadamente la tabla del sistema de archivos.

En términos generales, cada registro `/ETC/FSTAB` consta de seis campos. Cualquier registro precedido por una marca hash (`#`) se considera una línea de comentarios. Los siguientes elementos describen estos campos.

**Partition o volumen** Una partición de dispositivo, como `/dev/sda1`, generalmente se enumera aquí. Un volumen lógico también podría enumerarse aquí. Volúmenes lógicos comienzan con `/dev/mapper/`.

Otro método para identificar una partición o volumen del dispositivo es mediante el uso de una etiqueta. Las etiquetas se pueden configurar en nombres fáciles de usar, como `TMPDIR`, en particiones cuyo nombre de archivo del dispositivo puede ser fácil de olvidar, como `/dev/sdf3`. Se asigna una etiqueta cuando la partición o volumen se formatean usando `MKFS`. Posiblemente puede determinar la etiqueta de un sistema de archivos utilizando el comando `E2Label`.

En lugar de una partición o volumen del dispositivo, se puede usar un identificador universalmente único (`UUID`), y se están convirtiendo en el método preferido para la identificación de partición dentro de `/etc/fStab`. Un `UUID`, como su nombre lo indica, es un número de identificación único. Este número se asigna cuando la partición o volumen se formatean usando `MKFS`. Puede determinar el `UUID` de un sistema de archivos utilizando el comando `BLKID`. Este número es persistente, y es especialmente útil si tiene una gran cantidad de particiones adjuntas a su sistema.

**Punto de montaje** El punto de montaje es la referencia de directorio absoluto para donde se va a conectar la partición o volumen a la estructura del directorio de Linux. Este es el mismo `Mount_Point` que usaría con el comando `mount`, si tuviera que montar el sistema de archivos temporalmente. Para un sistema de archivos de intercambio, verá el intercambio de palabras clave aquí. 

**Tipo de sistema de archivos** El tipo de sistema de archivos es el código de tipo de sistema de archivos utilizado para identificar el formato del sistema de archivos o del sistema de volumen. Es el mismo `Fstype` que usaría con el comando `mount` si tuviera que montar el sistema de archivos temporalmente.
Para un sistema de archivos de intercambio, verá el intercambio de palabras clave aquí. 

**Opciones de montaje** Las palabras clave separadas por comas enumeradas aquí son las diversas opciones de montaje que puede configurar en el sistema de archivos. Son las mismas opciones que usaría con el comando `Mount -O` si montara el sistema de archivos temporalmente. 

**Selección de copia de seguridad** Este campo es un campo booleano, ya que se puede establecer en 0 (falso) o 1 (verdadero). A 0 indica que la utilidad de volcado no realizará una copia de seguridad en este sistema de archivos. A 1 indica que la utilidad del volcado realizará una copia de seguridad. Si la utilidad de copia de seguridad de volcado no se usa en el sistema, esta configuración se ignora. No tiene ningún efecto en otras utilidades de respaldo.

**Orden de verificación de integridad** Este campo se puede establecer en un blanco, 0, 1 o 2, y es utilizado por la utilidad `FSCK` en el arranque del sistema. Un en blanco o 0 indica que `FSCK` nunca debe ejecutarse en el sistema de archivos en el arranque del sistema.

A 1 indica que este sistema de archivos tiene prioridad, y debe verificarse, si es necesario, antes de cualquier otro sistema de archivos. Por lo general, el sistema de archivos montado en root (`/`) es el único sistema de archivos establecido con este indicador.

A 2 indica que este sistema de archivos debe verificarse, si es necesario, en el arranque del sistema. Sin embargo, él y cualquier otro sistema de archivos debido a una verificación y establecido en 2 se verificarán después de que se verifique los sistemas de archivos establecidos en 1.
Se muestra un archivo de muestra `/etc/fstab` en el Listado 4.1. Este archivo de muestra no es de ninguna distribución en particular, sino que se creó solo con fines educativos. 

```sh
#partition          mount point fs type  options       dump  fsck
/dev/sda1           /           ext4     defaults      0     1
UUID=7e32f35e-[...] /boot       xfs      defaults      0     0
Label=Temp          /home/temp  ext4     users, noauto 0     0 
/dev/sdb3           /var        ext4     defaults      0     2 
server01:/nfsshare  /tmp/share  nfs      users         0     0 
/dev/mapper/a-swap  swap        swap     defaults      0     0
```

Veamos el archivo de muestra `/etc/fstab` línea por línea.

**Línea 1** Cualquier línea precedida por una marca hash (`#`) en este archivo es una línea de comentarios. Por lo general, encontrará los encabezados de la columna enumerados como un comentario, lo cual es útil.

**Línea 2** La partición, `/dev/sda1`, se debe montar en la raíz (`/`) en la estructura del directorio virtual. Es un sistema de archivos EXT4, y todas las opciones de montaje predeterminadas (`RW`, `Suid`, `Dev`, `Exec`, `Auto`, `Nouser` y `Async`) deben usarse. La utilidad de copia de seguridad del volcado no se usa en este sistema y, por lo tanto, se enumera un cero (0) en la columna de volcado para este sistema de archivos. Dado que este es el directorio raíz, este sistema de archivos tiene prioridad y debe verificarse, si es necesario, antes de cualquier otro sistema de archivos. Por lo tanto, un uno (1) se enumera en la columna `FSCK`.

**Línea 3** Esta partición se identifica en `/etc/fStab` por su número UUID. El número se corta en el listado, y el UUID completo para esta partición es 7E32F35E -C9E1–4AA9–8BABDF362221D706. Un número UUID es largo, porque es un número de identificación único. Incluso con su larga longitud, los UUID se están convirtiendo en el método preferido para la identificación de partición dentro de `/etc/fstab`. Esta partición es un tipo de sistema de archivos `XFS`, y está montado en el punto de montaje `/boot`. La utilidad `FSCK` no se ejecuta en los sistemas de archivos `XFS` y, por lo tanto, se enumera un cero (0) en la columna `FSCK` para este sistema de archivos.

**Línea 4** Esta partición en particular usa una etiqueta para identificación, `Label=temp`. Además, observe que tiene algunas opciones establecidas, `users` y `noauto`. La opción `users` permite a cualquier usuario autorizado usar este sistema, no solo aquellos con privilegios de súper usuario, para montar o desmontar esta partición etiquetada. Además, la opción `Noauto` evita que la partición se monte en el momento del arranque o cuando se emite un comando de `mount -a`.

**Línea 5** La partición `/dev/sdb3` está montada en `/var`. Tenga en cuenta que en su columna `FSCK`, se usa un número dos (2). Esto significa que este sistema de archivos debe verificarse, si es necesario, en el arranque del sistema. Sin embargo, si `/dev/sda1` se debe verificar, `/dev/sdb3` se verificará después de `/dev/sda1` se ha verificado.

**Línea 6** El `servidor01:/NFSSHare` es un sistema de sistema de archivo de red (`NFS`) compartido. 

**Línea 7** La última línea en el listado de muestra `/etc/fstab`, `/dev/mapper/a-swap`, es un volumen lógico. Este volumen particular está montado como el sistema de archivos de intercambio. 
Cuando el sistema se reinicia, emitirá el comando `Mount -A`. Cada sistema de archivos enumerado en `/etc/fStab`, que no tiene la opción `noauto` establecida, se montará a su punto de montaje designado en la estructura del directorio virtual del sistema.
### Mirando las unidades de montaje `Systemd`
Las distribuciones que usan `Systemd` tienen opciones adicionales para adjuntar persistentemente los sistemas de archivos.

Los sistemas de archivos se pueden especificar dentro del archivo `/etc/fstab` o dentro de un archivo de unidad de montaje. Un archivo de unidad de montaje proporciona información de configuración para `SystemD`  para montar y controlar los sistemas de archivos designados.

Se crea un solo archivo de unidad de montaje para cada punto de montaje, y el nombre del archivo contiene la referencia de directorio absoluto del punto de montaje. Sin embargo, la referencia del directorio absoluto tiene su corte hacia adelante (`/`); Las bases posteriores se convierten en guiones (`-`); y se elimina cualquier corte hacia adelante. Los nombres de los archivos de la unidad de montaje también tienen una extensión. `Mount`. Por ejemplo, el punto de montaje, `/home/temp/`, tendría un archivo de unidad de montaje llamado `Home-Temp.mount`.

El contenido de un archivo de unidades de montaje imita otros archivos de la unidad `Systemd`, con algunas secciones y opciones especiales. Usando el punto `/home/temp/mount`, aquí hay un archivo de unidad de montaje de ejemplo para ello:

```sh
cat /etc/systemd/system/home-temp.mount
[Unit]
Description=Test Mount Units

[Mount]
What=/dev/sdo1
Where=/home/temp
Type=ext4
Options=defaults
SloppyOptions=on
TimeOutSec=4

[Install]
WantedBy=multi-user.target
```

Hay tres secciones necesarias como mínimo para este punto de montaje particular: [Unidad], [Monte] e [Instalar]. La opción qué opción dentro de la sección [MONTACIÓN] puede usar el nombre del archivo del dispositivo o un UUID, como `/dev/disk/by-uuid/uuid`.

El `sloppyOptions` es útil, ya que si se establece en `On`, ignora cualquier opción de montaje que no sea compatible con un tipo de sistema de archivos en particular. Por defecto, está configurado en `OFF`. Otra opción útil es el tiempo de espera. Si el comando de montaje no se completa por el número de segundos designados, el soporte se considera una operación fallida.

Asegúrese de incluir la sección [Install] y configure las opciones `WantedBy` o las Opciones requeridas. Si no hace esto, el sistema de archivos no se montará en un reinicio del servidor.
Se debe probar cualquier archivo de unidad de montaje recién configurado, especialmente antes de realizar un reinicio del sistema. Primero pruebe un montaje manual del sistema de archivos como se muestra cortado aquí:

```sh
blkid | grep /dev/sdo1 
/dev/sdo1: UUID="474c1322-[...]" TYPE="ext4"

mkdir /home/temp

touch /home/temp/test_mount_units.txt

ls /home/temp 
test_mount_units.txt

mount -t ext4 /dev/sdo1 /home/temp

ls /home/temp 
lost+found

umount /home/temp

ls /home/temp 
test_mount_units.txt 
```

Una vez que haya probado el nuevo sistema de archivos a través del montaje manual y desmontándolo, se prueba el archivo de la unidad de montaje. Usando el archivo de unidad de montaje de ejemplo, lo siguiente demuestra probarlo en una distribución de CentOS:

```sh
systemctl daemon-reload

systemctl start home-temp.mount

ls /home/temp 
lost+found #
```

En el ejemplo anterior, el primer comando vuelve a cargar `Systemd` y el segundo comando tiene `Systemd` de montar el sistema de archivos utilizando el archivo de la unidad de montaje `home-Temp.Mount`. El segundo comando `SystemCTL` es similar a cómo se inicia un servicio, ya que utiliza el comando `Start`.

A continuación, asegúrese de que el sistema de archivos esté montado correctamente. El comando `mount` funciona en esta situación, y también lo hace el comando `SystemCTL`. Al igual que un servicio, utiliza el comando `SystemCTL` para obtener el estado de un sistema de archivos montado como se muestra cortado aquí:

```sh
mount | grep /home/temp 
/dev/sdo1 on /home/temp type ext4 (rw,relatime,data=ordered)

systemctl status home-temp.mount
• home-temp.mount - Test Mount Units
   Loaded: loaded (/etc/systemd/system/home-temp.mount; [...]
   Active: active (mounted) since Sat 2017-06-11 16:34:2[...]
    Where: /home/temp
     What: /dev/sdo1
  Process: 3990 ExecMount=/bin/mount /dev/sdo1 /home/temp[...]
[...]
```

Se requiere un paso adicional. Para garantizar que `Systemd` monte el sistema de archivos de manera persistente, el archivo de la unidad de montaje debe habilitarse como se muestra aquí:

```sh
systemctl enable home-temp.mount
Created symlink from
/etc/systemd/system/multi-user.target.wants/home-temp.mount to /etc/systemd/system/home-temp.mount.
```

Tenga en cuenta que solo debe usar archivos de Unidad de montaje si necesita ajustar la configuración del sistema de archivos persistente. Si no lo hace, es mejor usar el registro A `/ETC/FSTAB` para montar el sistema de archivos de manera persistente. Para obtener más información sobre el archivo de la unidad de montaje, consulte las páginas `Systemd.Mount Man`.
### Visualización de sistemas de archivos adjuntos
Si desea ver la estructura de accesorio del sistema de archivos actual de su sistema o ver los atributos de varios dispositivos de bloque, hay varias herramientas útiles disponibles. Cada uno proporciona un punto de vista diferente de la estructura del directorio virtual y sus medios de almacenamiento subyacentes.

Un comando simple para comenzar es el comando `MountPoint`. No requiere privilegios de súper usuario. Simplemente escriba en `MountPoint Directory_Reference` en la línea de comandos, y si recibe el mensaje es un punto de montaje, entonces se ha montado un sistema de archivos en esa ubicación de directorio en particular, como se muestra en la distribución de Ubuntu aquí:

```sh
mountpoint  / 
/ is a mountpoint

mountpoint /home
/home is not a mountpoint
```

Otro buen comando es `Blkid`. Con el comando `BLKID`, puede ver los diversos dispositivos de bloque y sus atributos. No se requieren privilegios de súper usuario para ver parte de la información; Sin embargo, las cuentas sin privilegios de súper usuario reciben información en caché no verificada o ninguna. Aquí hay un ejemplo recortado de usar el comando `BLKID` en una distribución de Ubuntu:

```sh
blkid

sudo blkid 
[sudo] password for christine:
/dev/sda1: UUID="0dc214d2-[...] TYPE="ext4"
/dev/sda5: UUID="1b0f22a2-[...] TYPE="swap"
/dev/sdb1: UUID="06c41b8c-[...] TYPE="ext4"
/dev/sdc1: UUID="14ca54ba-[...] TYPE="ext4"
/dev/sdc2: LABEL="Extra" UUID="82558d44-[...]" TYPE="ext4"

sudo blkid -L Extra
/dev/sdc2

sudo blkid -U 14ca54ba-ee44–4588-a32c-dee848a0435f
/dev/sdc1

$
```

Observe en el ejemplo anterior de que el uso de privilegios de súper usuario con el comando `BLKID` generalmente proporciona información más exhaustiva (y, por lo tanto, es una buena idea usarla con privilegios de súper usuarios). Observe también que puede mostrar información sobre un dispositivo de bloque particular utilizando su etiqueta (`opción -l`) o su UUID (`-U opción`). Si lo desea, puede especificar un solo nombre de archivo de dispositivo con el comando `BLKID`, como se muestra aquí en una distribución de CentOS:

```sh
blkid /dev/sda1 
/dev/sda1: UUID="7e32f35e-[...] TYPE="xfs"
```

El comando `LSBLK` también puede ser una utilidad útil. Funciona de manera similar al comando `BLKID` en el sentido de que también muestra la información del dispositivo de bloque. Dado que algunas de sus opciones extraen información del comando `BLKID`, es mejor tener privilegios de súper usuarios al emplearla. Aquí hay dos ejemplos de comando `LSBLK SNPED` en una distribución de CentOS:

```sh
lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT 
sda               8:0    0    8G  0 disk

├─sda1            8:1    0  500M  0 part /boot 
└─sda2            8:2    0  7.5G  0 part
  ├─centos-root 253:0    0  6.7G  0 lvm  /
  └─centos-swap 253:1    0  820M  0 lvm  [SWAP]
[...]

lsblk -f
NAME         FSTYPE      LABEL UUID             MOUNTPOINT 
sda

├─sda1       xfs               7e32f35e-[...]   /boot
└─sda2       LVM2_member       YlVA3C-[...]
  ├─centos-root
             xfs               1ea0c68f-[...]   /
  └─centos-swap
             swap              09502922-[...]   [SWAP]
[...]
```

La opción `-f` utilizada con `LSBLK` mostrará los UUID y etiquetas del dispositivo de bloque, si se usa. Tenga en cuenta que no todas las distribuciones muestran UUID del dispositivo de bloque con el comando y opción `LSBLK -F`.

Otra utilidad que puede encontrar útil es el comando `E2Label`. Con esta utilidad, puede ver cualquier etiqueta del sistema de archivos para un sistema de archivos Ext2, Ext3 o Ext4, como se muestra aquí en una distribución de Ubuntu:

```sh
sudo e2label /dev/sdc2
[sudo] password for christine:
Extra
```

Observe que se requieren privilegios de súper usuario para usar el comando `E2Label`. También puede cambiar la etiqueta pasando un nuevo nombre de etiqueta después del nombre del dispositivo en esta cadena de comando.

La utilidad `FindFS` también puede ser útil para administrar sus sistemas de archivos. Le permite ver el dispositivo de bloque asociado con un UUID o etiqueta particular, como se muestra en un sistema Ubuntu aquí:

```sh
findfs LABEL=Extra
/dev/sdc2

findfs UUID="82558d44–16af-4f2c-8670–6f54732bb31b"
/dev/sdc2
```

El comando `FindFS` no requiere privilegios de supervisión de súper. Sin embargo, desafortunadamente, al escribir un UUID del sistema de archivos para el comando `FindFS`, la finalización del comando de pestaña del shell no está disponible.

Además de las utilidades mencionadas hasta ahora, otras utilidades pueden ser útiles, incluidas estas: 
`FindMnt`: muestra sistemas de archivos montados en un formato de árbol.
`DF`: Muestra el uso del espacio del disco del sistema de archivos montado, e incluye el punto de montaje del sistema de archivos.
`mount`: muestra sistemas de archivos montados e incluye el punto de montaje del sistema de archivos.
Puede usar la opción `-l` en el comando `mount` para mostrar etiquetas y puede usar el comando `-t fstype` para reducir su lista solo para ciertos tipos de sistemas de archivos, como se muestra en este Snip desde una distribución de CentOS:

```sh
mount -t xfs
/dev/mapper/centos-root on / type xfs [...]
/dev/sda1 on /boot type xfs [...]
```

Todas estas utilidades son muy útiles para administrar sus sistemas de archivos. Es posible que no los necesite en cada situación, pero son útiles para saber por las diversas circunstancias que puede encontrar en sus sistemas Linux.
### Explorando temas adicionales del sistema de archivos
Ciertos temas del sistema de archivos requieren una discusión adicional. Estos incluyen mirar los sistemas de archivos, como la memoria, Swap, BTRFS, etc. Además, los sistemas de archivos que se pueden montar automáticamente (fuera del archivo `/etc/fstab`) son un tema especial que requiere detalles adicionales.
### Mirando los sistemas de archivos Linux basados en la memoria
Al cubrir los sistemas de archivos, un tema que merece algo de atención especial es los sistemas de archivos Linux virtuales o basados en la memoria. Estos sistemas de archivos son únicos porque sus datos residen dentro de la memoria del sistema, pero puede ver sus datos utilizando sus puntos de montaje.
A menudo encontrará estos sistemas de archivos basados en la memoria montados en `/dev`, `/proc`, `/sys` y `/run` o uno de sus subdirectorios. Algunos ejemplos de sistemas de archivos basados en la memoria son `Devpts`, `Proc`, `SYSFS` y `TMPFS`.

Para comprender esto un poco mejor, veamos archivos `PROC`. Los archivos en el sistema de archivos `PROC` están basados en memoria (virtual), generalmente contienen información del sistema y se actualizan continuamente, aunque no muestran información de tamaño en sus listados de archivos. Aquí se muestra el listado largo de un archivo de `Proc` virtual en un ejemplo del sistema CentOS:

```sh
ls -l /proc/cpuinfo
-r--r--r--. 1 root root 0 Jan 13 13:12 /proc/cpuinfo
```

Aunque el archivo `/proc/cpuinfo` reside en la memoria, al utilizar el punto de montaje del sistema de archivos, se puede acceder o ver los datos. Aquí hay un ejemplo recortado de cómo mostrar los datos del archivo `/proc/cpuinfo`, que reside en la memoria:

```sh
cat /proc/cpuinfo
processor    : 0
vendor_id    : GenuineIntel
[...] 
power management:
```

Estos sistemas de archivos se crean cuando se inicia el sistema y, a menudo, el sistema los monta automáticamente. Sin embargo, si se necesitan opciones especiales para estos sistemas de archivos basados en memoria, las verá enumeradas en el archivo `/etc/fstab`.

Debido a que estos sistemas de archivos se basan en la memoria, cuando un sistema se apaga, todos los datos que residen en estos sistemas de archivos se eliminan. Por lo tanto, son un excelente medio para almacenar sistemas, procesos y otra información temporal.
### Mirando el sistema de archivos `Btrfs`
El sistema de archivos `Btrfs` adopta un enfoque único sobre cómo se logra el formateo y el montaje de alto nivel. Merece una atención especial.

`Btrfs`, un sistema de archivos relativamente nuevo, fue creado para manejar archivos y sistemas de archivos de gran tamaño, así como la escalabilidad necesaria. El sistema de archivos `Btrfs` utiliza una estructura de datos de árbol B, de ahí su nombre. Esta estructura de datos proporciona un método competente para acceder y actualizar grandes bloques de datos almacenados en el sistema de archivos. Este método también puede seguir siendo competente a medida que crece el tamaño del sistema de archivos.

El sistema de archivos `Btrfs` proporciona integridad de datos a través de COW. Esta implementación COW, además de proteger los metadatos, proporciona instantáneas, lo que le permite mover el sistema de archivos a una instantánea anterior en caso de que ocurra un desastre. El término instantánea, tal como se utiliza aquí, se refiere a una unidad distinta. Comparte los datos y metadatos con la partición de la instantánea original, pero actúa como su propia partición al permitir que se agreguen archivos (que no aparecerán en la partición original) y se puede montar de forma independiente.

`Btrfs` también proporciona integridad de datos a través de una función de suma de comprobación y su propia funcionalidad RAID integrada. Puede configurar configuraciones RAID 0, RAID 1 o RAID 10 utilizando `Btrfs`.
Los atributos de rendimiento y escalabilidad de `Btrfs` incluyen su propia gestión integrada de volúmenes lógicos. También proporciona compresión y desfragmentación de datos.

Unos pocos ejemplos sencillos le ayudarán a comprender el sistema de archivos `Btrfs`. 

Primero, formatear particiones con el sistema de archivos `Btrfs` es similar a realizar otro formateo de alto nivel usando el comando `mkfs`. El ejemplo que se muestra aquí se realiza en dos particiones, porque necesitará al menos dos particiones para implementar `Btrfs RAID`:

```sh
mkfs -t btrfs  /dev/sdb  /dev/sdc
Btrfs v3.16.2 
See [http://btrfs.wiki.kernel.org f](http://btrfs.wiki.kernel.org/)or more information.
Turning ON incompat feature 'extref':
increased hardlink limit per file to 65536
adding device /dev/sdc id 2 
fs created label (null) on /dev/sdb
  nodesize 16384 leafsize 16384 sectorsize 4096 size 8.00GiB #
```

En el ejemplo anterior, debido a que no se usaron opciones además de `-t btrfs` y se incluyeron dos particiones, `Btrfs` está configurado para usar RAID 0 (división de discos) para datos y RAID 1 (duplicación) para sus metadatos. Otras opciones le permitirán configurar diferentes tipos de RAID. Además, puedes incluir más de dos particiones.
Luego puede montar el sistema de archivos `Btrfs`. Sin embargo, sólo necesita montar una de las particiones para montar el volumen RAID del sistema de archivos `Btrfs`, como se muestra aquí:

```sh
mkdir BTrial

mount /dev/sdb BTrial

ls BTrial

touch BTrial/file_b.txt**

ls BTrial
file_b.txt
```

Una vez montado el volumen del sistema de archivos `Btrfs`, puede usarlo como cualquier otro sistema de archivos, como se muestra en el ejemplo anterior. Sin embargo, tenga en cuenta que no hay ningún directorio `lost+found` como lo vería en un punto de montaje del sistema de archivos ext4.
Un comando útil para ayudarle con su sistema de archivos `Btrfs` es el comando `btrfs filesystem show`. Aquí se muestra un ejemplo de este comando:

```sh
btrfs filesystem show
Label: none  uuid: 5125431c-37c3–4d70-aa85–42b8b4fea161
       Total devices 2 FS bytes used 384.00KiB        
       devid    1 size 4.00GiB used 847.12MiB path /dev/sdb        
       devid    2 size 4.00GiB used 827.12MiB path /dev/sdc
Btrfs v3.16.2
```

### Explorando los subvolúmenes `Btrfs`
Otra característica interesante de `Btrfs` son los subvolúmenes. Los subvolúmenes `Btrfs` pueden actuar como subdirectorios de un sistema de archivos `Btrfs` montado. No son verdaderos subdirectorios porque se pueden montar por separado de su volumen principal. Aunque se puede montar un subvolumen `Btrfs`, no es un dispositivo de bloque. Un subvolumen `Btrfs` es una estructura organizativa.

Los subvolúmenes `Btrfs` son útiles en determinadas situaciones. Por ejemplo, puede mantener un conjunto de subvolúmenes y montarlos según sean necesarios los datos que contienen.
Para crear un subvolumen, primero se debe montar el volumen `Btrfs` principal. La sintaxis básica para crear un subvolumen es la siguiente.

```sh
btrfs subvolume create Mount_Point/Subvolume_Name
```

`Mount_Point` es el punto de montaje del volumen `Btrfs` principal actual. `Subvolume_Name` es el nombre del subvolumen.
Para demostrar la creación de un subvolumen, usaremos el sistema de archivos `Btrfs` creado anteriormente. Antes de crear un subvolumen, el sistema de archivos `Btrfs` (volumen principal) debe montarse como se muestra aquí en una distribución CentOS usando privilegios de superusuario:

```sh
mount /dev/sdb BTrial

ls BTrial/ 
file_b.txt

btrfs subvolume create BTrial/subvolume_1
Create subvolume 'BTrial/subvolume_1'
```