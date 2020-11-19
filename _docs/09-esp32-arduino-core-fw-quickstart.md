---
title: "ESP32 Arduino Core Quick Start"
permalink: /docs/quick-start/esp32/arduino-core/
last_modified_at: 2020-11-11
toc: true
toc_label: "ESP32 Quick Start"
toc_sticky: true
---

The following instructions should work for any development board or module that can run the [ESP32 Arduino Core library](https://github.com/espressif/arduino-esp32). If your project uses the Arduino Core library the steps below illustrate how to modify your firmware so your devices connect to Deploy the Fleet for updates.

## Video Walkthrough

<div class="responsive-video-container">
<iframe id="lbry-iframe" width="800" height="450" src="https://lbry.tv/$/embed/dtf-esp32-quickstart/cb789329b8bf72718c377002a61247e2b78cc86e?r=FMmfD3i3a3LWW4n5arB65GwERbZDqgyE" allowfullscreen></iframe>
</div>

## Sample Project
If you already have a project or product using the Arduino Core library you can skip this section. If you are starting from scratch this section will walk you through getting a sample project ready for integration with Deploy the Fleet.

Before continuing, follow the ESP32 Arduino Core instructions for [installing the library](https://github.com/espressif/arduino-esp32#installation-instructions) if you haven't already done so.


  1. Launch the Arduino IDE
  1. From the _Tools->Board->ESP32 Arduino_ menu select the appropriate board for your hardware.
  1. Create a new sketch with the following contents

      ```cpp
      #include <WiFi.h>
      #include <WiFiMulti.h>

      #define WIFI_SSID     "[YOUR WIFI SSID]"
      #define WIFI_PASSWORD "[YOUR WIFI PASSWORD]"
      String CURRENT_VERSION = "1.0.0";

      WiFiMulti WiFiMulti;

      void setup() {
        Serial.begin(115200);
        Serial.println("Deploy the Fleet ESP32 Example");

        for (uint8_t t = 4; t > 0; t--) {
          Serial.printf("[SETUP] WAIT %d...\n", t);
          Serial.flush();
          delay(1000);
        }

        WiFi.mode(WIFI_STA);
        WiFiMulti.addAP(WIFI_SSID, WIFI_PASSWORD);
      }

      void loop() {
        // wait for WiFi connection
        if ((WiFiMulti.run() == WL_CONNECTED)) {
          Serial.println("This is version " + CURRENT_VERSION);
          delay(5000);
        }
      }
      ```

  1. Replace _[YOUR WIFI SSID]_ with your actual WiFi network SSID name.
  1. Replace _[YOUR WIFI PASSWORD]_ with your actual WiFi password.
  1. Compile the project by clicking the **Verify** button or using the **Ctrl-R** keyboard shortcut.
  1. Connect your hardware.
  1. Upload the firmware by clicking the **Upload** button or using the **Ctrl-U** keyboard shortcut.
  1. Open the Serial Monitor and set the baud rate to **115200**
  1. You should see output similar to the following

      ![serial output of sample v1 program](/assets/images/docs/serial_out_v1.png)

The sample project is a very simple firmware that repeatedly outputs the current version over serial. You are now ready to modify your project to use Deploy the Fleet as the update service.

## Integrate With Deploy the Fleet

In this section you will modify your existing firmware which will allow you to manage updates via Deploy the Fleet going forward.

### Install the DTF_ESP8266Update Library

To make the integration as easy as possible we created an Arduino library. It can be installed from the built-in Arduino library manager or by importing a zip file.

#### Using Library Manager (recommended)

  1. From the _Sketch_ menu select _Include Library->Manage Libraries_. The Library Manager dialog will open
  1. In the filter field enter "DTF" to filter the results
  1. Install the latest version of the DTF_ESP32Update library.

  ![Arduino IDE Library Manager dialog](/assets/images/docs/arduino_library_manager.png)

#### Import ZIP File

  1. Download the latest released zip file from [https://github.com/deploythefleet/arduino_esp32_update/releases](https://github.com/deploythefleet/arduino_esp32_update/releases)
  1. From the _Sketch_ menu select _Include Library->Add .ZIP Library_
  1. Navigate to the location where you saved the ZIP file in step 1, select it, and click **OK**.

### Updates from Deploy the Fleet

As a trivial example we'll have the firmware check for an update as soon as it is connected to the network. Depending on your firmware and use case you could trigger the firmware update process with the press of a button or some other event that contextually makes sense. 

Make sure the library header is included at the top of your sketch file.

```cpp
#include <DTF_ESP32Update.h>
```

If you are using the sample project we just created replace your `loop` function with the following code. Make sure you replace `DTF_UPDATE_URL` with the URL found on your Deploy the Fleet dashboard.

```cpp
void loop() {
  static bool checkedForUpdates = false;

  // wait for WiFi connection
  if ((WiFiMulti.run() == WL_CONNECTED)) {
    if (!checkedForUpdates)
    {
      checkedForUpdates = true;
      DTF_ESP32Update::getFirmwareUpdate(DTF_UPDATE_URL, CURRENT_VERSION.c_str());
    }
    Serial.println("This is version " + CURRENT_VERSION);
    delay(5000);
  }
}
```

If instead you are integrating Deploy the Fleet with an existing project all you need to do is add the following line of code wherever you would like the update process to occur.

```cpp
DTF_ESP32Update::getFirmwareUpdate("YOUR DTF UPDATE URL", "CURRENT VERSION i.e. 1.0.0");
```

<i class='fas fa-info-circle'></i> **IMPORTANT:** Make sure you replace the URL and firmware version placeholders in the above code with your own values. The update URL can be found on the [main dashboard](/docs/dashboard/) for your product.
{: .notice--info}

### Export Firmware From Arduino IDE
Before you can upload your firmware to Deploy the Fleet you need to export it from the Arduino IDE.

  1. Compile the project by clicking the **Verify** button or using the **Ctrl-R** keyboard shortcut.
  1. Export the firmware binary using the menu _Sketch->Export compiled Binary_ or using the **Ctrl-Alt-S** keyboard shortcut.

Your firmware binary will be exported to the same folder where your sketch is located.

### Upload Firmware to your Device
Now that you've made your firmware Deploy the Fleet aware upload it to your device.

  1. Upload the modified firmware by clicking the **Upload** button or using the **Ctrl-U** keyboard shortcut.

### Upload Firmware to Deploy the Fleet

  1. Open Deploy the Fleet.
  1. [Create a product](/docs/manage-products/#create-a-product) if you don't already have one.
  1. Navigate to the Firmware page.
  1. Click **Upload A New Firmware**
  1. Select the firmware binary
  1. Set the version to the same value used in the firmware code. In our example we set it as 1.0.0 but you may have set it differently for your project.
  1. Optionally add any release notes
  1. Click **Upload**
    
      ![ESP32 Quickstart firmware upload dialog](/assets/images/docs/esp32_quickstart_fw_upload_dialog.png)

Since this is the first firmware for your product it will automatically be marked as the default.

## Your First Update

Now that everything in your firmware is configured let's create an update.

  1. Modify the `CURRENT_VERSION` variable to be **2.0.0**.
  1. Compile the project by clicking the **Verify** button or using the **Ctrl-R** keyboard shortcut.
  1. Export the firmware binary using the menu _Sketch->Export compiled Binary_ or using the **Ctrl-Alt-S** keyboard shortcut.
  1. Open Deploy the Fleet.
  1. Navigate to the Firmware page.
  1. Click **Upload A New Firmware**
  1. Select the newly created firmware binary
  1. Set the version to 2.0.0.
  1. Select **Mark as product default**
  1. Optionally add any release notes
  1. Click **Upload**
  1. Reset your device

Your device should update and start outputting the new message indicating it is running version 2.0.0.