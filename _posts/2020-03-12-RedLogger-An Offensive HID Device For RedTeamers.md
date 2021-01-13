---
layout: page
title:  "RedLogger-An Offensive HID Device For RedTeamers"
date:   2020-01-09 13:21:45 +0530
categories: ["Research"]
---

RedLogger was born from the need for cheap and dedicated hardware that could be remotely controlled in order to conduct HID attacks.It is a cheap but reliable piece of hardware designed to fulfill Pentesters needs related to HID Attacks, during their engagements.

RedLogger v1.0 has in build wifi capability with web app interface with **Remote keylogger, Live Payload executor**.

![image1](/assets/img/Redlogger1.png)

![image1](/assets/img/Redlogger1.1.png)


The core of RedLogger is mainly an **Atmega 32u4** (commonly used in many Arduino boards) and an **ESP-12s** (which provides the WiFi capabilities and is commonly used in IoT projects).

![image1](/assets/img/Redlogger2.jpg)

However, in coming days, a new hardware is under R&D (i.e. **RedLogger X**). It replaces the Wi-Fi capabilities with a 2G baseband and 4G LTE. Which extends its wireless capabilities to (potentially) an unlimited working range.The increased range has made it possible to add mobile phone-like additional capabilities to the hacking tool. This includes GPS location tracking and acoustic surveillance – a command sent to RedLogger X will turn on its microphone and relay eavesdropped audio back to the attacker

![image1](/assets/img/Redlogger3.jpg)

