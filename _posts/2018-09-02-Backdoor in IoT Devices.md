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

[!image1](/assets/img/)

going through the extracted firmware and exploring the filesystem of your router like this
[!image2](/assets/img/)
