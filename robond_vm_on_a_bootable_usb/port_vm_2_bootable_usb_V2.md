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

