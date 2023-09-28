# Capaccino GitHub Wiki

![drawing2](https://github.com/APSP-AG/capaccino-public/assets/72441261/67944aeb-196d-4319-8650-049a388afa8c)

## Introduction

Welcome to the GitHub Wiki for Capaccino. This repository serves as a comprehensive guide and reference for this tool, designed to assist with real-time data visualization, configuration, logging, and data retrieval. It is intended for developers, hobbyists, or anyone interested in sensor data management and analysis.


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

### Installation Guide

<!-- Step-by-step guide on how to install the project. -->


---
## Connection

### Introduction

Capaccino offers flexible connection options, operating either in **Access Point (AP) Mode** or **Client Mode**. By default, the device attempts to connect as a client to a pre-configured network upon boot. If unsuccessful, it automatically switches to AP Mode.

---

### Boot Behavior and Default Mode

Upon booting, the device tries to establish a connection as a client to the stored WiFi network. It will make several attempts to connect. If these attempts are unsuccessful, the device automatically falls back to AP Mode to allow direct connections.

> [!NOTE]  
> Highlights information that users should take into account, even when skimming.

---

### Access Point (AP) Mode

#### How to Connect:

1. **Enable WiFi on your device** and look for available networks.
2. **Select `Capaccino` from the list** of available WiFi networks.
3. **Enter the password `LetMeInPlease`** to connect.
4. **Open a web browser** and go to `http://192.168.4.1`.

#### Network Credentials:

- **SSID:** ``Capaccino``
- **Password:** ``LetMeInPlease``
- **IP Address (AP): ** ``192.168.4.1``

> [!NOTE]
> **Performance Consideration:** AP Mode connections might experience slight delays as some operating systems check for internet availability and time out when they don't find any.



---

### Client Mode

#### How to Connect:

1. **Initially, connect to Capaccino in AP Mode**.
2. **Navigate to the WiFi Configuration section** on the Capaccino dashboard.
3. **Enter your network's SSID and password** to configure the device for Client Mode.
4. **Save the settings and reboot the device** to apply the changes.

#### Browser Access Options:

You have three ways to access the Capaccino dashboard in a web browser after connecting in Client Mode:

1. `http://capaccino/`
2. `http://capaccino.local/`  
   > **Note for Windows Users:** To resolve `.local` domain names, you may need to download and install [Bonjour drivers](https://support.apple.com/kb/dl999?locale=en_US).
3. `http://[local_ip]/`  
   *(The local IP address will be displayed when you are in AP Mode)*

> [!WARNING]
> **Logs are Context-Sensitive:** Logs are only persistent when accessed via the same URL. Switching between URLs may result in a loss of log data.


### Alternative Connection via Serial Command

If you're unable to connect through the above methods or prefer a more direct approach, you can set network credentials via a serial command. Use the Arduino terminal at a serial speed of 115200 and send the following command:
```
set_credentials(your_ssid,your_password)
```

This will set the SSID and password for Client Mode.





---

## Data Logging & Visualization

### Dashboard Overview

<!-- Screenshots and description of the dashboard. -->

#### Setting Logging Frequency

<!-- How to set the frequency for logging data. -->

### Retrieving Logs

<!-- Guide on how to retrieve the logged data. -->

---

## Configuration Interface

### Accessing the Web Interface

<!-- Information on how to access the web interface. -->

### Adjusting Device Parameters

<!-- How to adjust device parameters from the web interface. -->

### Use Cases

<!-- Examples or scenarios where adjusting device parameters is useful. -->

---

## OTA Firmware Upgrades

### What is OTA?

<!-- Explain the concept of Over-The-Air updates. -->

### One-Click Update Procedure

<!-- Step-by-step guide on how to perform one-click updates. -->

### Firmware Changelog

<!-- A changelog for the firmware versions. -->

---

## Troubleshooting

### Common Issues and Fixes

<!-- List of common issues and their solutions. -->

### Where to Ask for Help

<!-- Point users to forums, issue trackers, or other places where they can ask for help. -->

---

## Support

<!-- Details about how to get support for the project. -->

