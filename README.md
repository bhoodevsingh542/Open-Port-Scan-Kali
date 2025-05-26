🕵️‍♂️ Local Network Open Port Scan and Packet Capture Analysis

🎯 Objective
To perform a TCP SYN scan on the local network to identify active hosts and open ports, and analyze network traffic using Wireshark to understand communication at the packet level.

🛠️ Tools Used
🔍 Nmap 7.95
📡 Wireshark
🐧 Kali Linux

🌐 Network Details
Interface IP: 192.168.163.128/24 (wlan0)

Scan Command:
sudo nmap -sS -oN local-network-scan.txt 192.168.163.0/24

📋 Nmap Scan Results Summary

Nmap 7.95 scan initiated Mon May 26 21:01:59 2025 as: /usr/lib/nmap/nmap -sS -oN local-network-scan.txt 192.168.163.0/24

Nmap scan report for 192.168.163.165
Host is up (0.0052s latency).
Not shown: 999 closed tcp ports (reset)
PORT STATE SERVICE
53/tcp open domain
MAC Address: 62:DE:AB:58:8D:02 (Unknown)

Nmap scan report for 192.168.163.128
Host is up (0.0000050s latency).
Not shown: 999 closed tcp ports (reset)
PORT STATE SERVICE
21/tcp open ftp

Nmap done at Mon May 26 21:02:10 2025 -- 256 IP addresses (2 hosts up) scanned in 10.32 seconds

IP Address	Open Port	Service	Notes
192.168.163.165	53/tcp	DNS	Likely a DNS server or router
192.168.163.128	21/tcp	FTP	FTP service on Kali Linux

🔐 Analysis and Security Considerations

Port 53 (DNS):
DNS servers exposed on a network can be targets for abuse such as DNS amplification attacks. Ensure DNS services are restricted and monitored. ⚠️

Port 21 (FTP):
FTP transmits data unencrypted. If FTP is unnecessary, disable it or replace it with secure alternatives like SFTP or FTPS. 🔒

🕵️‍♀️ Wireshark Packet Capture Analysis

During the TCP SYN scan, a packet capture was recorded on the wlan0 interface. The file scan-capture.pcapng contains the network traffic generated during the scan.

Key Observations:
📨 SYN Packets: TCP SYN packets are sent from the scanning host (192.168.163.128) to multiple IPs within the subnet, probing ports.

✅ SYN-ACK Responses: Hosts with open ports respond with SYN-ACK packets, confirming their availability.

❌ RST Packets: Closed ports reply with TCP RST packets, rejecting connection attempts.

Wireshark Filters Applied:

Show SYN packets: tcp.flags.syn == 1 && tcp.flags.ack == 0

Filter traffic involving the scanning host: ip.addr == 192.168.163.128

Importance:
Packet-level analysis explains the handshake process and scanning techniques.
Helps recognize stealth scanning and defensive responses.
Useful for network security monitoring and forensic analysis. 🔍

📁 Files Included

local-network-scan.txt – Nmap scan output.

scan-capture.pcapng – Wireshark capture of the scan traffic.

✅ Conclusion
This task improves skills in network reconnaissance by combining active port scanning and packet capture analysis. It highlights how services expose themselves on a network and how network tools communicate at the protocol level. Proper service configuration and firewall management are critical to reducing network exposure. 🔐

Report generated on May 26, 2025 using Kali Linux tools.
