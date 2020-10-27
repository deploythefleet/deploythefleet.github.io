---
title: "Device View"
permalink: /docs/device-view/
last_modified_at: 2020-10-23
toc: false
classes: wide
---

[IMAGE of device page]

The device page contains a list of devices that have connected to Deploy the Fleet for firmware updates. They are automatically generated and updated as devices connect to the service. Each device is an entry in the device table containing the following information:

  - Device ID
  - Last Check-In
  - Reported Version

The device list can be updated at any time by clicking the refresh icon next to the total device count.
{: .notice--info}

## Device ID
This is the ID the device reports in as when it connects to Deploy the Fleet. It is controlled by your firmware code and can be something like a MAC address or GUID. It must be globally unique to your product.

## Last Check-In
This is the date and time when the device last requested an update from Deploy the Fleet. It is useful to see if devices are checking in as often as you expect.

## Reported Version
This is the version of firmware the device reported when it last checked in. If an update was delivered to the device it will be indicated in this column. The following is an example of a device that reported firmware version X.X.X and was sent version Y.Y.Y. 

[IMAGE of device that is updating]

The next time the device checks in it should report the new version which will be reflected in the device list.

## Coming Soon
The following are device features we're currently working on.

  - **Device Audit Log** - A complete log of all device interactions with the service.
  - **Device Deactivation** - Used to prevent a device from getting future updates.
  - **Support Prediction** - Are devices checking in as often as you expect or have some gone offline. This can allow you to proactively reach out to customers if you suspect an issue.

Have other suggestions for features. Please send them to us using the _Feedback_ page within the app.