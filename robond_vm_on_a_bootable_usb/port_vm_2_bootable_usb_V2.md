# Guide to Port the RoboND VM to a Bootable USB drive V2

## Intro
This guide is simple and works on Windows, MacOS, and Ubuntu. If you have any trouble with this guide, I am `@robottrainer` on the [RoboND Slack][roboslack]

## Why do this?
Lot of classmates in RoboND are experiencing slow and laggy performance of Gazebo inside the VM.
Some of us tried to solve this by installing ROS natively on Ubuntu. However, it is a lot of steps and
only a few students were able to run the project succesfully.

The VM comes with all tools installed and setup perfectly to work out of the box.
Easiest way is to just take the VM and boot into it natively. This guide does exactly that.

## Requirements

1.  Download the [RoboND Virtual Machine image][robovm]
2.  A 32GB USB drive

## Overview

The RoboND VM comes in the form of a ".ova" file. This file can be loaded using the VMWare player.
Inside this ".ova" file is a ".vmdk" file that VMWare Player uses as storage.
The ".vmdk" file has the LUbuntu OS and all ROS software installed in it.

We can convert this ".vmdk" file (virtual storage) into a ".img" file which can be
written to a physical storage device such as an USB drive.

That's it. We can then connect this USB drive to a real computer and boot from it.

## Step-by-Step Guide

- [Windows](#windows)
- [MacOS](#macos)
- [Ubuntu](#ubuntu)

### Windows

1.  Unzip the file `RoboVM_V2.1.0.zip`

    - Download and install [7-Zip][7zip]
    - Right-click `RoboVM_V2.1.0.zip` and select `7-Zip` -> `Extract Here`

2.  Check the MD5 checksum for `Ubuntu 64-bit Robo V2.1.0.ova`. Make sure it is
   `95bfba89fbdac5f2c0a2be2ae186ddbb`

    - Open a `Cmd` window and goto the folder where `.ova` file is present and
      run the following command

    ```bash
    $ certutil -hashfile "Ubuntu 64-bit Robo V2.1.0.ova" MD5
    ```

3.  Extract `Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk` from the `.ova`

    - Right-click `Ubuntu 64-bit Robo V2.1.0.ova` and select `7-Zip` -> `Extract Here`

    If you want to be sure that `.vmdk` is extracted properly, check that SHA256 is
    `8e28c53471415a1fa6e9834c890462b93ab5f5bad30d839430f7f6cdffc34517`

    ```bash
    $ certutil -hashfile Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk SHA256
    ```

4.  Convert `.vmdk` to `.img`

    Download and install [Virtual Box][vbox].

    ```bash
    $ cd "C:\Program Files\Oracle\VirtualBox"
    $ VBoxManage clonehd --format RAW "C:\Robotic VM V2.1.0\Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk" "C:\Robotic VM V2.1.0\Ubuntu_64-bit_Robo_V2.1.0-disk1.img"
    ```

    You can double-check that your `.img` file is good by verifying the SHA256
    `8ee1dba28ad518dd8f9c9090363deb94404120829d54f72e63c97843f998ad79`

    ```bash
    $ cd "C:\Robotic VM V2.1.0"
    $ certutil -hashfile Ubuntu_64-bit_Robo_V2.1.0-disk1.img SHA256
    ```

5.  Create a Bootable USB drive using [Rufus][rufus]. Select `DD Image` instead of the default `ISO Image` and then select `Ubuntu_64-bit_Robo_V2.1.0-disk1.img` as source
    and `32GB` USB drive as destination.

### MacOS

1.  Unzip the file `RoboVM_V2.1.0.zip`

    ```bash
    $ unzip RoboVM_V2.1.0.zip
    ```

2.  Check the MD5 checksum for `Ubuntu 64-bit Robo V2.1.0.ova`. Make sure it is
   `95bfba89fbdac5f2c0a2be2ae186ddbb`

    ```bash
    $ cd Robotic\ VM\ V2.1.0
    $ md5 Ubuntu\ 64-bit\ Robo\ V2.1.0.ova
    ```

3.  Extract `Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk` from the `.ova`

    ```bash
    $ tar -xvf Ubuntu\ 64-bit\ Robo\ V2.1.0.ova
    ```

    If you want to be sure that `.vmdk` is extracted properly, check that SHA256 is
    `8e28c53471415a1fa6e9834c890462b93ab5f5bad30d839430f7f6cdffc34517`

    ```bash
    $ shasum -a 256 Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk
    ```

4.  Convert `.vmdk` to `.img`

    Download and install [Virtual Box][vbox].

    ```bash
    $ cd /Applications/VirtualBox.app/Contents/MacOS
    $ VBoxManage clonehd --format RAW ~/Robotic\ VM\ V2.1.0/Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk ~/Robotic\ VM\ V2.1.0/Ubuntu_64-bit_Robo_V2.1.0-disk1.img
    ```

    You can double-check that your `.img` file is good by verifying the SHA256
    `8ee1dba28ad518dd8f9c9090363deb94404120829d54f72e63c97843f998ad79`

    ```bash
    $ cd ~/Robotic\ VM\ V2.1.0/
    $ shasum -a 256 Ubuntu_64-bit_Robo_V2.1.0-disk1.img
    ```

5.  Create a Bootable USB drive using [Etcher][etcher]. Select the `Ubuntu_64-bit_Robo_V2.1.0-disk1.img` as source
    and `32GB` USB drive as destination.

### Ubuntu

1.  Unzip the file `RoboVM_V2.1.0.zip`

    ```bash
    $ unzip RoboVM_V2.1.0.zip
    ```

2.  Check the MD5 checksum for `Ubuntu 64-bit Robo V2.1.0.ova`. Make sure it is
   `95bfba89fbdac5f2c0a2be2ae186ddbb`

    ```bash
    $ cd Robotic\ VM\ V2.1.0
    $ md5sum Ubuntu\ 64-bit\ Robo\ V2.1.0.ova
    ```

3.  Extract `Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk` from the `.ova`

    ```bash
    $ tar -xvf Ubuntu\ 64-bit\ Robo\ V2.1.0.ova
    ```

    If you want to be sure that `.vmdk` is extracted properly, check that SHA256 is
    `8e28c53471415a1fa6e9834c890462b93ab5f5bad30d839430f7f6cdffc34517`

    ```bash
    $ sha256sum Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk
    ```

4.  Convert `.vmdk` to `.img`

    ```bash
    $ sudo apt install qemu-kvm
    $ qemu-img convert Ubuntu_64-bit_Robo_V2.1.0-disk1.vmdk -O raw Ubuntu_64-bit_Robo_V2.1.0-disk1.img
    ```

    You can double-check that your `.img` file is good by verifying the SHA256
    `8ee1dba28ad518dd8f9c9090363deb94404120829d54f72e63c97843f998ad79`

    ```bash
    $ sha256sum Ubuntu_64-bit_Robo_V2.1.0-disk1.img
    ```

5.  Create a Bootable USB drive using [Etcher][etcher]. Select the `Ubuntu_64-bit_Robo_V2.1.0-disk1.img` as source
    and `32GB` USB drive as destination.

    To install `Etcher` from a terminal

    ```bash
    $ wget https://github.com/resin-io/etcher/releases/download/v1.1.2/etcher-electron_1.1.2_amd64.deb
    $ sudo dpkg -i etcher-electron_1.1.2_amd64.deb
    $ etcher-electron
    ```

[vbox]: https://www.virtualbox.org/wiki/Downloads
[robovm]: https://s3-us-west-1.amazonaws.com/udacity-robotics/Virtual+Machines/Lubuntu_071917/RoboVM_V2.1.0.zip
[etcher]: https://etcher.io/
[rufus]: https://rufus.akeo.ie/
[7zip]: http://www.7-zip.org/download.html
[roboslack]: https://udacity-robotics.slack.com/


# Guide to Expand the root Partition on the RoboVM

Most of the time, the USB drive we used is larger than the size of the VM disk. In that case, we will be left with a large unused space and the root partition will only be ~16GB. This guide has step-by-step instructions to merge that unallocated space into the root partition. This might look long and scary but it is actually simple and it works perfectly.


## Overview

Following are the top-level changes we are going to perform.

1. Modify the Partition Table to utilize the unallocated space
  - Turn off the swap partition
  - Delete the swap(logical) partition
  - Delete the extended partition
  - Delete the root partition
  - Create a larger root partition
  - Create an extended partition at the end of the root partition
  - Create the swap(logical) partition
  - Set the type of the recently created swap partition to `Linux swap / Solaris`
  - Apply all changes
  - reboot
2. Resize the file system to make use of the extra space in the root partition
  - Resize the file system
  - Setup a new swapspace in the new swap partition
  - Turn on swap
  - Make sure swap partition is automatically mounted on every boot


## 1. Modify the Partition Table to utilize the unallocated space

**A note before we begin**
We are making changes to the partition table and if this goes wrong, we will loose all our data.
So, please backup important files. One good thing about `fdisk` is that no changes will get applied until we use the `w` command.
So, if we make a mistake, we can always use `q` to quit without making any permanent changes to the partition table.

We are going to use the commands `fdisk`, `swapon`, and `swapoff` in this section.
First, let's take a look at our partition table.

```bash
robond@udacity:~$ sudo fdisk /dev/sda

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 105775103 105773056 50.4G 83 Linux
/dev/sda2       105775104 122552319  16777216    8G  5 Extended
/dev/sda5       105777152 122552319  16775168    8G 82 Linux swap / Solaris

Command (m for help): m

Help:

  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition

  Misc
   m   print this menu
   u   change display/entry units
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit
   q   quit without saving changes

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table

Command (m for help): q
```

Once inside `fdisk`, Command `p` prints the partition table. `m` gives a list of usable commands and `q` is to quit `fdisk`.
What we need is the table at the end. In the example above we see a `50.4GB` root partition and `8.0GB` swap partition
but no unallocated space at the end. This is because I already resized my partitions.
So, for the sake of this guide we will increase the root partition by `4.0GB` and reduce the swap partition by the same amount.
The process is exactly the same if you have a smaller `16.0GB` root partition and some unallocated space at the end after
the swap partition.


### Turn off the swap partition

Check the current state of the swapspace using the following command.

```bash
robond@udacity:~$ sudo swapon -s
[sudo] password for robond:
Filename				Type		Size	Used	Priority
/dev/sda5                              	partition	4193276	0	-1
```

Turn swap off by specifying correct swap partition. `-v` is for verbose.

```bash
robond@udacity:~$ sudo swapoff -v /dev/sda5
swapoff /dev/sda5
```

If we check the status of swapspace now, we get nothing.

```bash
robond@udacity:~$ sudo swapon -s
robond@udacity:~$
```


### Delete all three partitions

We are going to complete all the following steps using `fdisk`. We are going to launch and stay with in `fdisk` to complete all the steps.

First, delete all existing partitions. When we print the partition table at the end, the list of partitions should be empty.

```bash
robond@udacity:~$ sudo fdisk /dev/sda

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 105775103 105773056 50.4G 83 Linux
/dev/sda2       105775104 122552319  16777216    8G  5 Extended
/dev/sda5       105777152 122552319  16775168    8G 82 Linux swap / Solaris

Command (m for help): d
Partition number (1,2,5, default 5): 5

Partition 5 has been deleted.

Command (m for help): d
Partition number (1,2, default 2):

Partition 2 has been deleted.

Command (m for help): d
Selected partition 1
Partition 1 has been deleted.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Command (m for help):
```

If we want to select the default option, we can just press enter. Now, without exiting `fdisk` we go to the next step.


### Create a larger root partition

Use command `n` to create new partitions. While creating partitions, we need to know a few things
like partition type, partition number, start sector, and end sector.

We need to do a bit of math for selecting start and end sectors.
A sector is 512 bytes (`fdisk` says this at the top). 1KB is 1024 bytes or 2 sectors. 1MB is 1024KB and 1GB is 1024MB.

Just select the start sector to be the default of 2048. We are going to select the end sector of the
root partition such that we leave just enough space at the end for our swap partition.

Here, I wanted 4GB for swap, which is 4 * 1024 * 1024 * 1024 / 512 = 8388608 sectors. The default last sector suggested is usually the maximum possible sector. If we subtract required number of swap sectors from the max sector, we get our end of the root partition. So, last sector of the root partition is 122552319 - 8388608 = 114163711

```bash
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-122552319, default 2048): 2048
Last sector, +sectors or +size{K,M,G,T,P} (2048-122552319, default 122552319): 114163711

Created a new partition 1 of type 'Linux' and of size 54.4 GiB.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot Start       End   Sectors  Size Id Type
/dev/sda1        2048 114163711 114161664 54.4G 83 Linux

Command (m for help):
```

Use the command `a` to set the root partition as bootable.

```bash
Command (m for help): a
Selected partition 1
The bootable flag on partition 1 is enabled now.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot Start       End   Sectors  Size Id Type
/dev/sda1  *     2048 114163711 114161664 54.4G 83 Linux

Command (m for help):
```


### Create an extended partition at the end of the root partition

Now, we need to create an extended partition and a logical partition inside it. Accept the default start and end sectors.

```bash
Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): e
Partition number (2-4, default 2): 2
First sector (114163712-122552319, default 114163712):
Last sector, +sectors or +size{K,M,G,T,P} (114163712-122552319, default 122552319):

Created a new partition 2 of type 'Extended' and of size 4 GiB.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 114163711 114161664 54.4G 83 Linux
/dev/sda2       114163712 122552319   8388608    4G  5 Extended

Command (m for help): n
All space for primary partitions is in use.
Adding logical partition 5
First sector (114165760-122552319, default 114165760):
Last sector, +sectors or +size{K,M,G,T,P} (114165760-122552319, default 122552319):

Created a new partition 5 of type 'Linux' and of size 4 GiB.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 114163711 114161664 54.4G 83 Linux
/dev/sda2       114163712 122552319   8388608    4G  5 Extended
/dev/sda5       114165760 122552319   8386560    4G 83 Linux

Command (m for help):
```


### Change the type of logical partition

We need to change the type of the swap partition to `Linux swap / Solaris`. We do that by using the `t` command.

```bash
Command (m for help): t
Partition number (1,2,5, default 5): 5
Partition type (type L to list all types): L

 0  Empty           24  NEC DOS         81  Minix / old Lin bf  Solaris
 1  FAT12           27  Hidden NTFS Win 82  Linux swap / So c1  DRDOS/sec (FAT-
 2  XENIX root      39  Plan 9          83  Linux           c4  DRDOS/sec (FAT-
 3  XENIX usr       3c  PartitionMagic  84  OS/2 hidden or  c6  DRDOS/sec (FAT-
 4  FAT16 <32M      40  Venix 80286     85  Linux extended  c7  Syrinx
 5  Extended        41  PPC PReP Boot   86  NTFS volume set da  Non-FS data
 6  FAT16           42  SFS             87  NTFS volume set db  CP/M / CTOS / .
 7  HPFS/NTFS/exFAT 4d  QNX4.x          88  Linux plaintext de  Dell Utility
 8  AIX             4e  QNX4.x 2nd part 8e  Linux LVM       df  BootIt
 9  AIX bootable    4f  QNX4.x 3rd part 93  Amoeba          e1  DOS access
 a  OS/2 Boot Manag 50  OnTrack DM      94  Amoeba BBT      e3  DOS R/O
 b  W95 FAT32       51  OnTrack DM6 Aux 9f  BSD/OS          e4  SpeedStor
 c  W95 FAT32 (LBA) 52  CP/M            a0  IBM Thinkpad hi ea  Rufus alignment
 e  W95 FAT16 (LBA) 53  OnTrack DM6 Aux a5  FreeBSD         eb  BeOS fs
 f  W95 Ext'd (LBA) 54  OnTrackDM6      a6  OpenBSD         ee  GPT
10  OPUS            55  EZ-Drive        a7  NeXTSTEP        ef  EFI (FAT-12/16/
11  Hidden FAT12    56  Golden Bow      a8  Darwin UFS      f0  Linux/PA-RISC b
12  Compaq diagnost 5c  Priam Edisk     a9  NetBSD          f1  SpeedStor
14  Hidden FAT16 <3 61  SpeedStor       ab  Darwin boot     f4  SpeedStor
16  Hidden FAT16    63  GNU HURD or Sys af  HFS / HFS+      f2  DOS secondary
17  Hidden HPFS/NTF 64  Novell Netware  b7  BSDI fs         fb  VMware VMFS
18  AST SmartSleep  65  Novell Netware  b8  BSDI swap       fc  VMware VMKCORE
1b  Hidden W95 FAT3 70  DiskSecure Mult bb  Boot Wizard hid fd  Linux raid auto
1c  Hidden W95 FAT3 75  PC/IX           bc  Acronis FAT32 L fe  LANstep
1e  Hidden W95 FAT1 80  Old Minix       be  Solaris boot    ff  BBT
Partition type (type L to list all types): 82

Changed type of partition 'Linux' to 'Linux swap / Solaris'.

Command (m for help): p
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 114163711 114161664 54.4G 83 Linux
/dev/sda2       114163712 122552319   8388608    4G  5 Extended
/dev/sda5       114165760 122552319   8386560    4G 82 Linux swap / Solaris

Command (m for help):
```


### Apply all changes

Make sure that the partition table looks exactly the way we want before permanently applying the changes.

```bash
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Re-reading the partition table failed.: Device or resource busy

The kernel still uses the old table. The new table will be used at the next reboot or after you run partprobe(8) or kpartx(8).

robond@udacity:~$
```


### Reboot

```bash
robond@udacity:~$ sudo reboot now
```


## 2. Resize the file system to make use of the extra space in the root partition

### Resize the file system

`df` is a program used to display free disk space in a filesystem. Below, on the `/dev/sda1`
line, we can see that the size of the partition used by the filesystem is still `50GB`.

```bash
robond@udacity:~$ sudo df -h
[sudo] password for robond:
Filesystem      Size  Used Avail Use% Mounted on
udev             16G     0   16G   0% /dev
tmpfs           3.2G  9.6M  3.2G   1% /run
/dev/sda1        50G   15G   34G  30% /
tmpfs            16G   20M   16G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs            16G     0   16G   0% /sys/fs/cgroup
tmpfs           3.2G   16K  3.2G   1% /run/user/1000
```

Let us confirm that the actual size of the `/dev/sda1` is `54.4GB` by using
`fdisk`.

```bash
robond@udacity:~$ sudo fdisk -l
Disk /dev/sda: 58.4 GiB, 62746787840 bytes, 122552320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x145df288

Device     Boot     Start       End   Sectors  Size Id Type
/dev/sda1  *         2048 114163711 114161664 54.4G 83 Linux
/dev/sda2       114163712 122552319   8388608    4G  5 Extended
/dev/sda5       114165760 122552319   8386560    4G 82 Linux swap / Solaris
```

The partition table looks exactly like we saved. Now, let's resize the
filesystem to use the entire partition.

```bash
robond@udacity:~$ sudo resize2fs /dev/sda1
resize2fs 1.42.13 (17-May-2015)
Filesystem at /dev/sda1 is mounted on /; on-line resizing required
old_desc_blocks = 4, new_desc_blocks = 4
The filesystem on /dev/sda1 is now 14270208 (4k) blocks long.

```

Run `df` again to check that the root partition is bigger.

```bash
robond@udacity:~$ sudo df -h
Filesystem      Size  Used Avail Use% Mounted on
udev             16G     0   16G   0% /dev
tmpfs           3.2G  9.6M  3.2G   1% /run
/dev/sda1        54G   15G   38G  28% /
tmpfs            16G   17M   16G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs            16G     0   16G   0% /sys/fs/cgroup
tmpfs           3.2G   16K  3.2G   1% /run/user/1000
```


### Setup a new swapspace in the new swap partition

`mkswap` creates a new swapspace. Make a note of the UUID of the swap
partition.

```bash
robond@udacity:~$ sudo mkswap /dev/sda5
Setting up swapspace version 1, size = 4 GiB (4293914624 bytes)
no label, UUID=db7be434-75e7-414e-bded-d86d836776b0
```


### Turn on swap

```bash
robond@udacity:~$ sudo swapon /dev/sda5
robond@udacity:~$ swapon -s
Filename				Type		Size	Used	Priority
/dev/sda5                              	partition	4193276	0	-1
```

We can use `swapon -s` to make sure swap is actually on.


### Make sure swap partition is automatically mounted on every boot

We need to make one more change to automatically activate the swap partition every time the
system reboots.

First, we need the UUID of the swap partition(the one we saved from the previous step). We can also
use `blkid` to get the UUID.

```bash
robond@udacity:~$ sudo blkid
/dev/sda1: UUID="88be6cf5-e738-4c37-a493-cfa5ba2b3e11" TYPE="ext4" PARTUUID="145df288-01"
/dev/sda5: UUID="db7be434-75e7-414e-bded-d86d836776b0" TYPE="swap" PARTUUID="145df288-05"
```

`/etc/fstab` should have the correct UUID for the swap partition for it to be
activated automatically. Let's check out our `/etc/fstab`.

```bash
robond@udacity:~$ sudo cat /etc/fstab
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda1 during installation
UUID=88be6cf5-e738-4c37-a493-cfa5ba2b3e11 /               ext4    errors=remount-ro 0       1
# swap was on /dev/sda5 during installation
UUID=db9caa61-9727-44b7-8479-87ee388c5e66 none            swap    sw              0       0
```

We need to replace the old UUID with the new UUID. Use `vi` or `gedit`.

```bash
robond@udacity:~$ sudo vi /etc/fstab
```

or

```bash
robond@udacity:~$ sudo gedit /etc/fstab
```

Here is my `/etc/fstab` with the correct UUID for the swap partition.

```bash
robond@udacity:~$ sudo cat /etc/fstab
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda1 during installation
UUID=88be6cf5-e738-4c37-a493-cfa5ba2b3e11 /               ext4    errors=remount-ro 0       1
# swap was on /dev/sda5 during installation
UUID=db7be434-75e7-414e-bded-d86d836776b0 none            swap    sw              0       0
robond@udacity:~$
```

Job done!

