# Capaccino

![capaccino_render3](https://github.com/APSP-AG/capaccino-public/assets/72441261/abb2da1d-3be5-44ca-9d4e-bc8f306ff6d1)



## Introduction

Welcome to the GitHub Wiki for Capaccino. This repository serves as a comprehensive guide and reference for this tool, designed to assist with real-time data visualization, configuration, logging, and data retrieval. It is intended for developers, hobbyists, or anyone interested in sensor data management and analysis.


## Table of Contents
* [Introduction](#introduction)
  + [Project Overview](#project-overview)
  + [Key Features](#key-features)
* [Getting Started](#getting-started)
  + [Connection](#connection)
    - [Boot Behavior and Default Mode](#boot-behavior-and-default-mode)
    - [Access Point (AP) Mode](#access-point-ap-mode)
      * [How to Connect:](#how-to-connect)
      * [Network Credentials:](#network-credentials)
    - [Client Mode](#client-mode)
      * [How to Connect:](#how-to-connect-1)
      * [Browser Access Options:](#browser-access-options)
    - [Alternative Connection via Serial Command](#alternative-connection-via-serial-command)
* [Data Logging & Visualization](#data-logging--visualization)
  + [Dashboard Overview](#dashboard-overview)
    - [Data Storage and CSV Download](#data-storage-and-csv-download)
  + [Setting Logging Frequency](#setting-logging-frequency)
  + [Retrieving Logs](#retrieving-logs)
* [CDC Configuration Interface](#cdc-configuration-interface)
  + [Adjusting Device Parameters](#adjusting-device-parameters)
    - [How to Adjust](#how-to-adjust)
* [OTA Firmware Upgrades](#ota-firmware-upgrades)
  + [What is OTA?](#what-is-ota)
  + [One-Click Update Procedure](#one-click-update-procedure)
* [Troubleshooting](#troubleshooting)
  + [Common Issues and Fixes](#common-issues-and-fixes)
* [Support](#support)
  + [Reporting Bugs](#reporting-bugs)
  + [Feature Requests](#feature-requests)
  + [General Questions](#general-questions)

### Project Overview

Capaccino is designed to manage and visualize sensor data through a web-based dashboard. The tool aims to simplify tasks like device configuration and data logging, which often require manual coding or separate software. By integrating these functions into a single interface, Capaccino aims to streamline the process of sensor data management for a variety of applications.

---

### Key Features

- 📊 **Real-time Visualization:**  
The web-based dashboard displays sensor readings in real-time, providing immediate feedback and allowing for effective monitoring of various data points.

- ⚙️ **Configuration Interface:**  
The web interface allows users to adjust device parameters directly, negating the need to modify the source code for simple configuration changes.
  
- 💾 **Data Logging:**  
Users have the option to create logs based on sensor data. The logging frequency can be adjusted as needed, offering flexibility in data capture for later analysis.

- 📡 **Easy Connection:**  
Capaccino supports both WiFi Access Point (AP) and client modes, enabling easy integration into existing networks or standalone operation.

- 🔄 **OTA Firmware Upgrades:**  
Over-The-Air (OTA) firmware upgrades are supported, allowing for straightforward updates to add features or address bugs.


---

## Getting Started

Since the entire project runs on an embedded web server on the ESP32, there's no traditional installation required. Instead, you'll access Capaccino's features through a web browser. Below are the steps and tips for a smooth first-time experience.
### Connection

#### Introduction

Capaccino offers flexible connection options, operating either in **Access Point (AP) Mode** or **Client Mode**. By default, the device attempts to connect as a client to a pre-configured network upon boot. If unsuccessful, it automatically switches to AP Mode.

---

#### Boot Behavior and Default Mode

Upon booting, the device tries to establish a connection as a client to the stored WiFi network. It will make several attempts to connect. If these attempts are unsuccessful, the device automatically falls back to AP Mode to allow direct connections.

---

#### Access Point (AP) Mode

##### How to Connect:

1. **Enable WiFi on your device** and look for available networks.
2. **Select `Capaccino` from the list** of available WiFi networks.
3. **Enter the password `LetMeInPlease`** to connect.
4. **Open a web browser** and go to `http://192.168.4.1`.

##### Network Credentials:

- **SSID:** ``Capaccino``
- **Password:** ``LetMeInPlease``
- **IP Address (AP):** ``192.168.4.1``

> [!NOTE]
> **Performance Consideration:** AP Mode connections might experience slight delays as some operating systems check for internet availability and time out when they don't find any.

---

#### Client Mode

##### How to Connect:

1. **Initially, connect to Capaccino in AP Mode**.
2. **Navigate to the WiFi Configuration section** on the Capaccino dashboard.
3. **Enter your network's SSID and password** to configure the device for Client Mode.
4. **Save the settings and reboot the device** to apply the changes.

##### Browser Access Options:

You have three ways to access the Capaccino dashboard in a web browser after connecting in Client Mode:

1. `http://capaccino/`
2. `http://capaccino.local/`  
   > **Note for Windows Users:** To resolve `.local` domain names, you may need to download and install [Bonjour drivers](https://support.apple.com/kb/dl999?locale=en_US).
3. `http://[local_ip]/`  
   *(The local IP address will be displayed when you are in AP Mode)*

> [!WARNING]
> **Logs are Context-Sensitive:** Logs are only persistent when accessed via the same URL. Switching between URLs may result in a loss of log data.


#### Alternative Connection via Serial Command

If you're unable to connect through the above methods or prefer a more direct approach, you can set network credentials via a serial command. Use the Arduino terminal at a serial speed of 115200 and send the following command:
```
set_credentials(your_ssid,your_password)
```

This will set the SSID and password for Client Mode.

---

## Data Logging & Visualization

### Dashboard Overview

The Dashboard is your central hub for real-time data visualization. It offers an easy-to-understand interface, complete with charts and download options. To access this feature, navigate to the "Log" section in the sidebar.

#### Data Storage and CSV Download

- **Local Storage:** Every data point received from the sensors is stored locally in a browser-based database. This data is persistent between sessions.
- **CSV Export:** Clicking the "Download" button will loop through all stored data points and export them into a CSV file. 
- **Database Clearance:** The "Clear" button will erase all stored data points in the local database.

> [!WARNING]
> **CDC Parameter Caveats:** The CDC parameters are not stored with individual data points. When you download the CSV file, the CDC parameters are gathered and assumed to be the same across all data points. They will reflect the state that is active at the time of download.

### Setting Logging Frequency

To adjust how often data is logged:

1. Navigate to "Configure" in the sidebar.
2. Select the "Logging" subsection.
3. Here, you can adjust the frequency settings as per your requirements.

### Retrieving Logs

Retrieving logs is straightforward:

- **CSV File:** Click the "Download" button in the "Log" section to generate a CSV file. 
  - **Note:** While generating the CSV is usually fast, it might take longer if the database contains a large number of data points (e.g., in the millions).

---
## CDC Configuration Interface

### Adjusting Device Parameters

In the Capaccino interface, you'll find several options for configuring the CDC (Capacitive-to-Digital Converter). Each option controls a specific aspect of how the CDC behaves, affecting the precision, speed, and type of measurements you get. Below is a breakdown of these options:

- **Reference**: This setting establishes a baseline or "starting point" for measuring changes in capacitance. Imagine it as setting zero on a scale before weighing something. It helps the system know what to consider as the "normal" state.

- **Offset**: This acts like the tare function on a digital scale, allowing you to account for existing, or "parasitic," capacitance in the system. By doing so, you effectively "zero" the sensor, making sure that subsequent readings only measure the changes in capacitance that you are interested in. This is crucial in applications where absolute accuracy is needed.

- **Resolution**: Think of this as the sensor's sensitivity level. A high resolution will detect even very tiny changes in capacitance but might be more susceptible to noise or errors. A low resolution is less sensitive but more stable. 14-bit is recommended here.

- **Multiplier:** This determines the range of values the sensor can detect and how quickly it takes those measurements. Higher settings expand the range but may reduce the measurement's precision.

- **Differential Mode**: This setting dictates the configuration of your sensor system. In 'single-ended' mode, you are measuring the capacitance between the sensor and a fixed reference point, typically the ground. This is simpler but may be more susceptible to external noise. In 'differential' mode, the system measures the difference in capacitance between two sensors, which often results in more accurate readings by canceling out common-mode noise or interference affecting both sensors.

In practice, the key is to select the 'Multiplier', 'Reference', and 'Offset' parameters in such a way that maximizes the number of counts yielded by the digital conversion within the range of capacitance values you're interested in. 

> [!IMPORTANT]
> The reference tables in the datasheet are very useful for setting the correct CDC parameters. A link to the relevant pages of the datasheet is available in the sidebar of the UI.

#### How to Adjust

1. Navigate to the CDC Configuration Interface in the sidebar.
2. Select the appropriate values from the dropdowns or input fields.
3. Save your settings to apply changes.

> [!NOTE]
> It's important to choose the settings carefully to optimize sensor performance. Incorrect settings can produce readings that appear accurate but are actually invalid. 

> [!WARNING]
> The CDC input range should be adjusted experimentally with your actual setup to achieve optimal results. Make sure to validate your configuration.

---

## OTA Firmware Upgrades

### What is OTA?

OTA stands for Over-The-Air, a method of distributing updates to devices wirelessly rather than requiring a physical connection (like a USB cable). This feature in Capaccino allows you to seamlessly update both the device firmware and server files stored on the filesystem. The device automatically checks this GitHub repository for new releases and notifies you if an update is available.

### One-Click Update Procedure

Updating your Capaccino device is made simple with our one-click update feature. Follow the steps below to keep your device up-to-date:

1. **Navigate to the Configuration Section:**  
Go to "Config" in the sidebar of the web dashboard.

2. **Access Firmware Updates:**  
Click on the "Firmware" subsection to view your current firmware version and check for available updates.

3. **Check for Updates:**  
If there's a new version, you'll see an "Update" button.

4. **Initiate Update:**  
Click the "Update" button to start the firmware upgrade process.

5. **Wait for Update to Complete:**  
After initiating the update, it will take approximately 2 minutes for the process to complete. During this time, it's important not to turn off or disconnect the device.

> [!Note]
> The update procedure fetches the latest release from this GitHub repository, which includes both firmware and server files. Make sure you have a stable internet connection before initiating an update.


---

## Troubleshooting

### Common Issues and Fixes

<!-- List of common issues and their solutions. -->


---

## Support

If you encounter any issues, have suggestions for improvements, or would like to request new features, your input is more than welcome.

### Reporting Bugs

If you discover a bug:

1. **Create a New Issue:**  
Open a new issue in this GitHub repository. Please be as detailed as possible when describing the bug. Clearly outline the steps required to reproduce the issue.

2. **Attach Logs or Screenshots:**  
Additional information like logs or screenshots can be very helpful and can expedite the resolution process.

### Feature Requests

If you have an idea for a new feature or an enhancement:

1. **Create a New Issue:**  
Open a new issue and tag it as 'Feature Request'. Provide a comprehensive description of the feature you'd like to see, explaining its value and any implementation ideas you might have.

### General Questions

For general questions that are not directly related to bugs or feature requests, please create a post in the discussions section of this repository.


