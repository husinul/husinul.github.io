---
layout: page
title:  "How to Create Backoors in IoT Devices"
date:   2018-09-02 03:18:21 +0530
categories: ["IoT"]
---
Warning: The author takes no responsibility for any damage you may cause to your device. 
This post is meant for educational purposes and strictly NOT for malicious purposes.

This post is all about modifying your existing router firmware to perform cool things by creating a backdoor using bindshell.    

Hardware and Tools Needed:

For the router, I am using a Dlink DIR-300. 
You may use whatever router you like but make sure you won’t brick your device after or while uploading the modified firmware.
Also make sure your firmware can be reversed and dumped using the FMK (Firmware Mod Kit).

#### AIM :
 Need to  add a netcat listner to Dlink_firmware

#### Requirements:
- Should automatically start  at boot up.
- Need to write and compile code for MIPS architecture

At first examine firmware using Binwalk you will get lots of useful information 
such as headers, sections, compressions used, etc.

![image1](/assets/img/binwalk.png)

going through the extracted firmware and exploring the filesystem of your router like this

![image2](/assets/img/3.png)

**For making a malicious code start at system boot**

- find scripts which executed when device starts
- focus on scripts which run as root
- /etc/init.d is a important place for start looking
- finding scripts which start other services such as ssh or telnet

for our purpose /etc/init.d is good, inside /etc/init.d edit the following script

```nano /etc/scripts/system.h```  by adding bindshell location on to it.

![image3](/assets/img/9.png)

write a simple C backdoor and compile it using GCC for MIPS

- for this we are using C backdoor bindshell written by Osanda Malith
 (https://github.com/OsandaMalith/TP-Link/blob/master/bindshell.c)

![image4](/assets/img/12.png)

- for this purposes we are using buildroot-2015.11.1
- copy  the bindshell to this location
- Compile using the GCC cross compiler for the MIPS architecture.

![image5](/assets/img/15.png)

After that we can place this shell inside the “etc/templates/” directory and change the startup script to run our shell after booting

![image6]](/assets/img/)

After your modifications are done use this bash script inside the fmk directory and build the firmware

```./build-firmware.sh Dlink_firmware.bin/ -nopad -min``` 

![image7](/assets/img/22.png)

using fat.py emulate the firmware

![image8](/assets/img/26.png)

![image](/assets/img/30.png)

![image17](/assets/img/31.png)

finally netcat listener

![image9](/assets/img/34.png)

root access to the router

![image10](/assets/img/35.png)

![image11](/assets/img/37.png)

![image12](/assets/img/38.png)

Pwned

![image13](/assets/img/39.png)
