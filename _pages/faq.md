---
title: "Frequently Asked Questions"
permalink: /docs/faq
last_modified_at: 2020-10-23
layout: single
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/masthead1a.jpg
toc: true
toc_label: "Questions"
toc_icon: "question-circle"
toc_sticky: true
---


## What devices are supported?

Deploy the Fleet currently supports ESP32 and ESP8266 devices and all custom derivatives. This includes support for ESP devices running the Arduino Core code. The service can also support any device that accepts firmware updates over HTTPS. If you have a specific question about device support [just reach out](/contact) and we can take a look.

## Why would I use this service?

As a maker or product creator your focus should be on writing your core firmware, not worrying about all the details that go into updating it. With Deploy the Fleet you get a complete web-based solution that allows you to manage new versions of firmware that your devices seamlessly receive. The service also offers device insights allowing you to monitor your devices.

Questions Deploy the Fleet can answer for you:

  - Where should I store my firmware binaries?
  - How do I make my updates available to all my deployed devices?
  - How many devices are running version X of my firmware?
  - How many versions of my firmware are currently running on different devices?
  - Has that device I shipped been set up yet by the customer?
  - When was the last time a particular device was updated?

## Is there a free tier?

Absolutely! The Maker Tier will always be free and does not require a credit card to get started.

## Do I have to modify my firmware to use the service?

For the ESP devices running FreeRTOS or Arduino Core there are minimal code changes required to connect your device to Deploy the Fleet. There is documentation to help you and usually it only takes a few minutes of copy/paste development to get started.
