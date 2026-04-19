# WiFi Traffic Analysis using Monitor Mode and Tshark

## 📌 Overview
This project focuses on capturing and analyzing raw IEEE 802.11 Wi-Fi frames using monitor mode in a Linux environment.

The goal is to understand wireless network behavior at a low level by inspecting management, control, and data frames directly from the air.

---

## 🎯 Objectives
- capture raw Wi-Fi traffic using monitor mode
- analyze IEEE 802.11 frames
- extract signal strength, MAC addresses and timestamps
- identify different frame types (management, control, data)
- analyze wireless activity patterns in real environments

---

## 🛠️ Technologies Used
- Linux
- Wireshark
- Tshark
- monitor mode configuration tools
- command-line packet analysis

---

## ✅ Main Experiments and Results

### 1. Traffic Capture without Monitor Mode
Initial packet capture was performed in managed mode.

Results:
- packets appeared as Ethernet frames
- only processed traffic was visible
- no access to Wi-Fi management or control frames

This confirmed that monitor mode is required for low-level wireless analysis :contentReference[oaicite:0]{index=0}

---

### 2. Monitor Mode Configuration
The wireless interface was switched to monitor mode.

This allowed:
- capturing raw IEEE 802.11 frames
- observing all wireless activity in the environment
- analyzing packets directly at Layer 2

---

### 3. Wi-Fi Frame Capture
Traffic was generated using ICMP (ping) and captured using Wireshark and Tshark.

Results:
- full 802.11 headers were visible
- MAC addresses, sequence numbers and frame control fields were accessible
- management and control frames became visible :contentReference[oaicite:1]{index=1}

---

### 4. Frame Type Analysis
Different types of Wi-Fi frames were identified:

- Management frames (beacons, probe requests)
- Control frames (ACK)
- Data frames (ICMP traffic)

Using Wireshark filters and coloring rules helped distinguish between these frame types.

---

### 5. Tshark-Based Data Extraction
Tshark was used to extract specific fields:

- timestamp
- source MAC
- destination MAC
- sequence number
- signal strength (dBm)

Output was structured in CSV-like format for further analysis :contentReference[oaicite:2]{index=2}

---

### 6. Probe Request Analysis
Probe request frames were captured and analyzed.

Key observations:
- devices broadcast probe requests to discover networks
- packets are sent to broadcast address (ff:ff:ff:ff:ff:ff)
- high number of probe requests indicates active scanning

---

### 7. Beacon Frame Analysis
Beacon frames were inspected in detail.

Extracted information included:
- SSID
- supported rates
- access point capabilities

This data is available only when capturing in monitor mode.

---

### 8. MAC Address Analysis
Captured MAC addresses were analyzed to identify devices.

Results:
- MAC addresses were grouped and counted
- vendor identification was performed using OUI
- example: detection of Apple devices in the network environment :contentReference[oaicite:3]{index=3}

---

## 📊 Example Results
- successful capture of raw 802.11 frames
- visibility of management and control frames
- detection of probe requests and beacon frames
- extraction of signal strength and timing information
- identification of active devices through MAC analysis

---

## 📂 Repository Contents
- Tshark capture script
- packet capture outputs
- Wireshark analysis
- processed data for traffic inspection
- project report with screenshots and results

---

## ▶️ How to Run

### Enable monitor mode
```bash
sudo airmon-ng start wlan0
