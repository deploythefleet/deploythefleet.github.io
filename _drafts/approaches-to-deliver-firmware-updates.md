---
title: "4 Approaches to Deliver Firmware Updates to Customers"
excerpt_separator: "<!--more-->"
categories:
  - blog
output: false
tags:
  - Technical
  - OTA
---

Programming Cable (USB to TTL)
Hard for customers, open to hijacking, very simple delivery.
Best for very low volume and technical user base or if you allow for custom firmware hacking.
Must make sure drivers work on all platforms, provide instructions

USB Cable
Drivers again and a bootloader
If customers aren't technical you will have to create and maintain a cross platform app that simplifies the process for them
Best if updates are infrequent and if the device can be easily put in range of computer. Requires a computer.

Bluetooth OTA
Some devices have BT or BLE. Need an app to communicate with your device. Still need a way to get the firmware to the device that will deliver it to the product. Must maintain an app

HTTP(S) OTA
Browser Method from ESP Arduino Core docs
Very clunky and again going to be very hard for anyone accept advanced users.

