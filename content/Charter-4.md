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

Una vez creado el subvolumen, denominado `subvolumen_1` en el ejemplo anterior, se accede al subvolumen a través de una referencia de directorio. Puede crear archivos adicionales, subdirectorios e incluso subvolúmenes adicionales dentro del subvolumen.

Verifica los subvolúmenes mediante el comando `subvolume list` del volumen principal junto con `mount point` . La opción `-t` es útil porque muestra la información en formato de tabla como se muestra aquí:

```sh
btrfs subvolume list  BTrial
ID 258 gen 13 top level 5 path subvolume_1

btrfs subvolume list -t BTrial
ID   gen   top level   path
--   ---   ---------   ----
258   13   5           subvolume_1
```

Para acceder al subvolumen, utiliza una referencia de directorio que incluye el punto de montaje de su volumen principal y el nombre del subvolumen. En esencia, se accede al subvolumen como un subdirectorio del punto de montaje del volumen principal. Aquí hay un ejemplo:

```sh
cd BTrial/subvolume_1

pwd
/root/BTrial/subvolume_1

touch file_b_subvol.txt

ls
file_b_subvol.txt

cd

pwd
/root

ls -R BTrial/
BTrial: 
file_b.txt  subvolume_1 

BTrial/subvolume_1: 
file_b_subvol.txt
```

De forma predeterminada, para montar un volumen principal y un subvolumen Btrfs, solo necesita montar el volumen principal:

```sh
umount BTrial

mount /dev/sdb BTrial

btrfs subvolume list -t BTrial
ID   gen   top level   path
--   ---   ---------   ----
258   14   5           subvolume_1
```

Una vez montado el volumen principal, se pueden verificar los subvolúmenes montados. Esto se hace mediante el comando `subvolume list`, como se muestra en el ejemplo anterior.

El acceso a los volúmenes principales y subvolúmenes de Btrfs se realiza a través de un punto de entrada. Este punto de entrada se denomina nivel predeterminado y normalmente se establece en el nivel superior (a veces denominado subvolumen de nivel superior). El nivel superior estándar tiene un ID 5, como se muestra en el ejemplo anterior.
Puede determinar el nivel predeterminado de un subvolumen mediante el comando `subvolume get-default`. El ejemplo que se muestra aquí confirma que el nivel predeterminado actual es el nivel superior (ID 5):

```sh
btrfs subvolume get-default BTrial
ID 5 (FS_TREE)
```

Un subvolumen se puede montar independientemente de su volumen principal. Sin embargo, si el nivel predeterminado del subvolumen se establece en ID 5 (nivel superior), aún se puede acceder a los datos del volumen principal. Recuerde que los subvolúmenes Btrfs no son verdaderos dispositivos de bloques.

Existen dos métodos para montar un subvolumen y no permitir el acceso al volumen principal. Para el primer método, debe modificar las opciones de `mount`. En el siguiente ejemplo, el volumen principal y el subvolumen se desmontan y luego el subvolumen se monta de manera que impida el acceso al volumen principal:

```sh
umount BTrial

mkdir BTrial_subvol

mount -o subvol=subvolume_1 /dev/sdb BTrial_subvol

ls BTrial_subvol/
file_b_subvol.txt

umount BTrial_subvol
```

Después de desmontar el volumen principal, se crea un nuevo directorio (punto de montaje), `BTrial_subvol`. A continuación, el subvolumen se monta utilizando una opción de montaje especial `-o subvol=subvolume_name`, donde `subvolume_name` es `subvolume_1`, el nombre del subvolumen de ejemplo. Una lista de directorio muestra solo los datos del subvolumen y no se proporciona acceso al volumen principal.

El segundo método para montar un subvolumen y bloquear el acceso al volumen principal es cambiar el número de identificación de nivel predeterminado del subvolumen. El número de identificación del nivel predeterminado cambia de 5 al número de identificación del subvolumen. El subvolumen debe estar montado porque el punto de montaje se utiliza en el comando que cambia este número de ID. El comando `subvolume set-default` se utiliza para realizar esta tarea, como se muestra aquí:

```sh
mount /dev/sdb BTrial

btrfs subvolume list -t BTrial
ID   gen   top level   path
--   ---   ---------   ----
258   14   5           subvolume_1

btrfs subvolume get-default BTrial/subvolume_1
ID 5 (FS_TREE)

btrfs subvolume set-default 258 BTrial/subvolume_1

btrfs subvolume get-default BTrial/subvolume_1
ID 258 gen 14 top level 5 path subvolume_1

umount BTrial
```

Una vez que se cambia el nivel predeterminado del subvolumen, solo se usa un comando de montaje simple. No se concede acceso al volumen principal. Un ejemplo de esto se muestra aquí:

```sh
mount /dev/sdb BTrial_subvol

ls BTrial_subvol/
file_b_subvol.txt

btrfs subvolume get-default BTrial_subvol
ID 258 gen 14 top level 5 path subvolume_1

btrfs subvolume list -t BTrial_subvol
ID   gen   top level   path
--   ---   ---------   ----
258   14   5           subvolume_1

umount BTrial_subvol
```

### Explorando los Btrfs Snapshots
Una vez que comprenda los subvolúmenes de Btrfs, podrá explorar más a fondo los Btrfs Snapshots, porque los Snapshots también son subvolúmenes. Los Snapshots son bastante fáciles de crear y administrar.

Para crear un Snapshots, se debe montar el volumen o subvolumen principal. El comando `btrfs` a utilizar es `subvolume Snapshots`. La sintaxis básica de este comando es la siguiente:
`btrfs subvolume snapshot Volume_Mount_Point Snapshot_Name`
El `Volume_Mount_Point` en el comando de instantánea del subvolumen designa qué volumen o subvolumen montado se debe tomar la instantánea. `Snapshot_Name` en el comando designa el punto de montaje del subvolumen de la instantánea.

A partir de los ejemplos anteriores de Btrfs, se crea una instantánea del subvolumen montado en `BTrial_subvol`. El comando `Snapshot` está dividido en dos líneas para mayor claridad y se muestra en el ejemplo aquí:

```sh
mount /dev/sdb BTrial_subvol

ls BTrial_subvol/
file_b_subvol.txt

btrfs subvolume snapshot BTrial_subvol \
> BTrial_subvol/my_snapshot
Create a snapshot of 'BTrial_subvol' in 'BTrial_subvol/my_snapshot'

ls -RF BTrial_subvol/
BTrial_subvol/
file_b_subvol.txt  my_snapshot/

BTrial_subvol/my_snapshot: 
file_b_subvol.txt #
```

Debido a que un `snapshot` es un subvolumen, puede ver sus detalles mediante el comando `subvolume list`. Aquí se muestra un ejemplo, utilizando la instantánea creada anteriormente:

```sh
btrfs subvolume list BTrial_subvol
ID 258 gen 27 top level 5 path subvolume_1
ID 259 gen 26 top level 258 path my_snapshot
```

Al igual que los subvolúmenes normales, los subvolúmenes de instantáneas se pueden montar con su volumen principal o por separado. Además, es bastante sencillo crear un subvolumen de instantánea del sistema. La creación de un subvolumen de instantánea antes de la actualización del software permite revertir fácilmente a la versión anterior del software, en caso de que surja la necesidad.
Obviamente, hay muchas cosas en el sistema de archivos Btrfs. Si desea obtener más información, escriba `man btrfs-filesystem` en la línea de comando o utilice su motor de búsqueda web favorito. 
### Mirando los sistemas de archivos de intercambio
El término sistema de archivos de intercambio es realmente inexacto. Una partición de intercambio no contiene un sistema de archivos, sino que es una ubicación especial en el disco que actúa como espacio de intercambio del sistema (también llamado memoria virtual). 

Normalmente, se crea, formatea y agrega una partición de intercambio al archivo de configuración `/etc/fstab` durante la instalación del sistema. Sin embargo, es posible que necesite crear y administrar particiones de intercambio adicionales, por ejemplo, si aumenta la RAM de su sistema.

Hay un par de utilidades útiles disponibles para verificar su espacio de intercambio actual. Lo más probable es que ya estés familiarizado con el comando `free`. Pero es posible que no esté familiarizado con el uso del comando `swapon` para las estadísticas del espacio de intercambio, como se muestra aquí en una distribución de CentOS:

```sh
free -m
	  total   used   free   shared   buff/cache   available
Mem:   993     467    136    7        390          365
Swap:  819     0      819

swapon -s
Filename   Type        Size    Used   Priorit
/dev/dm-1  partition   839676  0      -1
```

En el ejemplo anterior, la opción `-m` se usa con el comando `free` para mostrar las estadísticas de memoria en megabytes. Tenga en cuenta que este es un sistema bastante silencioso en cuanto a memoria. Además, la opción `-s` se utiliza con el comando `swapon` para mostrar las estadísticas del espacio de intercambio. En algunas distribuciones, puede obtener la misma información del archivo `/proc/swaps`.

La columna Prioridad dentro de las estadísticas del espacio de intercambio del ejemplo anterior se muestra como negativa (-1). El número de prioridad determina qué espacio de intercambio se utiliza primero (si hay varios espacios de intercambio). Si no establece el número de prioridad, lo crea el kernel de Linux y se establecerá en un número negativo. Puedes establecer la prioridad tú mismo y, si lo haces, debe ser un número positivo. Los números más altos obtienen una mayor preferencia de uso.

Una vez que haya creado una nueva partición de disco, el comando `mkswap` se usa para "formatear" la partición en una partición de intercambio. A continuación se muestra un ejemplo en un sistema CentOS, utilizando privilegios de super usuario:

```sh
mkswap /dev/sdd1

Setting up swapspace version 1, size = 838652 KiB 
no label, UUID=3297cded-69e9–4d35-b29f-c50cf263fb8b

blkid
[...]
/dev/sdd1: UUID="3297cded-[...]-c50cf263fb8b" TYPE="swap"
```

Ahora que la partición de intercambio se ha preparado adecuadamente, puede activarla usando el comando `swapon`, como se muestra aquí:

```sh
swapon /dev/sdd1

swapon -s
Filename   Type        Size    Used   Priority
/dev/dm-1  partition   839676  0      -1
/dev/sdd1  partition   838652  0      -2

free -m
	  total   used   free   shared   buff/cache   available
Mem:   993     581    66     8        345          249
Swap:  1638    0      1638
```

Puede ver que el tamaño del espacio de intercambio ha aumentado significativamente debido a la adición de una segunda partición de intercambio. Si lo desea, la prioridad de uso de la nueva partición de intercambio se puede cambiar de su actual negativo dos (-2) a una prioridad más alta usando el comando `swapon`, como se muestra aquí:

```sh
swapoff /dev/sdd1

swapon -p 0 /dev/sdd1

swapon -s
Filename   Type        Size    Used   Priority
/dev/dm-1  partition   839676  4      -1
/dev/sdd1  partition   838652  0      0
```

Primero debe usar el comando `swapoff` en la partición de intercambio antes de cambiar su prioridad y luego usar el comando `swapon -p prioridad` para cambiar la prioridad de preferencia. Puede establecer la prioridad en cualquier número entre 0 y 32767. Para las diversas opciones disponibles con el comando `swapon`, escriba `man swapon` en la línea de comando.

Si todo está bien con su nueva partición de intercambio, debe agregarla al archivo `/etc/fstab` para que sea persistente. Puede imitar fielmente la configuración de registro de la partición de intercambio actual, pero asegúrese de cambiar el nombre de la partición a su nueva partición de intercambio.
### Mirando los sistemas de archivos basados en red
Algunos sistemas de archivos no están conectados localmente, sino que residen físicamente en medios de almacenamiento conectados a la red. Estos sistemas de archivos basados en red se comparten en toda la red.

Los sistemas de archivos que se pueden incluir en esta categoría son NFS y Sistema de archivos común de Internet (CIFS), que se implementa a través de Samba  y se llama SMBFS en sistemas más antiguos.

Puede ampliar un poco la definición del sistema de archivos para incluir el almacenamiento conectado en red (NAS), que tiene distribuciones completas de Linux disponibles para implementarlo, como OpenMediaVault. NAS normalmente utiliza NFS o CIFS como núcleo. Mientras ampliamos las definiciones, incluyamos las redes conectadas a almacenamiento (SAN). Puede implementar una SAN con el protocolo iSCSI en Linux.
### Comprender el montaje automático
Muchas distribuciones montan automáticamente medios extraíbles, como unidades flash USB y DVD, en un directorio virtual de Linux. Normalmente, en varias distribuciones actuales, los medios extraíbles se montan automáticamente en el directorio `/run` o `/media`. La administración dinámica de dispositivo es responsable de manejar las funciones de montaje automático de estos dispositivos. Las distribuciones de Linux más antiguas utilizaban el demonio de capa de abstracción de hardware (`HALd`) y, a menudo, montaban medios extraíbles en el directorio `/mnt`.
### Explorando AutoFS
Otro tipo de montaje automático está orientado a sistemas de archivos basados en red. Por ejemplo, el servicio de montaje automático, `AutoFS`, puede gestionar las funciones de montaje automático de los sistemas de archivos NFS, así como las de otros sistemas de archivos basados en red. Puede colocar sistemas de archivos NFS en el archivo de configuración `/etc/fstab` para que se monten automáticamente al iniciar el sistema. Sin embargo, en algunos casos, el sistema puede experimentar problemas de rendimiento al utilizar esta disposición. Al permitir que `AutoFS` administre el montaje de sistemas de archivos NFS, evitará estos problemas. Por ejemplo, una forma en que `AutoFS` ayuda con el rendimiento del sistema es que los sistemas de archivos NFS se montan cuando se accede a ellos en lugar de en el momento del inicio del sistema. Esto hace que el proceso de arranque sea mucho más rápido.

`AutoFS` utiliza el archivo `/etc/auto.master`, también llamado mapa maestro, como su archivo de configuración principal para administrar el almacenamiento de red conectado automáticamente. El archivo de mapa maestro brinda al servicio `AutoFS` información sobre los sistemas de archivos basados en red, incluido dónde se encuentran actualmente, dónde se montarán y las opciones a usar.
Excepto por las líneas de comentarios que están precedidas por una almohadilla (`#`), cada entrada del mapa maestro tiene este formato básico:

```sh
mount-point map-name [ mount-options ]
```

Las entradas en el mapa maestro son uno de tres tipos de mapas diferentes. Cada tipo de mapa determina la sintaxis exacta de la entrada del mapa maestro. Estos mapas se describen aquí:
**Built-in-map** El archivo de mapa incorporado se activa al tener `-hosts` en el campo de nombre del mapa de un mapa maestro. Tiene `AutoFS` para montar todos los sistemas de archivos NFS disponibles desde cualquier servidor NFS listado dentro de un directorio especial, `/net`. (Esto a veces se denomina montaje diferido, pero el mapeo integrado suena mejor).

Por ejemplo, si desea montar el sistema de archivos NFS del servidor NFS, Server01, necesitará el directorio `/net/Server01`, junto con la entrada de mapa incorporada en el archivo de mapa maestro. El sistema de archivos NFS del Servidor01 se montaría automáticamente en `/net/Server01`. Por lo tanto, los directorios no sólo sirven como disparadores para el mapa integrado, sino que también sirven como punto de montaje. Puede tener varios directorios en `/net`, uno para cada servidor NFS. Por ejemplo, si también tiene sistemas de archivos NFS en Server02 y Server03, los directorios `/net/Server02` y `/net/Server03` también actuarían como activadores para el mapa integrado y los puntos de montaje.

Una entrada de mapa incorporada típica en el archivo de mapa maestro se ve así:

```sh
/net   -hosts
```

**Direct map** Una entrada de mapa directo es simplemente un puntero a otro archivo. El otro archivo es `/etc/auto.direct`. Esta entrada normalmente no está en el mapa maestro de forma predeterminada, por lo que si la deseas, tendrás que agregarla. Una entrada típica de mapa directo en el archivo de mapa maestro se ve así:

```sh
/-  /etc/auto.direct
```

Dentro del archivo `/etc/auto.direct`, se enumeran los nombres de ruta de directorio absolutos para los puntos de montaje, así como las opciones y sus servidores asociados. Dos entradas típicas en el archivo de mapa directo pueden verse así:

```sh
/home/bucket server01.acme.com:/home/bucket
/mnt/nfs/var/nfsshare  192.168.56.101:/var/nfsshare
```

**IndirectMaps** Una entrada de mapa indirecto también es un puntero a otro archivo. El otro archivo es `/etc/auto.directory`, donde el directorio coincide con el punto de montaje. Por ejemplo, la típica entrada de mapa indirecto predeterminada en el archivo del mapa maestro se ve así:

```
/misc /etc/auto.misc
```

El archivo `/etc/auto.misc` se utiliza normalmente para montar medios extraíbles, como sistemas de archivos ópticos o unidades flash USB. También tiene varias entradas disponibles para su uso si no incluyen ninguna marca hash anterior, como esta: 

```
cd -fstype=iso9660,ro,nosuid,nodev :/dev/cdrom
```

Debido a que este archivo es un mapa indirecto, esta entrada hará que cualquier CD se monte en el directorio `/misc`, específicamente usando el punto de montaje `/misc/cd`. Por lo tanto, aquí se aplica el término mapa indirecto. Mientras que un archivo de mapa directo indica una referencia de directorio absoluta, como `/home/bucket`, un archivo de mapa indirecto solo enumera un punto de mapa relativo, como cd, que se montará en el directorio que figura en su entrada de mapa maestro, como `/misceláneos`

Puede tener archivos de mapas indirectos adicionales según sea necesario. Por ejemplo, si su empresa tenía proyectos especiales llamados ProjectX y ProjectY, que requerían espacio de trabajo temporal (pero sin respaldo) en el directorio `/tmp` para varios sistemas, podría configurar dos sistemas de archivos NFS y luego agregar una entrada como tal en su mapa maestro:

```
/tmp /etc/auto.tmp
```

Siguiendo con este ejemplo, crearía el archivo `/etc/auto.tmp`. Este archivo de mapa indirecto podría contener las dos entradas siguientes:

```
proyectox -fstype=nfs4,rw :/tmp/projectx 
proyectoy -fstype=nfs4,rw :/tmp/projecty
```

También se pueden incluir mapas secundarios adicionales, que son útiles si tiene una implementación de sistema de archivos basado en red a gran escala. Esta entrada en el mapa maestro incluye todos los mapas (cuyas entradas deben seguir el mismo formato que las del archivo de mapa maestro) ubicados en el directorio `/etc/auto.master.d/`:

```
+dir:/etc/auto.master.d
```

Cuando modifique la configuración de `AutoFS` y los archivos de mapas, deberá reiniciar su servicio `AutoFS`. Además, recuerde que necesitará acceder al directorio que se montará automáticamente mediante `AutoFS` (un comando `ls` será suficiente) para activar el montaje automático de ese directorio. Puede verificar que el directorio esté montado usando el comando `df`. Si el directorio no se está montando, verifique el archivo `/var/log/messages` para ver si hay mensajes de error pertinentes.

`AutoFS` y sus mapas permiten una gran flexibilidad para el montaje automático de sistemas de archivos basados en red. Si decide configurar `AutoFS` y agregarle cualquier sistema de archivos basado en red que actualmente esté montado mediante el archivo `/etc/fstab`, asegúrese de eliminarlo de `/etc/fstab` o tendrá algunas situaciones interesantes durante su próximo reinicio de sistema. 
### Explorando unidades de montaje automático
Si su servidor Linux tiene `systemd`, puede configurar el montaje bajo demanda, así como el montaje en paralelo utilizando unidades de montaje automático. Además, puede configurar los sistemas de archivos para que se desmonten automáticamente ante la falta de actividad.

Un archivo de configuración de unidad de montaje automático funciona de manera muy similar a un archivo de unidad de montaje. La convención de nomenclatura es la misma, excepto que la extensión del archivo es `.automount`.

Dentro de un archivo de configuración de unidad de montaje automático, solo hay tres opciones disponibles. La opción Dónde es una opción obligatoria y está configurada exactamente de la misma manera que en los archivos de la unidad de montaje.

La opción `DirectoryMode` no es una opción obligatoria. La configuración de la opción determina los permisos colocados en cualquier punto de montaje y directorio principal creado automáticamente. De forma predeterminada, está configurado en el código octal 0755.

La opción `TimeOutIdleSec` tampoco es necesaria. Esta opción particular le permite configurar la cantidad de tiempo (en segundos) que un sistema de archivos montado ha estado inactivo. Una vez que se alcanza el límite de tiempo, el sistema de archivos se desmonta. Por defecto esta opción está deshabilitada.
### Mirando los sistemas de archivos cifrados
Otro grupo de sistemas de archivos que merece una mirada son los sistemas de archivos cifrados. El cifrado es el proceso de convertir texto que un humano o una máquina puede leer (texto sin formato) en texto que un humano o una máquina no puede leer (texto cifrado) y viceversa, utilizando un algoritmo (cifrado). El descifrado invierte el proceso, permitiéndole acceder/leer el texto y, por lo general, requiere una clave (o un conjunto de claves) mediante el algoritmo. La(s) clave(s) suele ser una frase de contraseña, que es similar a una contraseña.

En Linux se pueden utilizar un par de sistemas de archivos cifrados con Linux e incluyen los siguientes:
**dm-crypt El cifrado dm-crypt** se puede implementar utilizando la utilidad `cryptsetup`. Este tipo puede resultar un poco confuso, porque el software detrás de `cryptsetup` se llama `dm-crypt`, y su tipo de cifrado muy básico también se llama `dm-crypt`.

Los sistemas de archivos cifrados `dm-crypt` utilizan Device Mapper. Esto permite que las aplicaciones utilicen texto sin formato, mientras que cualquier escritura en el volumen está cifrada.
A menos que tenga un buen conocimiento del cifrado, no se recomienda utilizar el tipo `dmcrypt`. Utiliza un hash de frase de contraseña sin sal para su clave única y no mantiene metadatos en el volumen.

`eCryptfs` Un tipo de sistema de archivos cifrado más nuevo, `eCryptfs`, es en realidad un pseudosistema de archivos en el sentido de que está superpuesto a un sistema de archivos actual. La capa proporciona capacidades de cifrado, que incluyen elegir qué algoritmo de cifrado utilizar, como AES, Blowfish, des3_ede, etc.

Una de las cosas más interesantes de `eCryptfs` es que no hay nuevos comandos de utilidad que aprender. Siempre que tenga el paquete de software `ecryptfs-utils` en su sistema, simplemente use el comando `mount` con `eCryptfs` de la siguiente manera:

```sh
mount -t ext4 /dev/sdd1 /home
mount -t eCryptfs /home /home
```

El primer comando de montaje adjunta la partición a la estructura del directorio virtual de Linux. El segundo comando de montaje coloca el sistema de archivos `eCryptfs` encima.

El sistema de archivos `eCryptfs` cifra una partición o volumen archivo por archivo. Además, los archivos cifrados se pueden copiar entre varios sistemas, porque los metadatos de `eCryptfs` se almacenan en el encabezado de cada archivo.

Puede agregar opciones como tamaño de bytes de clave, elección de cifrado, cifrado de nombre de archivo, etc. mediante la opción `-o` del comando `mount`. Además, los volúmenes `eCryptfs` se pueden montar automáticamente al iniciar el sistema mediante entradas en el archivo `/etc/fstab`.

**Configuración de clave unificada de Linux (LUKS)** LUKS es un tipo de sistema de archivos cifrado `dm-crypt` mejorado. También se puede implementar utilizando la utilidad `cryptsetup` y utiliza Device Mapper. Es el método preferido sobre el tipo básico `dm-crypt`.

LUKS utiliza una clave maestra y varias claves de usuario. Mantiene metadatos en el volumen y proporciona funciones antiforenses mejoradas.

Tenga en cuenta que el cifrado no significa protección contra desastres de hardware. Sólo ayuda a proteger los datos de quienes no deberían tener acceso a ellos. Aún necesita emplear todos los demás elementos y métodos importantes para proteger la integridad de sus datos.
### Mantenimiento de sistemas de archivos Linux
Parte de la gestión de un sistema Linux incluye el mantenimiento adecuado de sus sistemas de archivos a través de varias utilidades del sistema disponibles para este fin. El mantenimiento del sistema de archivos comprende la manipulación de sistemas de archivos estándar a través de utilidades como `tune2fs`, monitorear el estado de un sistema de archivos y repararlos cuando se encuentran problemas.
### Ajustar un sistema de archivos
Es posible que sea necesario ajustar un sistema de archivos por varias razones, y estas pueden incluir muchos elementos diferentes. Por ejemplo, puede decidir cambiar la etiqueta de un sistema de archivos porque ya no refleja el propósito del sistema de archivos.

Las utilidades para ajustar sistemas de archivos suelen ser específicas de un determinado sistema de archivos o grupo de sistemas de archivos. Para los sistemas de archivos extendidos ext2, ext3 y ext4, puede utilizar las utilidades.
### Cómo ver la información del sistema de archivos EXT2/EXT3/EXT4

**dumpe2fs** es una herramienta de línea de comandos que se utiliza para volcar información del sistema de archivos ext2/ext3/ext4, lo que significa que muestra información de super bloques y grupos de bloques para el sistema de archivos en el dispositivo.

Antes de ejecutar **dumpe2fs**, asegúrese de ejecutar el comando `df -hT` para conocer los nombres de los dispositivos del sistema de archivos.

```sh
sudo dumpe2fs /dev/sda10
```

##### Sample Output

```sh
dumpe2fs 1.42.13 (17-May-2015)
Filesystem volume name:   
Last mounted on:          /
Filesystem UUID:          bb29dda3-bdaa-4b39-86cf-4a6dc9634a1b
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
Filesystem flags:         signed_directory_hash 
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              21544960
Block count:              86154752
Reserved block count:     4307737
Free blocks:              22387732
Free inodes:              21026406
First block:              0
Block size:               4096
Fragment size:            4096
Reserved GDT blocks:      1003
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Sun Jul 31 16:19:36 2016
Last mount time:          Mon Nov  6 10:25:28 2017
Last write time:          Mon Nov  6 10:25:19 2017
Mount count:              432
Maximum mount count:      -1
Last checked:             Sun Jul 31 16:19:36 2016
Check interval:           0 ()
Lifetime writes:          2834 GB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:	          256
Required extra isize:     28
Desired extra isize:      28
Journal inode:            8
First orphan inode:       6947324
Default directory hash:   half_md4
Directory Hash Seed:      9da5dafb-bded-494d-ba7f-5c0ff3d9b805
Journal backup:           inode blocks
Journal features:         journal_incompat_revoke
Journal size:             128M
Journal length:           32768
Journal sequence:         0x00580f0c
Journal start:            12055
```

Puedes pasar el indicador `-b` para mostrar cualquier bloque reservado como incorrecto en el sistema de archivos (ninguna salida implica bloques incorrectos):

```sh
dumpe2fs -b
```

### Comprobación de errores en los sistemas de archivos EXT2/EXT3/EXT4

**e2fsck** se utiliza para examinar los sistemas de archivos ext2/ext3/ext4 en busca de errores y `fsck` verificaciones y, opcionalmente, puede reparar un sistema de archivos Linux; Básicamente es una interfaz para una variedad de verificadores de sistemas de archivos (`fsck.fstype` por ejemplo `fsck.ext3`, `fsck.sfx` etc) que se ofrecen en Linux.

Recuerde que Linux ejecuta `e2fack/fsck` automáticamente al iniciar el sistema en las particiones etiquetadas para registrar el archivo de configuración `/etc/fstab` . Normalmente, esto se hace después de que un sistema de archivos no se ha desmontado limpiamente.

**Atención**: No ejecute `e2fsck` o `fsck` en sistemas de archivos montados, siempre desmonte una partición antes de poder ejecutar estas herramientas en ella, como se muestra a continuación.

```sh
sudo unmount /dev/sda10
sudo fsck /dev/sda10
```

Alternativamente, habilite la salida detallada con el interruptor `-V` y use `-t` para especificar un tipo de sistema de archivos como este:

```sh
sudo fsck -Vt ext4 /dev/sda10
```

### Tuning EXT2/EXT3/EXT4 Filesystems

Mencionamos desde el principio que una de las causas del daño del sistema de archivos es el ajuste incorrecto. Puede utilizar la utilidad `tune2fs` para cambiar los parámetros ajustables de los sistemas de archivos ext2/ext3/ext4 como se explica a continuación.

Para ver el contenido del super bloque del sistema de archivos, incluidos los valores actuales de los parámetros, use la opción `-l` como se muestra.

```sh
sudo tune2fs -l /dev/sda10
```
##### Sample Output

```sh
tune2fs 1.42.13 (17-May-2015)
Filesystem volume name:   
Last mounted on:          /
Filesystem UUID:          bb29dda3-bdaa-4b39-86cf-4a6dc9634a1b
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
Filesystem flags:         signed_directory_hash 
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              21544960
Block count:              86154752
Reserved block count:     4307737
Free blocks:              22387732
Free inodes:              21026406
First block:              0
Block size:               4096
Fragment size:            4096
Reserved GDT blocks:      1003
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         8192
Inode blocks per group:   512
Flex block group size:    16
Filesystem created:       Sun Jul 31 16:19:36 2016
Last mount time:          Mon Nov  6 10:25:28 2017
Last write time:          Mon Nov  6 10:25:19 2017
Mount count:              432
Maximum mount count:      -1
Last checked:             Sun Jul 31 16:19:36 2016
Check interval:           0 ()
Lifetime writes:          2834 GB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:	          256
Required extra isize:     28
Desired extra isize:      28
Journal inode:            8
First orphan inode:       6947324
Default directory hash:   half_md4
Directory Hash Seed:      9da5dafb-bded-494d-ba7f-5c0ff3d9b805
Journal backup:           inode blocks
```

A continuación, utilizando el indicador `-c` , puedes establecer el número de montajes después de los cuales `e2fsck` comprobará el sistema de archivos. Este comando indica al sistema que ejecute `e2fsck` en `/dev/sda10` después de cada **4** montajes.

```sh
sudo tune2fs -c 4 /dev/sda10

tune2fs 1.42.13 (17-May-2015)
Setting maximal mount count to 4
```

También puedes definir el tiempo entre dos comprobaciones del sistema de archivos con la opción `-i` . El siguiente comando establece un intervalo de **2** días entre comprobaciones del sistema de archivos.

```sh
sudo tune2fs  -i  2d  /dev/sda10

tune2fs 1.42.13 (17-May-2015)
Setting interval between checks to 172800 seconds
```

Ahora, si ejecuta este comando a continuación, el intervalo de verificación del sistema de archivos para `/dev/sda10` ahora está configurado.

```sh
sudo tune2fs -l /dev/sda10
```

##### Sample Output

```sh
Filesystem created:       Sun Jul 31 16:19:36 2016
Last mount time:          Mon Nov  6 10:25:28 2017
Last write time:          Mon Nov  6 13:49:50 2017
Mount count:              432
Maximum mount count:      4
Last checked:             Sun Jul 31 16:19:36 2016
**Check interval:           172800 (2 days)**
Next check after:         Tue Aug  2 16:19:36 2016
Lifetime writes:          2834 GB
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:	          256
Required extra isize:     28
Desired extra isize:      28
Journal inode:            8
First orphan inode:       6947324
Default directory hash:   half_md4
Directory Hash Seed:      9da5dafb-bded-494d-ba7f-5c0ff3d9b805
Journal backup:           inode blocks
```

Para cambiar los parámetros de registro predeterminados, utilice la opción `-J` . Esta opción también tiene subopciones: **size=diario-tamaño** (establece el tamaño del diario), **device=external-diario** (especifica el dispositivo en el que se almacena) y `ubicación=diario-ubicación` (define la ubicación de la revista).

Tenga en cuenta que solo se puede configurar una de las opciones de tamaño o dispositivo para un sistema de archivos:

```sh
sudo tune2fs -J size=4MB /dev/sda10
```

Por último, pero no menos importante, la etiqueta de volumen de un sistema de archivos se puede configurar usando la opción `-L` como se muestra a continuación.

```sh
sudo tune2fs -L "ROOT" /dev/sda10
```

### Debug EXT2/EXT3/EXT4 Filesystems

**debugfs** es un depurador de sistemas de archivos ext2/ext3/ext4, sencillo e interactivo, basado en una línea de comandos. Le permite modificar los parámetros del sistema de archivos de forma interactiva. Para ver subcomandos o solicitudes, escriba `"?"`.

```sh
sudo debugfs /dev/sda10
```

De forma predeterminada, el sistema de archivos debe abrirse en modo lectura-escritura; utilice el indicador `-w` para abrirlo en modo lectura-escritura. Para abrirlo en modo catastrófico, use la opción `-c` .

##### Sample Output

```sh
debugfs 1.42.13 (17-May-2015)
debugfs:  ?
Available debugfs requests:

show_debugfs_params, params
Show debugfs parameters
open_filesys, open       Open a filesystem
close_filesys, close     Close the filesystem
freefrag, e2freefrag     Report free space fragmentation
feature, features        Set/print superblock features
dirty_filesys, dirty     Mark the filesystem as dirty
init_filesys             Initialize a filesystem (DESTROYS DATA)
show_super_stats, stats  Show superblock statistics
ncheck                   Do inode->name translation
icheck                   Do block->inode translation
change_root_directory, chroot
[....]
```

Para mostrar la fragmentación del espacio libre, utilice la solicitud **freefrag** de este modo.
```
debugfs: freefrag
```

##### Sample Output

```sh
Device: /dev/sda10
Blocksize: 4096 bytes
Total blocks: 86154752
Free blocks: 22387732 (26.0%)

Min. free extent: 4 KB 
Max. free extent: 2064256 KB
Avg. free extent: 2664 KB
Num. free extent: 33625

HISTOGRAM OF FREE EXTENT SIZES:
Extent Size Range :  Free extents   Free Blocks  Percent
    4K...    8K-  :          4883          4883    0.02%
    8K...   16K-  :          4029          9357    0.04%
   16K...   32K-  :          3172         15824    0.07%
   32K...   64K-  :          2523         27916    0.12%
   64K...  128K-  :          2041         45142    0.20%
  128K...  256K-  :          2088         95442    0.43%
  256K...  512K-  :          2462        218526    0.98%
  512K... 1024K-  :          3175        571055    2.55%
    1M...    2M-  :          4551       1609188    7.19%
    2M...    4M-  :          2870       1942177    8.68%
    4M...    8M-  :          1065       1448374    6.47%
    8M...   16M-  :           364        891633    3.98%
   16M...   32M-  :           194        984448    4.40%
   32M...   64M-  :            86        873181    3.90%
   64M...  128M-  :            77       1733629    7.74%
  128M...  256M-  :            11        490445    2.19%
  256M...  512M-  :            10        889448    3.97%
  512M... 1024M-  :             2        343904    1.54%
    1G...    2G-  :            22      10217801   45.64%
debugfs:  
```

Puede explorar muchas otras solicitudes, como crear o eliminar archivos o directorios, cambiar el directorio de trabajo actual y mucho más, simplemente leyendo la breve descripción proporcionada. Para salir de `debugfs`, utilice la solicitud `q` .

Con algunas distribuciones migrando a XFS como sistema de archivos predeterminado, comprender las diversas utilidades XFS se ha vuelto aún más importante. Las utilidades utilizadas para modificar el sistema de archivos XFS:

`xfs_fsr` Se utiliza para desfragmentar sistemas de archivos XFS montados. Cuando se invoca sin argumentos, `xfs_fsr` desfragmenta todos los archivos normales en todos los sistemas de archivos XFS montados. Esta utilidad también permite a los usuarios suspender una desfragmentación en un momento específico y continuar desde donde la dejó más tarde.

Además, `xfs_fsr` también permite la desfragmentación de un solo archivo, como en `xfs_fsr _/path/to/file_`. Red Hat desaconseja desfragmentar periódicamente un sistema de archivos completo, ya que normalmente esto no está garantizado.

`xfs_bmap` Imprime el mapa de bloques de disco utilizados por los archivos en un sistema de archivos XFS. Este mapa enumera cada extensión utilizada por un archivo específico, así como las regiones del archivo sin bloques correspondientes (es decir, agujeros).

`xfs_info` Prints XFS file system information.

`xfs_admin` Cambia los parámetros de un sistema de archivos XFS. La utilidad `xfs_admin` solo puede modificar parámetros de dispositivos o sistemas de archivos desmontados.

`xfs_copy` Copia el contenido de un sistema de archivos XFS completo a uno o más destinos en paralelo.

Las siguientes utilidades también son útiles para depurar y analizar sistemas de archivos XFS:

`xfs_metadump` Copia los metadatos del sistema de archivos XFS en un archivo. La utilidad `xfs_metadump` solo debe usarse para copiar sistemas de archivos desmontados, de solo lectura o congelados/suspendidos; de lo contrario, los volcados generados podrían estar dañados o ser inconsistentes.

`xfs_mdrestore` Restaura una imagen de metavolcado XFS (generada mediante `xfs_metadump`) en una imagen del sistema de archivos.

`xfs_db` Debugs an XFS file system.

Es probable que el sistema de archivos Btrfs más nuevo aparezca en una distribución que esté administrando. Por lo tanto, hemos incluido utilidades para modificar el sistema de archivos Btrfs.

```
       balance
           Balance btrfs filesystem chunks across single or several
           devices.

       check
           Do off-line check on a btrfs filesystem.

       device
           Manage devices managed by btrfs, including add/delete/scan
           and so on.

       filesystem
           Manage a btrfs filesystem, including label setting/sync and
           so on.

       inspect-internal
           Debug tools for developers/hackers.

       property
           Get/set a property from/to a btrfs object.

       qgroup
           Manage quota group(qgroup) for btrfs filesystem.

       quota
           Manage quota on btrfs filesystem like enabling/rescan and
           etc.

       receive
           Receive subvolume data from stdin/file for restore and etc.

       replace
           Replace btrfs devices.

       rescue
           Try to rescue damaged btrfs filesystem.

       restore
           Try to restore files from a damaged btrfs filesystem.

       scrub
           Scrub a btrfs filesystem.

       send
           Send subvolume data to stdout/file for backup and etc.

       subvolume
           Create/delete/list/manage btrfs subvolume.
```

### Comprobación y reparación de un sistema de archivos
Proteger, monitorear y reparar un sistema de archivos van de la mano. Afortunadamente, hay muchas herramientas en esta categoría que puedes emplear.

Utilidades de administración de sistemas de archivos que son capaces de verificar y reparar sistemas de archivos. Estas herramientas a menudo se denominan herramientas `fsck`, donde `fsck` es una versión abreviada de verificación del sistema de archivos. En la mayoría de los casos, estas utilidades se ejecutan automáticamente durante el inicio del sistema, si es necesario, pero también se pueden invocar manualmente si es necesario.
### Escenarios que requieren una verificación del sistema de archivos
Las herramientas `fsck` relevantes se pueden utilizar para verificar su sistema si ocurre cualquiera de las siguientes situaciones:
- El sistema no arranca
- Los archivos de un disco específico se corrompen
- El sistema de archivos se cierra o cambia a solo lectura debido a inconsistencias
- Un archivo en el sistema de archivos es inaccesible

Las inconsistencias del sistema de archivos pueden ocurrir por varias razones, que incluyen, entre otras, errores de hardware, errores de administración de almacenamiento y errores de software.

Para los sistemas de archivos con registro en diario, todo lo que normalmente se requiere en el momento del arranque es reproducir el diario si es necesario y esta suele ser una operación muy breve.

Sin embargo, si se produce una inconsistencia o corrupción en el sistema de archivos, incluso para sistemas de archivos con registro en diario, se debe utilizar el verificador del sistema de archivos para reparar el sistema de archivos.
###  Posibles efectos secundarios de ejecutar `fsck`
Generalmente, se puede esperar que la ejecución de la herramienta de reparación y verificación del sistema de archivos repare automáticamente al menos algunas de las inconsistencias que encuentre. En algunos casos, pueden surgir los siguientes problemas:
- Los inodos o directorios gravemente dañados pueden descartarse si no se pueden reparar.
- Pueden ocurrir cambios significativos en el sistema de archivos.

Para garantizar que no se realicen cambios inesperados o no deseados de forma permanente, asegúrese de seguir los pasos de precaución descritos en el procedimiento.
### Mecanismos de manejo de errores en XFS
Esta sección describe cómo XFS maneja varios tipos de errores en el sistema de archivos.
- Desmontajes impuros

Journalling mantiene un registro transaccional de los cambios de metadatos que ocurren en el sistema de archivos.

En caso de una falla del sistema, un corte de energía u otro desmontaje no limpio, XFS usa el diario (también llamado registro) para recuperar el sistema de archivos. El kernel realiza una recuperación del diario al montar el sistema de archivos XFS.
#### Corrupción
En este contexto, la corrupción significa errores en el sistema de archivos causados por, por ejemplo:
- Fallos de hardware
- Errores en el firmware de almacenamiento, los controladores de dispositivos, la pila de software o el propio sistema de archivos
- Problemas que hacen que partes del sistema de archivos se sobrescriban con algo externo al sistema de archivos

Cuando XFS detecta daños en el sistema de archivos o en los metadatos del sistema de archivos, puede cerrar el sistema de archivos e informar el incidente en el registro del sistema. Tenga en cuenta que si la corrupción ocurrió en el sistema de archivos que aloja el directorio `/var`, estos registros no estarán disponibles después de reiniciar.

**System log entry reporting an XFS corruption**

```sh
# dmesg --notime | tail -15

XFS (loop0): Mounting V5 Filesystem
XFS (loop0): Metadata CRC error detected at xfs_agi_read_verify+0xcb/0xf0 [xfs], xfs_agi block 0x2
XFS (loop0): Unmount and run xfs_repair
XFS (loop0): First 128 bytes of corrupted metadata buffer:
00000000027b3b56: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000005f9abc7a: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000005b0aef35: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000000da9d2ded: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000001e265b07: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000006a40df69: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
000000000b272907: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
00000000e484aac5: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  ................
XFS (loop0): metadata I/O error in "xfs_trans_read_buf_map" at daddr 0x2 len 1 error 74
XFS (loop0): xfs_imap_lookup: xfs_ialloc_read_agi() returned error -117, agno 0
XFS (loop0): Failed to read root inode 0x80, error 11
```

Las utilidades de espacio de usuario suelen informar el mensaje de error de entrada/salida cuando intentan acceder a un sistema de archivos XFS dañado. Montar un sistema de archivos XFS con un registro dañado da como resultado un montaje fallido y el siguiente mensaje de error:

```sh
mount: : mount(2) system call failed: Structure needs cleaning.
```

Debe utilizar manualmente la utilidad `xfs_repair` para reparar la corrupción.
### Comprobación de un sistema de archivos XFS con `xfs_repair`
Este procedimiento realiza una verificación de solo lectura de un sistema de archivos XFS utilizando la utilidad `xfs_repair`. Debe utilizar manualmente la utilidad `xfs_repair` para reparar cualquier daño. A diferencia de otras utilidades de reparación de sistemas de archivos, `xfs_repair` no se ejecuta en el momento del arranque, incluso cuando un sistema de archivos XFS no se desmontó limpiamente. En caso de un desmontaje incorrecto, XFS simplemente reproduce el registro en el momento del montaje, lo que garantiza un sistema de archivos coherente; `xfs_repair` no puede reparar un sistema de archivos XFS con un registro sucio sin volver a montarlo primero.

Procedimiento
Reproduzca el registro montando y desmontando el sistema de archivos:

```sh
mount file-system
umount file-system
```

Utilice la utilidad `xfs_repair` para realizar un ensayo y comprobar el sistema de archivos. Cualquier error se imprime y una indicación de las acciones que se tomarían, sin modificar el sistema de archivos.

```sh
xfs_repair -n _block-device_
```

Monte el sistema de archivos:

```sh
mount file-system
```

#### Reparar un sistema de archivos XFS con `xfs_repair`
Este procedimiento repara un sistema de archivos XFS dañado utilizando la utilidad `xfs_repair`.
#### Procedimiento
Cree una imagen de metadatos antes de la reparación con fines de diagnóstico o prueba utilizando la utilidad `xfs_metadump`. Una imagen de metadatos del sistema de archivos previa a la reparación puede resultar útil para las investigaciones de soporte si la corrupción se debe a un error de software. Los patrones de corrupción presentes en la imagen previa a la reparación pueden ayudar en el análisis de la causa raíz.

Utilice la herramienta de depuración `xfs_metadump` para copiar los metadatos de un sistema de archivos XFS a un archivo. El archivo de metavolcado resultante se puede comprimir utilizando utilidades de compresión estándar para reducir el tamaño del archivo si es necesario enviar archivos de metavolcado grandes al soporte.

```sh
xfs_metadump block-device metadump-file
```

Vuelva a reproducir el registro volviendo a montar el sistema de archivos:

```sh
mount file-system
umount file-system
```

Utilice la utilidad `xfs_repair` para reparar el sistema de archivos desmontado:

Si el montaje se realizó correctamente, no se requieren opciones adicionales:

```sh
xfs_repair block-device
```

Si el montaje falló con el error La estructura necesita limpieza, el registro está dañado y no se puede reproducir. Utilice la opción `-L` (forzar la puesta a cero del registro) para borrar el registro:

```sh
xfs_repair -L block-device
```

Monte el sistema de archivos:

```sh
mount file-system
```
### Usando SMART
El acrónimo SMART significa "Tecnología de informes y análisis de autocontrol". Los dispositivos SMART suelen ser unidades de disco duro o de estado sólido. Sin embargo, también pueden ser unidades de cinta conectadas SCSI.

Un dispositivo SMART tiene un sistema incorporado que le permite comunicarse con el software de su sistema. Esta comunicación incluye proporcionar información sobre el estado del disco: posibles advertencias de fallas del disco y resultados de autopruebas.

El demonio `smartd` permite monitorear cualquier dispositivo SMART conectado que tenga capacidad SMART. Puede verificar los dispositivos cada tantos minutos y registrar errores a través de su archivo de registro configurado, de forma predeterminada `/var/log/smartd.log`, `/var/log/messages` o `/var/log/syslog`, dependiendo de su distribución.

Puede configurar `smartd` utilizando su archivo de configuración. Dependiendo de su distribución, el archivo es `/etc/smartd.conf` o `/etc/smartmontools/smartd.conf`.

Puede interactuar directamente con dispositivos SMART utilizando el comando `smartctl`. Para ver la información de un dispositivo individual, puede usar el comando `smartctl -i dispositivo`, donde dispositivo es el nombre de archivo del dispositivo. Aquí hay un ejemplo recortado del uso de este comando en una Distribución basada en Debian, que muestra una unidad conectada por USB sin capacidades SMART:

```sh
sudo smartctl -i /dev/sda1
[...]
Vendor:               Maxtor
Product:              OneTouch II
[...]
Device does not support SMART
```

No es necesario montar el dispositivo en el sistema para obtener su información SMART. Sólo es necesario conectarlo al sistema, lo que puede resultar útil.

Muchos discos duros tienen capacidades SMART. Aquí hay un ejemplo recortado del uso del comando `smartctl` en una distribución de Ubuntu, que muestra un disco duro antiguo que tiene capacidades SMART:

```sh
sudo smartctl -i /dev/sda6
[...]
=== START OF INFORMATION SECTION ===
Model Family:     Seagate Momentus 5400.6
[...] 
SMART support is: Available—device has SMART capability.
SMART support is: Enabled
```

Observe en el ejemplo anterior no solo que la unidad tiene capacidades SMART sino también que la compatibilidad SMART está habilitada. Si su disco no tiene habilitada la compatibilidad con SMART, puede habilitarla usando el comando `smartctl -s` en el dispositivo.

Puede realizar una serie de pruebas en su disco duro mediante la opción `-t` en el comando `smartctl`. La opción toma diferentes argumentos para determinar qué tipo de prueba realizar. Por ejemplo, puede realizar una prueba automática, corta o larga. Tanto la opción de autoprueba como la de prueba corta son bastante rápidas. La opción de prueba larga puede ser bastante larga, como se muestra en este ejemplo recortado:

```sh
sudo smartctl -t long /dev/sda6
[...]
=== START OF OFFLINE IMMEDIATE AND SELF-TEST SECTION ===
[...] 
Testing has begun.
Please wait 74 minutes for test to complete.
Test will complete after Fri Jan 22 12:44:10 2017 
Use smartctl -X to abort test.
```

En el ejemplo anterior, puede ver que la prueba tardará 74 minutos en completarse. ¡Algunos viajes pueden tardar incluso más! No se mostrará ningún resultado en su terminal cuando se complete la prueba. Sin embargo, puede verificar el progreso de la prueba, como se muestra aquí:

```sh
sudo smartctl -a /dev/sda6 | grep -A1 "Self-test execution"
Self-test execution status:  ( 249)Self-test routine in progress                                    
									90% of test remaining.
```

No deje que el término rutina de autoprueba del listado anterior le confunda. Todas las pruebas son autopruebas y la prueba larga es una autoprueba extendida.

Una vez realizada la prueba, puede ver los resultados utilizando el comando `smartctl -a dispositivo`. De hecho, puede utilizar este comando en cualquier momento para determinar el estado general actual de su disco. La opción `smartctl -a` muestra una gran cantidad de información. Por lo tanto, puede ser una buena idea redirigir la salida a un archivo o canalizarla a la utilidad less. Aquí se muestra un ejemplo recortado de este comando en una distribución de Ubuntu: