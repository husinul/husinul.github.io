---
layout: page
title:  "Firmware 101"
date:   2018-05-18 03:11:21 +0530
categories: ["Firmware"]
---



Hello today let's discuss about firmwares

**Firmware**

The term ”firmware” has been coined by Ascher Opler in a 1967 Datamation article. His definition of firmware as a glue microcode layer between the CPU instruction set and the actual hardware has since been superseded.

IEEE Standard Glossary of Software Engineering Terminology, Std 610.12-1990, defines firmware today as follows:

The combination of a hardware device and computer instructions and data that reside as readonly software on that device.

Here is a non-exhaustive list of all the domains that use firmware-driven devices:

• Networking – Routers, Switches, NAS, VoIP phones
• Surveillance – Alarms, Cameras, CCTV, DVRs, NVRs
• Industry Automation – PLCs, Power Plants, Industrial Process Monitoring and Automation
• Home Automation – Sensoring, Smart Homes, Z-Waves,Philips Hue
• Whiteware – Washing Machine, Fridge, Dryer
• Entertainment gear – TV, DVRs, Receiver, Stereo, Game Console, MP3 Player, Camera, Mobile Phone, Toys
• Other Devices - Hard Drives, Printers
• Cars
• Medical Devices

**Common Processor Architectures**

LOW END:

MSP430
8051
ATMEL AVR

HIGH END:

ARM
Intel ATOM
MIPS
Motorola 6800/68000 (68k)
Ambarella

**Common Buses**

• Serial buses - SPI, I2C, 1-Wire, UART
• PCI, PCIExpress
• AMBA

**Common Communication Lines**

• Ethernet - RJ45
• RS485
• CAN/FlexRay
• Bluetooth
• WIFI
• Infrared
• Zigbee
• Other radios (ISM-Band, etc/)
• GPRS/UMTS
• USB

**Common Directly Addressable Memory**

• DRAM
• SRAM
• ROM
• Memory-Mapped NOR Flash

**Common Storage**

• NAND Flash
• SD Card
• Hard Drive

**Common Operating Systems**

• Linux -Perhaps most favourite and most encoutered
• VxWorks
• Cisco IOS
• Windows CE/NT
• L4
• eCos
• DOS
• Symbian
• JunOS
• Ambarella

**Common Bootloaders**

• U-Boot
• Perhaps most favourite and most encoutered
• RedBoot
• BareBox
• Ubicom bootloader
• OpenFirmware

**Common Libraries and Dev Envs**

• busybox + uClibc
• Perhaps most favourite and most encoutered
• buildroot
• openembedded
• crosstool
• crossdev

**Firmware Formats – Typical Objects Inside **

• Bootloader (1st/2nd stage)
• Kernel
• File-system images
• User-land binaries
• Resources and support files
• Web-server/web-interface

**Firmware Formats – Packing Category View I**
 Pure filesystems:
 
• YAFFS
• JFFS2
• SquashFS
• CramFS
• ROMFS
• UbiFS
• xFAT
• NTFS
• extNfs

**Firmware Formats – Packing Category View II**

Pure archives

• CPIO
• Ar
• Tar
• GZip
• Bzip2
• LZxxx
• RPM/DEB

Pure binary formats
• iHEX
• SREC/S19,ELF


Hybrids (any breed of above)

