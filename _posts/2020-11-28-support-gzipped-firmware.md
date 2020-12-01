---
title: "Support for Gzipped Firmware"
last_modified_at: 2020-11-28
excerpt_separator: "<!--more-->"
categories:
  - blog
tags:
  - Feature
  - Firmware
  - Gzip
---

If you use the Arduino Core library for ESP8266 devices you can now upload Gzipped firmware directly to Deploy the Fleet. <!--more-->

When you initially create your project you decide on a size for the OTA partition in flash memory. The size of this partition will depend on how large your firmware is and whether or not you need a SPIFFS or LittleFS file partition. Common OTA partition sizes are 512K and 1MB. Firmware updates for your devices must fit in the available OTA partition space. Gzipping your firmware binary before uploading it to Deploy the Fleet helps ensure the update will fit in the OTA partition.

Even if you don't need to compress your firmware to make it fit in the OTA partition it's a good idea to gzip the binaries anyway since this reduces the download size of the firmware delivered to your devices. This saves time and data usage.

<i class='fas fa-info-circle'></i> **IMPORTANT:** Deploy the Fleet can not validate that your firmware binary will fit in your device's OTA partition. You should validate this prior to uploading the firmware. The Arduino Core library will fail and skip any update that is too large to fit in the OTA partition.
{: .notice--warning}

## Possible Feature Addition
We are considering adding a feature that allows you to upload raw binaries and request Deploy the Fleet gzip them for you automatically. If you are interested in this feature please [up-vote it here](https://github.com/deploythefleet/website/issues/3).