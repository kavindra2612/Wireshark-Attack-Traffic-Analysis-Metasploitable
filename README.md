## 🛡️ Wireshark Attack Traffic Analysis – Metasploitable
## 📌 Project Summary

This project demonstrates network traffic analysis in a controlled lab environment using Wireshark.

Reconnaissance traffic was generated against a vulnerable Metasploitable machine using Nmap. The objective was to analyze how scanning activity appears at the packet level and identify early-stage reconnaissance behavior from a SOC analyst perspective.

## 🧪 Lab Environment

Attacker: Kali Linux (192.168.139.x)

Target: Metasploitable (192.168.139.x)

Network: VMware NAT (192.168.139.0/24)

Packet Capture Tool: Wireshark

## 🔍 Key Traffic Analysis Findings
## 1️⃣ TCP 3-Way Handshake
![TCP 3-Way Handshake](Screenshots/3%20way%20Handshak.png)


Observed:

SYN → SYN-ACK → ACK sequence

Successful connection establishment

Normal TCP session initialization

Analysis:
This confirms active service availability and successful connection establishment during the scanning phase.

## 2️⃣ TCP Connect Scan Behavior
![TCP Connect Scan](./Screenshots/TCP scan.png)

Observed:

Multiple sequential port connections

Full TCP handshake completed for each port

Ports scanned: 22, 25, 80, 110, 139, 445, 3306

Analysis:
This behavior is consistent with a TCP Connect scan (nmap -sT). High-frequency connection attempts across multiple ports indicate reconnaissance activity.

SOC Indicators:

Multiple short-lived TCP sessions

Sequential port probing

Elevated connection volume within a short time window

## 3️⃣ UDP Scan with ICMP Port Unreachable
![UDP Scan](./Screenshots/udp_scan.png)

Observed:

UDP probes sent to multiple ports

ICMP Type 3 Code 3 (Port Unreachable) responses

Analysis:
Closed UDP ports generate ICMP “Destination Unreachable – Port Unreachable” responses. This pattern confirms UDP scanning behavior.

SOC Indicators:

Multiple UDP packets with varying destination ports

ICMP error responses originating from the target

## 📊 Additional Traffic Observed

Additional protocol analysis (available in the /Screenshots folder):

ARP resolution (local host discovery)

DNS queries and responses

TLS handshake (Client Hello / Server Hello)

TCP RST packets for closed ports

## 🛡️ Security Observations

Active reconnaissance detected

Port enumeration activity identified

Service discovery attempts observed

Mixed TCP and UDP scanning techniques

Clear indicators of early-stage attack lifecycle

## Skills Demonstrated

Packet-level traffic analysis

Strong TCP/IP protocol understanding

ARP and DNS traffic inspection

TCP Connect scan identification

UDP scan detection

ICMP response analysis

Reconnaissance detection methodology

SOC-style investigative documentation

## Conclusion

This project demonstrates how reconnaissance and port scanning activity can be identified through packet-level analysis. By examining TCP handshakes, UDP probes, and ICMP responses, it is possible to detect early-stage attack behavior before exploitation occurs.
