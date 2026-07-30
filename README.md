# Wi-Fi Traffic Analysis with Monitor Mode and Tshark

A practical wireless-networking project focused on capturing and analysing raw IEEE 802.11 traffic in Linux using monitor mode, Wireshark, and Tshark.

## Project overview

The project examines Wi-Fi communication below the IP layer. By switching a compatible wireless adapter from managed mode to monitor mode, it becomes possible to inspect management, control, and data frames transmitted over the air.

## What the project demonstrates

- configuration of a wireless interface in monitor mode
- capture of raw IEEE 802.11 frames
- analysis of management, control, and data traffic
- extraction of timestamps, MAC addresses, sequence numbers, and signal strength
- study of probe requests and beacon frames
- command-line packet processing with Tshark
- basic device and vendor analysis using MAC-address prefixes

## Technologies and tools

- Linux
- Wireshark
- Tshark
- Aircrack-ng tools
- IEEE 802.11
- monitor-mode compatible Wi-Fi adapter
- command-line data extraction

## Managed mode versus monitor mode

| Mode | What is visible |
|---|---|
| Managed mode | Traffic processed for the connected device, often presented as Ethernet frames |
| Monitor mode | Raw 802.11 traffic on the selected wireless channel, including management and control frames |

Monitor mode is therefore required when the purpose is to inspect Wi-Fi behaviour at Layer 2 rather than only analyse the device's own network traffic.

## Experimental workflow

### 1. Identify the wireless interface

```bash
iw dev
```

### 2. Enable monitor mode

A common approach with Aircrack-ng is:

```bash
sudo airmon-ng check kill
sudo airmon-ng start <interface>
```

The command may create a monitor interface such as `<interface>mon`.

> Replace `<interface>` with the actual wireless interface name. Enabling monitor mode can temporarily disconnect normal Wi-Fi connectivity.

### 3. Capture traffic

Traffic can be captured graphically with Wireshark or from the terminal with Tshark:

```bash
sudo tshark -i <monitor-interface>
```

Generate controlled traffic, such as ICMP echo requests, while capturing packets so that data frames can be compared with surrounding wireless activity.

### 4. Filter frame categories

Useful Wireshark display filters include:

```text
wlan.fc.type == 0
```

Management frames:

```text
wlan.fc.type == 1
```

Control frames:

```text
wlan.fc.type == 2
```

Data frames:

```text
wlan.fc.type_subtype == 4
```

Probe requests:

```text
wlan.fc.type_subtype == 8
```

Beacon frames.

### 5. Extract fields with Tshark

Example command:

```bash
sudo tshark -i <monitor-interface> \
  -T fields \
  -e frame.time_epoch \
  -e wlan.sa \
  -e wlan.da \
  -e wlan.seq \
  -e radiotap.dbm_antsignal
```

The output can be redirected to a text or CSV file for later analysis.

## Frame types analysed

### Management frames

These coordinate Wi-Fi discovery and association. Examples include:

- beacon frames
- probe requests
- probe responses
- authentication and association frames

### Control frames

These support reliable access to the wireless medium. ACK frames are a common example.

### Data frames

These carry user traffic, such as ICMP packets generated during a ping experiment.

## Main observations

- raw 802.11 headers are visible only when the capture setup exposes link-layer Wi-Fi frames
- beacon frames advertise network information such as SSID and supported capabilities
- probe requests reveal active network discovery by nearby devices
- sequence numbers help track frame transmission order
- signal strength varies with distance, obstacles, antenna placement, and radio conditions
- MAC-address prefixes can support vendor identification, although address randomisation may limit device attribution

## Responsible-use note

Wireless captures may contain identifiers and traffic belonging to other devices. Perform experiments only in authorised environments, minimise retained data, and avoid publishing sensitive packet captures or personally identifiable information.

## Skills demonstrated

- IEEE 802.11 protocol analysis
- monitor-mode configuration
- Wireshark filtering
- Tshark automation
- Layer 2 troubleshooting
- wireless signal interpretation
- structured extraction of packet metadata
- responsible handling of network-capture data

## Academic context

This repository documents practical wireless-network analysis completed at Politecnico di Torino. It is intended as a technical portfolio project and a reproducible reference for monitor-mode capture and IEEE 802.11 frame analysis.
