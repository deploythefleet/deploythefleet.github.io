---
title: "Firmware View"
permalink: /docs/firmware-view/
last_modified_at: 2020-10-23
toc: false
classes: wide
---

![image-center](/assets/images/docs/firmware_view.png){: .align-center}

The firmware page is where you manage your firmware binaries. From the firmware page you can:

  - Upload new firmware binaries
  - View which firmware versions are currently active
  - Set the default firmware for your product
  - View metadata of existing firmware versions

The firmware versions displayed on the firmware page are separated into two groups; active and inactive firmware. A firmware is considered active if it meets one or more of the following criteria:

  - It is marked as the product default firmware
  - At least one device currently reports using the firmware version
  - At least one device has been sent the firmware for update

If a firmware does not meet any of the above criteria is is considered inactive. Active firmware versions are shown at the top of the view in card format. The card displays the firmware version, how many devices are running the firmware, a digest of release notes and a visual indicator if it is the default firmware for the product.

![image-center](/assets/images/docs/default_fw_card.png){: .align-center}

When firmware versions go inactive they are displayed in a table below the active firmware cards.

Whether active or inactive, clicking on a firmware version will open a dialog showing information about the firmware version. From this dialog there are actions available such as making a firmware the default version for the product.

![image-center](/assets/images/docs/fw_create_dialog.png){: .align-center}