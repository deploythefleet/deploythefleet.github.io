---
title: "Why I Built Deploy the Fleet"
last_modified_at: 2020-11-24
excerpt_separator: "<!--more-->"
categories:
  - blog
---

## My First Product
Like most makers I never really had a pressing need to update a device over-the-air. If it had a bug or I developed a new feature I'd just grab the programmer or USB cable, plug it in and, ta-da, new firmware loaded. It wasn't until I created my first customer facing product that I realized just how essential updates are and how incredibly simple the process has to be. Customers don't even read the thirty word Getting Started guide you spent hours simplifying for them. So you can forget about having them open a terminal to run an update or, even worse, trying to install drivers so your update-over-USB will work on their Windows XP machine. I learned very quickly that getting updates to customers works best when the customer is minimally involved. 

  > I was spending more time working on the OTA code than the actual core device code.

Pretty soon I found while many MCUs support some form of OTA update you're mostly left to your own devices (pun intended) to make it work seamlessly with the rest of your code. I was spending dozens of hours implementing, testing, bug fixing and tweaking firmware code to make sure updates were simple, secure, and wouldn't brick my customer's devices. I was spending more time working on the OTA code than the actual core device code.

## Migrating to Espressif
After about a year of development on my product I had to migrate to an ESP32 chip as the brain of my product. I designed my firmware to be platform-agnostic. Within an evening I had my entire firmware running on an ESP32 development board. Every aspect except one: OTA updates. My previous MCU had a platform-specific way of doing OTA updates that I had to program around and there was no clear migration path.

## Hours Turned to Days Turned to....Months
Getting a simple OTA update working with an ESP8266 or ESP32 is actually quite simple. I had it working within a few additional hours. However, a few-hour lift doesn't get you very far. I was still missing things which are an absolute must for a product OTA solution. Things like HTTPS, versioning, and a place to store and monitor things. One idea led to another and another. Hours turned to days. Days turned to weeks and weeks turned to months as I spent nights and weekends implementing new features and thinking about how to make the OTA process easier.

## Just Getting Started
I built Deploy the Fleet to solve my own problem of complicated firmware update management. I've poured a lot of love and hard work into building it with the central purpose of making OTA updates easy for product makers. I believe updates are a crucial part of any product's success but shouldn't require more effort to get right than your core business logic. The service as it exists today is just the beginning. I have so many ideas to improve and expand it to make it useful for product creators. I'd love to have you along for the journey and to help make it the best firmware management solution available.