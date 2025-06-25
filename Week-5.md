
# Networking Basics

## What is Networking?

Networking is the practice of connecting multiple computer devices to communicate with each other to share information, resources, and services. Devices can be connected using mediums like cables, telephone lines, satellite, or infrared beams.

---

## Types of Networks

| Type                              | Description                         | Example           |
| --------------------------------- | ----------------------------------- | ----------------- |
| **LAN** (Local Area Network)      | Small area                          | Home, office      |
| **WAN** (Wide Area Network)       | Large area, multiple locations      | The Internet      |
| **WLAN** (Wireless LAN)           | Wireless network                    | Wi-Fi             |
| **VPN** (Virtual Private Network) | Secure connection over the Internet | Remote work tools |

---

## IP Address

IP stands for Internet Protocol, a set of rules that govern how data is sent and received over the internet or any network.

| Type       | Version | Visibility     | Assigned By       | Example      |
| ---------- | ------- | -------------- | ----------------- | ------------ |
| IPv4       | IPv4    | Public/Private | ISP/Admin         | 192.168.1.1  |
| IPv6       | IPv6    | Public/Private | ISP/Admin         | 2001:db8::1  |
| Public IP  | Either  | Public         | ISP               | 203.0.113.5  |
| Private IP | Either  | Local only     | Router (DHCP)     | 192.168.0.10 |
| Static IP  | Either  | Either         | Manually set      | Varies       |
| Dynamic IP | Either  | Either         | Automatically set | Varies       |

---

## Networking Devices

- **Router**: Directs traffic between your local network and the Internet.
- **Switch**: Connects devices within a network.
- **Modem**: Connects your home network to your Internet provider.
- **DNS**: Translates domain names (like google.com) into IP addresses.
- **Ports**: Virtual doors for different types of traffic (e.g., 80=HTTP, 443=HTTPS).

---

## Firewall

A security system that controls incoming and outgoing network traffic.

---

## Useful Network Commands

| Command                                   | What it Does                      |
| ----------------------------------------- | --------------------------------- |
| `ping`                                    | Checks if a device is reachable   |
| `ipconfig` / `ifconfig`                   | Shows IP address and network info |
| `tracert` / `traceroute`                  | Shows the path your data takes    |
| `netstat`                                 | Lists network connections         |
| `nslookup`                                | Checks DNS info for a website     |

---

## OSI Model

"All People Seem To Need Data Processing"

| Layer | Name            | Description                          | Protocols                             |
| ----- | --------------- | ------------------------------------ | --------------------------------------|
| 7     | Application     | User interfaces and services         | HTTP, FTP, SMTP, DNS                  |
| 6     | Presentation    | Data formatting                      | SSL/TLS, JPEG                         |
| 5     | Session         | Starts and ends communication        | NetBIOS, RPC                          |
| 4     | Transport       | Reliable data transfer               | TCP, UDP                              |
| 3     | Network         | Routing and addressing               | IP, ICMP                              |
| 2     | Data Link       | Same-network delivery (MAC)          | Ethernet, ARP                         |
| 1     | Physical        | Physical hardware & signals          | Wi-Fi, Ethernet, Fiber Optics         |

---

## TCP/IP Model

| Layer              | Description                           | OSI Equivalent     | Protocols                |
| ------------------ | ------------------------------------- | ------------------ | ------------------------ |
| Application        | User-facing services                  | Layers 5, 6, 7     | HTTP, FTP, DNS           |
| Transport          | Reliable/unreliable transmission      | Layer 4            | TCP, UDP                 |
| Internet           | Routing and addressing                | Layer 3            | IP, ICMP, ARP            |
| Network Access     | Physical medium and addressing        | Layers 1, 2        | Ethernet, Wi-Fi, MAC     |

---

## Data Transmission Flow

| Step | What Happens                             | OSI Layer    | TCP/IP Layer   |
| ---- | ---------------------------------------- | ------------ | -------------- |
| 1    | You type a URL in browser                | Application  | Application    |
| 2    | Request is formatted                     | Presentation | Application    |
| 3    | Session is established                   | Session      | Application    |
| 4    | Data is chunked                          | Transport    | Transport      |
| 5    | IP is added                              | Network      | Internet       |
| 6    | MAC added for local delivery             | Data Link    | Network Access |
| 7    | Data sent via Wi-Fi/Ethernet             | Physical     | Network Access |

---

## Basic Network Troubleshooting

1. Physical connection
2. Restart devices
3. Check IP address
4. Ping test
5. Traceroute
6. Check firewall/antivirus
7. DNS settings
8. Flush DNS cache
9. Router/ISP status
10. Use advanced tools

### PRINCE-WAD Troubleshooting

| Letter | Meaning                  | Action                                         |
|--------|--------------------------|------------------------------------------------|
| P      | Power & Physical         | Check cables, power, and lights                |
| R      | Restart Devices          | Restart router and PC                          |
| I      | IP Address Check         | Run `ipconfig` or `ip a`                       |
| N      | Network Adapter          | Ensure adapter is enabled                      |
| C      | Connectivity Test        | Ping 8.8.8.8 and google.com                    |
| E      | Examine DNS              | Try different DNS or flush cache               |
| W      | Wi-Fi/Wired Settings     | Check network name and signal strength         |
| A      | Antivirus/Firewall       | Temporarily disable to test access             |
| D      | Device/ISP Issue         | Check another device or contact your ISP       |

---

## DNS (Domain Name System)

- Like a phonebook: Converts domain names to IP addresses.
- Steps:
  - Type a URL.
  - Resolver checks cache or queries root → TLD → authoritative server.
  - Returns IP to browser → loads website.

---

## HTTP Headers

Headers are metadata in HTTP requests/responses.

**Structure**: `Header-Name: Header-Value`

### Categories:
- General Headers
- Request Headers
- Response Headers
- Entity Headers
- Security Headers

**View Headers**:
- Browser Dev Tools → Network tab
- `curl -I https://example.com`

---

## Network Protocols

### Communication Protocols

| Protocol       | Description                                |
|----------------|--------------------------------------------|
| HTTP/HTTPS     | Transfers web data                         |
| FTP/SFTP       | Transfers files                            |
| SMTP/IMAP/POP3 | Sends and receives emails                  |
| Telnet/SSH     | Remote login                               |

### Internet Protocol Stack

| Layer              | Protocols         | Description                     |
|--------------------|-------------------|---------------------------------|
| Application        | HTTP, FTP, SMTP   | User-facing services            |
| Transport          | TCP, UDP          | Reliable/unreliable transfer    |
| Internet           | IP, ICMP          | Routing and addressing          |
| Network Access     | Ethernet, Wi-Fi   | Physical data transfer          |

### Core Protocols

| Protocol   | Purpose                                       |
|------------|-----------------------------------------------|
| IP         | Addressing and routing                        |
| TCP        | Reliable communication                        |
| UDP        | Fast, connectionless transfer                 |
| ICMP       | Diagnostics (e.g., ping)                      |
| ARP        | Resolves IP to MAC addresses                  |
| DHCP       | Assigns IP addresses                          |
| DNS        | Resolves domain names                         |

### Security Protocols

| Protocol    | Purpose                                      |
|-------------|----------------------------------------------|
| SSL/TLS     | Encrypted communication                      |
| IPsec       | Secure IP-level traffic                      |
| HTTPS       | Secure HTTP communication                    |
| SSH         | Secure remote terminal access                |
