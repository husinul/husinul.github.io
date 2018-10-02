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

 
