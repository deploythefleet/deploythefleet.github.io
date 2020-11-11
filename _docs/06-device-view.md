---
title: "Device View"
permalink: /docs/device-view/
last_modified_at: 2020-10-23
toc: false
classes: wide
---

![Device view example](/assets/images/docs/device_view.png){: .align-center}

The device page contains a list of devices that have connected to Deploy the Fleet for firmware updates. They are automatically generated and updated as devices connect to the service. Each device is an entry in the device table containing the following information:

  - Device ID
  - Last Check-In
  - Reported Version

<i class='fas fa-info-circle'></i> The device list can be updated at any time by clicking the refresh icon next to the total device count.
{: .notice--info}

## Device ID
The ID a device reports in with when it connects to Deploy the Fleet. It is controlled by your firmware code and can be something like a MAC address or GUID. It must be globally unique to your product.

## Last Check-In
The date and time when the device last requested an update from Deploy the Fleet. Useful to see if devices are checking in as often as you expect.

## Reported Version
The version of firmware the device reported when it last checked in. If an update was delivered to the device it will be indicated in this column. The following is an example of a device that reported firmware version 2.0.0 and was sent version 2.0.1 when the device last checked in. 

![Example of Reported Version column](/assets/images/docs/reported_version_example.png){: .align-center}

The next time the device checks in it should report the new version which will be reflected in the device list.