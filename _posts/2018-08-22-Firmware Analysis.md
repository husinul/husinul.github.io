---
layout: page
title:  "Firmware Analysis"
date:   2018-08-22 11:21:21 +0530
categories: ["Firmware"]
---
Intelligent dishwashers, smart factories, connected sensors and Wi-Fi fridges, these are only a few examples of everyday objects that now are connected to the Internet.
All these "brainless" objects have been upgraded to become Internet of Things devices and now they’re changing our lifestyle communicating with us at anytime and in any place.
As security experts have to face the challenge of testing the security of these devices in order to find their vulnerabilities before bad guys do.
At the same time, it is also important to make manufacturers and organizations aware of the security risks associated with this kind of devices.

This blog is written to do a brief overview of Firmware analysis , one of the IoT Testing approach.

**Firmware Analysis Methodology** – To analyze any firmware, there are two ways to do so – one is manual and other uses a tool. Manual Analysis consumes a lot of time, and due to time constraints often it is not possible to do a manual analysis. Thus, automated analysis of firmware comes in handy.

**Community Efforts and Tools**

There are many community efforts dedicated to reverse engineering of firmwares and embedded devices. Each of these efforts have a specific goal and thus the tools produces by those efforts are influenced by their main goals. We try to summarize in a comprehensive list the most used and visible efforts to date.

- **Binwalk**
Binwalk is a firmware analysis tool designed to assist in the analysis, extraction, and reverse engineering of firmware images and other binary blobs.

  [download it from here](https://github.com/ReFirmLabs/binwalk)

- **Firmware Mod Kit**
This kit is a collection of scripts and utilities to extract and rebuild linux based firmware images. This kit allows for easy deconstruction and reconstruction of firmware images for various embedded devices.

  [download it from here](https://github.com/rampageX/firmware-mod-kit)

- **Firmwalker** 
A simple bash script for searching the extracted or mounted firmware file system.

  [download it from here](https://github.com/craigz28/firmwalker)



**Preliminary Analysis**

The first thing to do in order to better understand an IoT device is to perform some preliminary analysis which consists in conducting the first recon on a new firmware we have never seen before.
The main goal here is to get an idea about the firmware architecture and if it is encrypted or not.

Firmware package will be analyzed and the file system will have to be unpacked and extracted.

This process can be summarized in the following steps:

1 **Identify the target device:** if you don’t know what device runs your firmware, additional analysis needs to be performed for example with an internet search.

2 **Understand if a firmware is encrypted or compressed:**

use **strings** against the firmware, and if there are no strings in the output the file is probably obfuscated. 
launch **hexdump** with the “-C” argument which provides some context for the strings. 
use **Radare** with “izz” command to search for non-ASCII characters i.e. Unicode-encoded strings.

3 **Identify firmware architecture and FS:** Binwalk is useful to examine and extract binary files so launch it against the firmware without any argument in order to gain useful information about it.

4. **Extract the Filesystem:** once the filesystem type has been identified (i.e. Squashfs, Cramfs, YAFFS2 and so on) the next steps are:

- extract it from the firmware 
- mount it in order to access the data inside. According to the filesystem type of your device, it is possible to use different tools like dd, binwalk or fmk to extract the fylesystem.

Below it is provided an example of a preliminary analysis performed with binwalk and regarding Dlink DIR-412 Firmware

first start with strings
**strings -n 10 “file.bin”**

![strings](/assets/img/afterstrings.jpg)

and later move to hexdump

**hexdump -C -n 512 xyz.bin**

![hexdump](/assets/img/hexdump.png)

Run Binwalk to extract the firmware
![firmware](/assets/img/binwalk.png)

the files in the extracted firmware is shown
![out_firmware](/assets/img/binwalk_extracted.png)

Once the file has been extracted run Firmwalker as shown below –
![firmwalker](/assets/img/firmwalker.png)


The Firwalker tool is basically a bash script capable of identifying following issues –

- etc/shadow and etc/passwd
- list out the etc/ssl directory
- search for SSL related files such as .pem, .crt, etc.
- search for configuration files
- look for script files
- search for other .bin files
- look for keywords such as admin, password, remote, etc.
- search for common web servers used on IoT devices
- search for common binaries such as ssh, tftp, dropbear, etc.
- search for URLs, email addresses, and IP addresses
- Experimental support for making calls to the Shodan API using the Shodan CLI

Below are the few things we can get through Firmwalker

IP Address embedded into the firmware
![firmwalker_ip](/assets/img/firmwalker_ip.png)

Passwords
![firmwaler_pass](/assets/img/firmware_telnet.png)

going after Telnet
![telnet](/assets/img/telnet.png)

It seems it is related to telnet login. here we found username Alphanetworks,and the password is being loaded from the variable image_sign.
![telnet_log](/assets/img/telnet2.png)

checking password
![passwd](/assets/img/passwd.png)


Now, we have the username and the password; we can easily login over the telnet connection. The worst part is all the devices running the firmware are vulnerable and can be compromised.

Thus, Firmwalker is a great tool for scanning and finding the issues in an IoT Firmware
