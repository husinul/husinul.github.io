---
layout: page
title:  "Getting Started to Firmware Emulation for IoT  Devices"
date:   2018-08-27 08:46:21 +0530
categories: ["Firmware"]
---

In this Post, we will have a look at how we can perform Firmware Emulation of a given IoT device.

Firmware Emulation can serve a number of different purposes such as analyzing the firmware in a better way,
performing exploitation,
performing remote debugging and so on.

With this technique, you can emulate a Firmware originally meant to be run on a different architecture, and interact with it, 
even without having a physical IoT device.

One of the earlier ways of performing Firmware Emulation was to create a Qemu image and 
then copy the firmware file system's contents on to the Qemu image and then launch the image.

However, there exists a much simpler alternative which is also prone to give you lesser issues while emulating firmware. 
Let's have a look.

**Tools Required**

- Any Linux based Image or AttifyOS VM
- firmadyne
- A firmware that you want to emulate (for ex - Netgear WNAP320 )

**Setup Process**

First, clone this repository recursively and install its dependencies.

1. `sudo apt-get install busybox-static fakeroot git dmsetup kpartx netcat-openbsd nmap python-psycopg2 python3-psycopg2 snmp uml-utilities util-linux vlan`
2. `git clone --recursive https://github.com/firmadyne/firmadyne.git`

## Extractor

The extractor depends on the [binwalk](https://github.com/devttys0/binwalk)
tool, so we need to install that and its dependencies.

1. `git clone https://github.com/devttys0/binwalk.git`
2. `cd binwalk`
2. `sudo ./deps.sh`
3. `sudo python ./setup.py install`
  * For Python 2.x, `sudo apt-get install python-lzma`
4. `sudo -H pip install git+https://github.com/ahupp/python-magic`
5. `sudo -H pip install git+https://github.com/sviehb/jefferson`.
6. Optionally, instead of [upstream sasquatch](https://github.com/devttys0/sasquatch),
our [sasquatch fork](https://github.com/firmadyne/sasquatch) can be used to
prevent false positives by making errors fatal.

## Database

Next, install, set up, and configure the database.

1. `sudo apt-get install postgresql`
2. `sudo -u postgres createuser -P firmadyne`, with password `firmadyne`
3. `sudo -u postgres createdb -O firmadyne firmware`
4. `sudo -u postgres psql -d firmware < ./firmadyne/database/schema`

## Binaries

To download our pre-built binaries for all components, run the following script:

* `cd ./firmadyne; ./download.sh`

## Demo

**Emulating Firmware Image**

In order to emulate a firmware is run ./fat.py and specify the firmware name. In this case, we are running the WNAP320.zip firmware, so we will specify that.

For the Brand, you can specify any brand, as that is used for purely database purposes.

Your output should be as shown below:

![firmare2](/assets/img/firmadyne2.png)

next
![firmware3](/assets/img/firmadyne3.png)

next
![firmware4](/assets/img/firmadyne4.png)

Once it has completed the initial setup process for the firmware, it will provide you with an IP address. In case the firmware runs a web server, you should be able to access the web interface, as well as interact with the firmware over SSH and perform additional network based exploitation.

![firmware5](/assets/img/firmadyne5.png)

Let's now open up Firefox and see if we are able to access the web interface.

![firmware6](/assets/img/firmadyne6.png)

Acess Via Default Credentials

![firmware7](/assets/img/firmadyne7.png)

**Congratulations!!!** - we have successfully emulated a firmware (which was originally meant for MIPS Big Endian architecture) and even have the web server from within the firmware accessible!
