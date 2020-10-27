---
title: "Initial Setup"
permalink: /docs/initial-setup/
last_modified_at: 2020-10-23
toc: false
classes: wide
---

## Create a Product

The first time you log in to Deploy the Fleet you will be prompted to create a product.

[IMAGE of product creation page]

After creating your product you will be taken to the main dashboard but things will look pretty empty. That's because Deploy the Fleet isn't very useful unless you've uploaded a firmware update for your devices to pull. What you will see, however, is a unique update URL endpoint for your product devices. You will need this URL to modify your existing firmware to point to Deploy the Fleet for updates.

## Prepare a New Firmware Version

You probably already have a firmware binary for your product but you don't want to upload that version to Deploy the Fleet. Your existing firmware doesn't contain code pointing to Deploy the Fleet for updates. Before you upload any firmware binaries you need to change your update code to point to Deploy the Fleet. We've made quick-start guides to make this change as simple as possible.

  - [ESP8266 Arduino Core](/docs/quick-start/esp8266/arduino-core/)
  - [ESP8266 ESP-IDF](/docs/quick-start/esp8266/idf/)
  - [ESP32 Arduino Core](/docs/quick-start/esp32/arduino-core/)
  - [ESP32 ESP-IDF](/docs/quick-start/esp32/idf/)

## Upload a Firmware Binary

At this point you are ready to [upload a firmware binary](/docs/manage-firmware#create) for your devices.

**WARNING:** Do **NOT** upload a firmware binary if it does not contain code to point your device to Deploy the Fleet for updates. This can result in devices no longer using the service.
{: .notice--danger}

## You're All Set

That's all there is to it. As soon as one of your devices requests an update it will show up on the [Devices View](/docs/device-view/). Any time you want to update devices simply [create a new version of the firmware](/docs/manage-firmware/#create) on the [Firmware View](/docs/firmware-view/) and set it as the default. It's that simple!