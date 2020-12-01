---
title: "Arduino Core OTA Partition Size and Gzipping"
last_modified_at: 2020-11-30
excerpt_separator: "<!--more-->"
layout: single
# header:
#   overlay_image: /assets/images/connected_city.jpg
#   overlay_filter: 0.4
#   show_overlay_excerpt: false
#   og_image: /assets/images/connected_city.jpg
categories:
  - blog
tags:
  - ESP8266
  - Technical
  - OTA
  - HTTPS
  - Gzip
---

When using the ESP Arduino Core library to flash updates for ESP8266 devices you must ensure you have a properly sized OTA partition. This article covers what the OTA partition is, how to set the size of the partition in the Arduino IDE, and how to gzip firmware binaries to ensure your updates will fit on that partition.<!--more-->

## What is the OTA Partition?

The flash memory on your ESP8266 device is partitioned similar to how you'd partition a hard drive on a computer. One partition holds your running application and the OTA partition is available to store a single firmware update. There are additional config partitions as well but those are beyond the scope of this article. Depending on your module you'll likely have 2M or 4M of _total_ flash memory. This memory is then sub-divided into the partitions mentioned. It looks something like this ([source](https://arduino-esp8266.readthedocs.io/en/latest/filesystem.html#flash-layout)):

```txt
|--------------|-------|---------------|--|--|--|--|--|
^              ^       ^               ^     ^
Sketch    OTA update   File system   EEPROM  WiFi config (SDK)
```

Depending on your application you may also have a file system partition as shown above. Remember, the OTA partition is only necessary if you want to support OTA firmware updates. If you don't, you can reclaim the space and extend the size of your main application partition.

<!-- <i class='fas fa-info-circle'></i> **ESP32 :** Make sure your configured OTA partition size is sufficient for the size of your firmware binary. Gzipping the exported binary will help ensure it fits. For more information on partition sizing and gzipping check out [our blog post on the topic.]()
{: .notice--info} -->


## Choose an OTA Partition Size

If you want to enable OTA firmware updates for your device you must have an OTA partition. The Arduino Core library downloads your firmware into that OTA partition. The bootloader then programs the firmware into the main application partition. Selecting the appropriate size for this partition isn't too difficult but requires knowing the answer to a few questions:

  - Do you need file system storage? If so, how much?
  - How much flash space does your compiled firmware need?

Once you have the answers to these questions you can select the proper OTA partition size that accommodates your app and file system needs. It must be large enough to hold at least a compressed version of your firmware (more on this below) but should also have some room to accept larger binaries as you add features and your firmware grows. 

## Set the Partition Size in the Arduino IDE

Setting the partition size in the Arduino IDE is very simple. Once you've selected the appropriate board for your device the _Tools_ menu will have an additional option like _Flash Size_ or _Partition Scheme_. Select the layout that has the OTA partition size you need.

![Select partition size](/assets/images/docs/partition_size.gif){: .align-center}

## Using Gzip to Compress an Update

The ESP8266 Arduino Core library utilizes the eboot bootloader which incorporates a Gzip decompressor. Therefore, if the binary stored in the OTA partition is compressed using Gzip it will know how to decompress it before writing the firmware to the application partition. You can read more about this capability [in the official Arduino Core docs](https://arduino-esp8266.readthedocs.io/en/latest/ota_updates/readme.html?highlight=gzip#compression).

This feature helps ensure you can fit firmware upgrades into the available space on the OTA partition. Even if you don't need the space it's still a good idea to compress your binary. This reduces the amount of data transferred to the device during an update which directly affects data usage and power consumption. To compress a firmware you must first export it from the Arduino IDE using the _Sketch->Export compiled Binary_ menu option.

![Export compiled binary](/assets/images/docs/export_compiled_binary.gif){: .align-center}

This will export your binary into the same folder which contains your sketch source code.

  1. Open a terminal window
  1. `cd` to the directory containing your exported binary
  1. Run the following command
      ```txt
      gzip -9 [your exported binary]
      ```
  1. Your compressed binary will be in the same folder as your sketch source code

The `-9` option to the `gzip` command specifies the compression level. It is the recommended level from the Arduino Core docs.