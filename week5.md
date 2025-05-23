Week-5

Networt: is a practice of connecting multiple computer devices communicate with each other to share information, resources, and services.
The computer network can be linked through a medium such as cables , telephone lines, satellite or infrared beam.

Types of network:
LAN:Local Area Network- used in home,office or school.
WAN:Wide area Networ that transfer the data from one area to other area.
WLAN (Wireless LAN)LAN that uses Wi-Fi
VPN (Virtual Private Network): Creates a secure connection over the internet

IP Address (Internet Protocol):Like a home address, but for devices.Every device on a network has one
Router: Directs traffic between your local network and the Internet.
Switch: Connects devices within a network (like PCs, printers).
Modem: Connects your home network to your Internet provider.
DNS (Domain Name System):Translates domain names (like google.com) into IP addresses.
Ports:Virtual doors on a device that control what kind of traffic comes in or out
Example:
Port 80 = HTTP (web),
Port 443 = HTTPS,
Port 22 = SSH

Firewall: A security system that controls incoming and outgoing traffic.

| Type                              | Description                         | Example           |
| --------------------------------- | ----------------------------------- | ----------------- |
| **LAN** (Local Area Network)      | Small area                          | Home, office      |
| **WAN** (Wide Area Network)       | Large area, multiple locations      | The Internet      |
| **WLAN** (Wireless LAN)           | Wireless network                    | Wi-Fi             |
| **VPN** (Virtual Private Network) | Secure connection over the Internet | Remote work tools |


| Command                                   | What it Does                      |
| ----------------------------------------- | --------------------------------- |
| `ping`                                    | Checks if a device is reachable   |
| `ipconfig` (Windows) / `ifconfig` (Linux) | Shows IP address and network info |
| `tracert` / `traceroute`                  | Shows the path your data takes    |
| `netstat`                                 | Lists network connections         |
| `nslookup`                                | Checks DNS info for a website     |


. OSI Model (Open Systems Interconnection):The OSI model (Open Systems Interconnection) is a theoretical framework with 7 layers.

Hint to remember:

"All People Seem To Need Data Processing"
(Application, Presentation, Session, Transport, Network, Data Link, Physical)

| OSI Layer | Layer Name       | Description                                    | Example Protocols                                |
| --------- | ---------------- | ---------------------------------------------- | ------------------------------------------------ |
| **7**     | **Application**  | User interfaces, app-level services            | **HTTP**, FTP, SMTP, DNS, POP3                   |
| **6**     | **Presentation** | Data formatting (encryption, compression)      | **SSL/TLS**, JPEG, MPEG                          |
| **5**     | **Session**      | Starts, maintains, ends communication sessions | **NetBIOS**, RPC, PPTP                           |
| **4**     | **Transport**    | Reliable delivery of data                      | **TCP**, UDP                                     |
| **3**     | **Network**      | Routing and addressing (IP addresses)          | **IP**, ICMP, IPsec                              |
| **2**     | **Data Link**    | Frame delivery on the same network             | **Ethernet**, PPP, MAC, ARP                      |
| **1**     | **Physical**     | Physical hardware (cables, signals)            | **Wi-Fi**, Ethernet (cables), Fiber optics, Hubs |

| **Layer**            | **Protocol**                                                        | **Full Form** |
| -------------------- | ------------------------------------------------------------------- | ------------- |
| **7 - Application**  |                                                                     |               |
| HTTP                 | HyperText Transfer Protocol                                         |               |
| FTP                  | File Transfer Protocol                                              |               |
| DNS                  | Domain Name System                                                  |               |
| SMTP                 | Simple Mail Transfer Protocol                                       |                                                                     
| **6 - Presentation** |                                                                     |               |
| SSL                  | Secure Sockets Layer                                                |               |
| TLS                  | Transport Layer Security                                            |               |
| **5 - Session**      |                                                                     |               |
| NetBIOS              | Network Basic Input/Output System                                   |               |
| **4 - Transport**    |                                                                     |               |
| TCP                  | Transmission Control Protocol                                       |               |
| **3 - Network**      |                                                                     |               |
| IP                   | Internet Protocol                                                   |               |
| **2 - Data Link**    |                                                                     |               |
| ARP                  | Address Resolution Protocol                                         |               |
| **1 - Physical**     |                                                                     |               |
| Wi-Fi                | Wireless Fidelity                                                   |               |

Troubleshooting by Layer:

Learn how problems at each layer look:

Layer 1: Cable unplugged
Layer 3: Wrong IP address
Layer 4: Port blocked by firewall
Layer 7: Web app not responding


🌐 TCP/IP Model (4 Layers)
| **TCP/IP Layer**      | **Description**                           | **Similar OSI Layers** | **Key Protocols**    |
| --------------------- | ----------------------------------------- | ---------------------- | -------------------- |
| **1. Application**    | Interfaces with the user; services & data | OSI Layers 5, 6, 7     | HTTP, FTP, SMTP, DNS |
| **2. Transport**      | End-to-end connection and reliability     | OSI Layer 4            | TCP, UDP             |
| **3. Internet**       | Logical addressing and routing            | OSI Layer 3            | IP, ICMP, ARP, IGMP  |
| **4. Network Access** | Physical addressing and media control     | OSI Layers 1 & 2       | Ethernet, Wi-Fi, MAC |


| Step | What Happens (Simplified)                | OSI Layer    | TCP/IP Layer   |
| ---- | ---------------------------------------- | ------------ | -------------- |
| 1    | You type a URL in your browser           | Application  | Application    |
| 2    | The browser formats your request         | Presentation | Application    |
| 3    | A session is established with the server | Session      | Application    |
| 4    | Data is broken into chunks (TCP packets) | Transport    | Transport      |
| 5    | Destination IP is added                  | Network      | Internet       |
| 6    | MAC address added for local delivery     | Data Link    | Network Access |
| 7    | Data is sent via Wi-Fi/Ethernet          | Physical     | Network Access |


Basic Network Troubleshooting Steps:
1.Physical connection
2.Restart devices
3.check ip address
4.ping test
5.traceroute
6.check firewall/antivirus
7.check dns settings
8.flush dns cache
9.check router/isp
10.advanced tool
