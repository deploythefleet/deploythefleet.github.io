---
title: "Managing Devices"
permalink: /docs/manage-devices/
last_modified_at: 2020-10-23
toc: true
toc_icon: clipboard-list
toc_sticky: true
classes: wide
---

## Create a Device
Devices are created automatically in Deploy the Fleet any time a device uses your product-specific update URL. 

## Update a Device
Each time a device connects to Deploy the Fleet the Last Check-In time is updated as well as the Reported Version of the firmware. At a minimum a device must send two pieces of information to the update endpoint.

  - Device ID
  - Current Firmware Version

See the Quick Start guides for examples of how this data is sent to Deploy the Fleet.

### Generic URL
The Device ID and Firmware Version can be reported via the update URL endpoint with query parameters as follows:

| Value            | Query Param | Example            |
|------------------|-------------|--------------------|
| Device ID        | did         | ?did=b89f3df8-bdd9 |
| Firmware Version | v           | ?v=1.2.0           |

#### Example

```txt
https://deploythefleet.io/api/ota/58e60a43-4e22-4652-8efa-4e92973a8736?v=[VERSION]&did=[DEVICE ID]
```

## Delete a Device
Currently there is no way to delete a device. If this is a feature you need please request it using the Feedback dialog within the app.