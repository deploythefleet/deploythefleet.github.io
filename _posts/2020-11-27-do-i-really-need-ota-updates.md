---
title: "Do I Really Need OTA Updates?"
last_modified_at: 2020-11-27
excerpt_separator: "<!--more-->"
tagline: Deciding which update approach is best for your product
layout: single
header:
  overlay_image: /assets/images/connected_city.jpg
  overlay_filter: 0.4
  show_overlay_excerpt: false
  og_image: /assets/images/connected_city.jpg
categories:
  - blog
tags:
  - Business
  - Information
  - OTA
---

Since the dawn of the Internet of Things there has been a seemingly endless wave of change. Platforms come and go, protocols come and go and even the tech stack is in a constant state of flux. But since the moment I programmed my first 8-bit PIC microcontroller I have learned there is one constant which will follow you from maker project to shipping products to customers; you have to get the ones and zeros programmed onto your devices. Regardless of programming language, cloud services, communication protocols or even the MCU, your device is ultimately useless if you can't get your code onto it. <!--more-->

Delivering updates is a crucial product feature but it shouldn't be anywhere close to the most important one. It should be minimally used compared to the core function of your product and it must be dead simple. Ideally it shouldn't require the time of your customer. Any amount of friction usually means updates won't get installed which means your product will experience feature decay or worse, will become a security liability.

So it's safe to say firmware updates will likely be an essential part of your product's lifecycle. But do you really need them to be delivered over-the-air(OTA)? This post breaks down the pros and cons of each approach to help you better decide what's best for your product and, more importantly, your customers.

## The Case For Non-OTA Updates
With almost all modern devices being of the OTA-update variety why would you consider going the non-OTA route? Well, there are actually some very good reasons you might choose non-OTA updates. But first, what is considered a non-OTA update solution? These are things like updates over a USB cable, files on a thumb drive or SD card which a device reads or some other form of wired connection like RS-485 and CAN bus.

### Pros
The number one reason to consider using a non-OTA approach is security. While most modern OTA solutions use TLS transport security and other measures to deliver updates there are simply more attack vectors when an update is delivered over-the-air. End-to-end network security requires you to rely on everyone doing their part. Your users, their ISP, and the cloud provider. Not to mention the mechanism which delivers the updates. If your product requires extreme levels of security then OTA may introduce a level of risk you and your customers aren't comfortable accepting. Some examples are nuclear reactors, voting machines, critical infrastructure, medical equipment and security devices. 

Another possible advantage of non-OTA updates is simplicity. I say possible because you may find "simplicity" to be a relative term. More on that in a minute. The bottom line is non-OTA updates have less moving parts than OTA ones. Any time you bring a wireless protocol to the table you are adding a level of complexity and unreliability which you wouldn't otherwise have. Reducing the number of 3rd-party variables (ISP, home router, cloud provider) can be advantageous especially when it comes to troubleshooting issues with your customers.

Finally, the decision to use non-OTA updates may already be inherently made for you given the context of your device. If you are building an add-on component for a device which already has a non-OTA update mechanism built-in then introducing OTA as a one-off is probably a bad idea.

### Cons
So far it might sound like non-OTA updates are more-secure, more reliable and easier to troubleshoot. Why even consider OTA updates? You will find there are plenty of drawbacks to non-OTA updates the biggest of which is friction. With all of the above-mentioned benefits comes a great cost of making non-OTA updates virtually impossible to automate. A user will have to be involved in the process. As such it is more likely devices won't receive critical security patches and new features. 

Because of this update friction it is also likely you will have to support more versions of your firmware, specifically older ones. Without a way to automatically roll out new firmware updates your customers will naturally be running many different versions of your firmware. This will incur extra support costs. 

I mentioned simplicity as a possible benefit of non-OTA updates. Simplicity is in the eye of the beholder. If a user has to open a terminal prompt to run an update over a USB cable you may find "simple" to you is rocket science to a customer. Regardless of how simple you think your update process is the real test is whether your customer agrees with you. It works fine on your development laptop but what happens when a user tries to run an update on a Windows XP machine that doesn't have the FTDI drivers needed to make things work smoothly. You've traded troubleshooting a network connection for troubleshooting an operating system.

Finally, with a non-OTA approach you must consider how to get updates to your customer. This fact makes most non-OTA approaches somewhat OTA in nature. Your customer needs to get the updated firmware somehow. Unless you mail them a thumb drive or SD card they are probably getting the update via an email or downloading it from your website. Distribution of updates is an additional problem you'll need to solve.

### Non-OTA Summary
Despite what some IoT purists will tell you there are indeed times when a non-OTA approach to updates is exactly what your product requires.

#### Pros
  - Added security. Reduces the possibility of man-in-the-middle attacks and other attack vectors
  - Not a lot of moving parts to go wrong
  - Simple to manage firmware updates from a business-perspective

### Cons
  - Higher friction for customers
  - Virtually impossible to automate
  - Can lead to feature decay
  - Higher support costs

## The Case for OTA Updates
When the Internet of Things really started to pick up steam in the 20-teens over-the-air updates became ubiquitous. Almost every smart device you own receives updates wirelessly. Televisions, smart speakers, doorbells, thermostats, and even juicers 😉. This has become an MVP-level feature for many IoT devices. These updates can be delivered via any one of a multitude of communication channels such as TCP (HTTP and UDP), Bluetooth, BLE, LoRaWAN, and even cellular.

### Pros
OTA updates have a lot of benefits. Not just for your business but for your customers as well. The biggest advantage of OTA updates, in my opinion, is their ability to be automated and seamless to the customer. If done correctly, OTA updates are delivered to customers without any interaction on their part. This ensures devices receive important security patches, bug fixes, and feature updates. 

While OTA updates rely on variables outside of your control such as home networks, ISPs and cloud providers, the web is essentially a solved problem and "just works". Even if customer interaction is required most users know how to navigate basic web-related tasks and instructions. This is in stark contrast to managing device drivers or having to enter commands via a terminal shell.

OTA updates generally lower support costs especially if the updates are automated and have logic to handle rollbacks and failure retries. The step of distributing the firmware update can be automated as well.

Finally, OTA updates are well suited for advanced fleet management and telemetry. New versions of firmware can be released in controlled, predictably ways such as with [ring-based deployments](https://opensource.com/article/18/2/feature-flags-ring-deployment-model). It is much easier to know what firmware versions have been delivered to which devices giving you greater insight into the health and status of your fleet.

### Cons
OTA updates are not without drawbacks. First and foremost is the added complexity they introduce. OTA updates are meant to be effortless for customers which usually means your business has gone to great lengths to create a polished abstraction layer. Firmwares must be stored somewhere and made available 24/7. Tracking versions, ensuring secure delivery and storage of binaries, and hosting are all things your business must handle. Solutions like Deploy the Fleet help mitigate almost all of these. 

OTA updates can certainly be done securely but their very nature introduces additional security issues which are out of your control. You can implement every security best practice only to have your end user run the device on an insecure, compromised network. If OTA updates are compromised an attacker could theoretically run malicious code on your devices. This is a great reminder to use firmware signing whenever possible.

Finally, I stated earlier the internet normally "just works". This is true but when it doesn't, it REALLY doesn't. Getting an OTA update through a 15 year old router set up by a self-proclaimed network expert is a real adventure. Be prepared to become an expert network support technician.

### OTA Summary
The IoT device industry largely prefers the OTA method of delivering firmware updates. When done right they are secure and frictionless to customers while providing additional business insights not available with non-OTA approaches. Added complexity and support concerns must be addressed.

#### Pros
  - Seamless to customers
  - Easy to automate 
  - Keeps your devices patched and feature rich
  - Lower support costs
  - Can provide additional fleet insights

### Cons
  - Added complexity to manage
  - When it doesn't work it's hard to troubleshoot
  - Creates more attack vectors

## Wrap Up
At the end of the day the ability to update a device is just a feature of your product. You have to decide, before you ship a single unit, whether you want the ability to deliver firmware updates to the devices your customers purchase. The answer to this question is almost universally "yes". Hopefully this post has helped you consider both OTA and non-OTA options so you can pick the method that works best for your customers. If you choose the OTA route I'd be happy to show you how Deploy the Fleet can save you time and money.
