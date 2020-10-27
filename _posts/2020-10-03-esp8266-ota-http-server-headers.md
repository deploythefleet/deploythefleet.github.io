---
title: "Correct ESP8266 OTA HTTP Server Headers"
excerpt_separator: "<!--more-->"
categories:
  - blog
tags:
  - ESP8266
  - Technical
  - OTA
  - HTTPS
---

If you are using the Arduino Core libraries in your ESP8266 library and want to do OTA updates using the [HTTP Server method](https://arduino-esp8266.readthedocs.io/en/latest/ota_updates/readme.html#http-server) you may have run into issues with the server sample code or noticed something off with the headers. 

<!--more-->

We ran into a similar problem enabling ESP8266 support in Deploy the Fleet. As of this writing (October 2020) the docs list the following example header data which will be sent to your server when the device checks for a firmware update.

```
[HTTP_USER_AGENT] => ESP8266-http-Update
[HTTP_X_ESP8266_STA_MAC] => 18:FE:AA:AA:AA:AA
[HTTP_X_ESP8266_AP_MAC] => 1A:FE:AA:AA:AA:AA
[HTTP_X_ESP8266_FREE_SPACE] => 671744
[HTTP_X_ESP8266_SKETCH_SIZE] => 373940
[HTTP_X_ESP8266_SKETCH_MD5] => a56f8ef78a0bebd812f62067daf1408a
[HTTP_X_ESP8266_CHIP_SIZE] => 4194304
[HTTP_X_ESP8266_SDK_VERSION] => 1.3.0
[HTTP_X_ESP8266_VERSION] => DOOR-7-g14f53a19
```

The problem is, those aren't the actual headers sent. If we look at the [code](https://github.com/esp8266/Arduino/blob/70e4457041eeb723033fc8011f3d724245d004ae/libraries/ESP8266httpUpdate/src/ESP8266httpUpdate.cpp#L262) we find the headers have been updated and better named in my opinion. Here is the actual list:

```yaml
User-Agent: ESP8266-http-Update
x-ESP8266-STA-MAC: [STA MAC]
x-ESP8266-AP-MAC: [AP MAC]
x-ESP8266-free-space: [free space on device]
x-ESP8266-sketch-size: [size of current sketch]
x-ESP8266-sketch-md5: [MD5 of current sketch]
x-ESP8266-chip-size: [flash size of device in bytes]
x-ESP8266-sdk-version: [current SDK version]
x-ESP8266-mode: [spiffs or sketch]
x-ESP8266-version: [value of version string passed to update call]
```

The biggest change is that all of the headers have been slightly renamed. Using the proper `User-Agent` header instead of a custom one is a good change. Unfortunately it was not documented. Also not documented is the addition of the `x-ESP8266-mode` header which will always be `sketch` unless you specifically call the `ESP8266HTTPUpdate::updateSpiffs` or `ESP8266HTTPUpdate::updateFS` functions.

This also means the accompanying PHP sample code is also incorrect in the documentation as it references the old header names.

One of the amazing things about open source is that we have the ability to improve the documentation by submitting PRs to the repo.

  - [PR #7633 to Update Documentation](https://github.com/esp8266/Arduino/pull/7633)
  - [Issue #7634 Filed on Repo](https://github.com/esp8266/Arduino/issues/7634)

Until it is approved and merged I hope this blog post can help someone else who may be stuck wondering why their customer HTTP server code is not working with their ESP8266 project.
