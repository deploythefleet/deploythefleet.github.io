---
title: "Initial Setup"
permalink: /docs/initial-setup/
last_modified_at: 2020-10-23
toc: false
classes: wide
---

## Create a Product

The first time you log in to Deploy the Fleet you will be prompted to create a product.

![create product dialog](/assets/images/docs/create_product.png){: .align-center}

After creating your product you will be taken to the main dashboard but things will look pretty empty. That's because Deploy the Fleet isn't very useful unless you've uploaded a firmware update for your devices. What you will see, however, is a unique update URL endpoint for your product devices. You will need this URL to modify your existing firmware to point to Deploy the Fleet for updates.

![Update URL on main dashboard](/assets/images/docs/empty_dashboard.png){: .align-center}

## Prepare a New Firmware Version

You probably already have a firmware binary for your product but you don't want to upload that version to Deploy the Fleet. Your existing firmware doesn't contain code pointing to Deploy the Fleet for updates. Before you upload any firmware binaries you need to change your firmware update code to point to Deploy the Fleet. We've made several quick start guides to illustrate the changes required.

  - [ESP8266 Arduino Core](/docs/quick-start/esp8266/arduino-core/)
  - [ESP32 Arduino Core](/docs/quick-start/esp32/arduino-core/)

## Upload a Firmware Binary

Once you have a firmware binary that is Deploy the Fleet aware you are ready to [upload it](/docs/manage-firmware#create).

<i class='fas fa-exclamation-triangle'></i> **WARNING:** Do **NOT** upload a firmware binary if it does not contain code that points at Deploy the Fleet for updates. This can result in devices no longer using the service.
{: .notice--danger}

## You're All Set

That's all there is to it. As soon as one of your devices requests an update it will show up on the [Devices View](/docs/device-view/). Any time you want to update devices simply [create a new version of the firmware](/docs/manage-firmware/#create) on the [Firmware View](/docs/firmware-view/) and set it as the default. It's that simple!