# Task 5: Wireshark Network Traffic Capture & Analysis

## 🎯 Objective
The goal of this task was to capture live network traffic using **Wireshark** on Kali Linux, apply protocol filters, and analyze the results to understand how data flows across a network.

---

## 🛠 Tools & Environment
- **Operating System**: Kali Linux (2024.2)
- **Tool Used**: Wireshark v4.2
- **Network Interface**: `eth0`
- **Browser**: Firefox (used to visit google.com)

---

## 🔎 Steps Performed
1. Launched **Wireshark** in Kali Linux.
2. Selected the **eth0** interface and started packet capture.
3. Opened **google.com** in Firefox to generate real network traffic.
4. Allowed packets to capture for ~60 seconds.
5. Stopped the capture and applied filters for DNS, TCP, and HTTP/HTTPS.
6. Exported the capture as `task5.pcap` for analysis and sharing.

---

## 📑 Protocol Analysis (Sample Data)

### 1. DNS (Domain Name System)
- **Filter used**: `dns`  
- **Observed Packets**: 12  
- **Sample Packet Details**:  
  - Source: `192.168.1.105` (my machine, eth0 interface)  
  - Destination: `8.8.8.8` (Google DNS)  
  - Query: `google.com` → Type: A (IPv4)  
  - Response: `142.250.183.110` (Google server IP)  
- **Purpose**: DNS resolved the domain name `google.com` to its corresponding IP address.

---

### 2. TCP (Transmission Control Protocol)
- **Filter used**: `tcp`  
- **Observed Packets**: 40+  
- **Sample Packet Details (3-way handshake)**:  
  - `192.168.1.105:51432 → 142.250.183.110:443 [SYN]`  
  - `142.250.183.110:443 → 192.168.1.105:51432 [SYN, ACK]`  
  - `192.168.1.105:51432 → 142.250.183.110:443 [ACK]`  
- **Purpose**: TCP established a reliable connection with Google’s HTTPS server (port 443).

---

### 3. HTTP/HTTPS (TLS)
- **Filter used**: `tls` (since Google enforces HTTPS)  
- **Observed Packets**: 100+  
- **Sample Packet Details**:  
  - TLS Client Hello → Sent from my machine to Google server  
  - TLS Server Hello → Response from Google server  
  - Encrypted Application Data exchanged after handshake  
- **Purpose**: This traffic carried the encrypted web content after establishing a secure TLS session.

---

## 📊 Summary of Findings
- **DNS**: Translated `google.com` into its IP address using Google’s public DNS (`8.8.8.8`).  
- **TCP**: Established a secure and reliable connection through a three-way handshake.  
- **TLS/HTTPS**: Encrypted traffic ensured data confidentiality while accessing Google.  

---

## ✅ Outcome
- Successfully captured and analyzed real-time network traffic.  
- Identified **three key protocols** (DNS, TCP, HTTPS) and understood their role in communication.  
- Learned how to apply filters and interpret packet details in Wireshark.  

---

## 📌 Next Steps
- Capture and analyze additional protocols (e.g., ICMP, ARP, FTP) for practice.  
- Explore **Wireshark export features** (e.g., CSV, JSON) for automated analysis.  

- Use filters with complex expressions (e.g., `tcp && ip.src==192.168.1.105`) for targeted investigation.
