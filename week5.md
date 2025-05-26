Week-5

Networt: is a practice of connecting multiple computer devices communicate with each other to share information, resources, and services.
The computer network can be linked through a medium such as cables , telephone lines, satellite or infrared beam.

Types of network:
LAN:Local Area Network- used in home,office or school.
WAN:Wide area Networ that transfer the data from one area to other area.
WLAN (Wireless LAN)LAN that uses Wi-Fi
VPN (Virtual Private Network): Creates a secure connection over the internet

IP Address (Internet Protocol):Like a home address, but for devices.Every device on a network has one

IP stands for Internet Protocol.
It is a set of rules that govern how data is sent and received over the internet or any network.
Each device on a network is assigned a unique IP address.

Types of IP Addresses:

| Type       | Version | Visibility     | Assigned By       | Example      |
| ---------- | ------- | -------------- | ----------------- | ------------ |
| IPv4       | IPv4    | Public/Private | ISP/Admin         | 192.168.1.1  |
| IPv6       | IPv6    | Public/Private | ISP/Admin         | 2001\:db8::1 |
| Public IP  | Either  | Public         | ISP               | 203.0.113.5  |
| Private IP | Either  | Local only     | Router (DHCP)     | 192.168.0.10 |
| Static IP  | Either  | Either         | Manually set      | Varies       |
| Dynamic IP | Either  | Either         | Automatically set | Varies       |

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

All Transmissions Involve Networks

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

PRINCE-WAD:

| **Letter** | **Stands For**             | **What to Do**                                    |
| ---------- | -------------------------- | ------------------------------------------------- |
| **P**      | **Power & Physical**       | Check cables, power, router lights                |
| **R**      | **Restart Devices**        | Restart your computer and network devices         |
| **I**      | **IP Address Check**       | Use `ipconfig` / `ip a` to confirm valid IP       |
| **N**      | **Network Adapter**        | Make sure Wi-Fi or Ethernet adapter is enabled    |
| **C**      | **Connectivity Test**      | Ping `8.8.8.8` and `google.com`                   |
| **E**      | **Examine DNS**            | Try different DNS (8.8.8.8, 1.1.1.1), flush cache |
| **W**      | **Wi-Fi & Wired Settings** | Check if you’re on the correct network            |
| **A**      | **Antivirus/Firewall**     | Temporarily disable to test if they’re blocking   |
| **D**      | **Device or ISP Issue**    | Check other devices or contact your ISP           |

P – Plugged in? Power OK?
R – Reboot everything!.
I – IP valid?
N – Network adapter enabled?
C – Can you ping?
E – Edit DNS?
W – Wi-Fi connected?
A – Antivirus blocking?
D – Down ISP?

DNS is like the phonebook of the internet.
It translates human-friendly domain names (like google.com) into IP addresses (like 142.250.190.78) that computers use to talk to each other.

IP stands for Internet Protocol.
It is a set of rules that govern how data is sent and received over the internet or any network.
Each device on a network is assigned a unique IP address.

How DNS Works (Simplified):

You type www.example.com into your browser.
The DNS resolver checks its cache for the IP. If not found:
It asks a root DNS server, then a TLD server, then the authoritative DNS server for example.com.
The resolver gets the IP address and sends it to your browser.
The browser connects to the server at that IP and loads the website.

HTTP Headers:
Http headers is the set of metadata in the http request or response. 
It defines how the data is tranfered between the client and the server.
Headers give extra information such as content type, authentication details, caching instructions, and more.

Structure of an HTTP Header:
Header-Name: Header-Value

Categories of HTTP Headers:

General Headers:
Response headers:
Request Headers:
security headers:
Entity headers:

How to View HTTP Headers:

Browser Dev Tools: Open Dev Tools (F12) → Network tab → Click a request → Headers

curl -I https://example.com

Protocol is a set of rules that define how the data is formatted, transmitted and received over the network.
Without protocol, computer wont understand eachother.
Consider protocol like a agreement , where computer follow to commnunicate reliably.


Categories of Protocol:

Communication Protocol:

| Protocol         | Description                                        |
| ---------------- | -------------------------------------------------- |
| **HTTP/HTTPS**   | Transfers web data. HTTPS is secure using SSL/TLS. |
| **FTP/SFTP**     | File transfer protocol (SFTP is secure).           |
| **SMTP**         | Sends emails.                                      |
| **IMAP/POP3**    | Receives emails.                                   |
| **Telnet / SSH** | Remote login protocols (SSH is secure).            |

Internet Protocol:
| Layer              | Protocols       | Description                       |
| ------------------ | --------------- | --------------------------------- |
| **Application**    | HTTP, FTP, SMTP | User-facing services              |
| **Transport**      | TCP, UDP        | Reliable/unreliable data transfer |
| **Internet**       | IP, ICMP        | Routing and addressing            |
| **Network Access** | Ethernet, Wi-Fi | Physical data transfer            |


network Protocol:
| Protocol                                | Purpose                                     |
| --------------------------------------- | ------------------------------------------- |
| **IP (IPv4/IPv6)**                      | Assigns addresses and routes packets.       |
| **TCP (Transmission Control Protocol)** | Ensures reliable delivery.                  |
| **UDP (User Datagram Protocol)**        | Fast, connectionless transmission.          |
| **ICMP**                                | Sends error/report messages (e.g., `ping`). |
| **ARP**                                 | Maps IP addresses to MAC addresses.         |
| **DHCP**                                | Automatically assigns IP addresses.         |
| **DNS**                                 | Converts domain names to IP addresses.      |

4. Security Protocols

| Protocol    | Purpose                                      |
| ----------- | -------------------------------------------- |
| **SSL/TLS** | Encrypts data over networks (used in HTTPS). |
| **IPSec**   | Secures IP communications.                   |
| **HTTPS**   | Secure HTTP (web encryption).                |
| **SSH**     | Secure remote login.                         |
