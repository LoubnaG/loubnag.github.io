---
title: "Threat Hunting Using Wireshark"
description: "Learn how to identify threats and attacks via network analysis using wireshark."
readtime: 6 minute read
header:
  teaser: /threat-hunting/assets/images/tools-wireshark.png
  overlay_image: /threat-hunting/assets/images/tools-wireshark.png
  overlay_filter: 0.5

ribbon: Tools
tags:   
  - Threat Hunting
  - Tools
bg: rgb(0, 159, 0)
toc: true
toc_sticky: true
toc_label: "Table of Contents"
# toc_icon: "heart"
toc: true
classes: wide
last_modified_at: 2023-09-28
---
<span style="color:#909090">Learn how to identify threats and attacks via network analysis using wireshark</span>

# Wireshark Overview
## What is Wireshark?
Wireshark is a network packet analyzer. A network packet analyzer presents captured packet data in as much detail as possible. (*Wireshark.org*)<br>
It is a free open source tool that analyzes network traffic in real-time for Windows, Mac, Unix, and Linux systems by capturing packets from a network interface or reading packets from a capture file. 
## Wireshark Core Features
- Deep inspection of hundreds of protocols
- Live capture
- Offline analysis
- Support multiple OS (Windows, Linux, Mac OS)
- Powerful packet filters
- Colorize packet display based on filters
- Create various statistics
- ... and much more!
## Wireshark Options
📌 Protocol Hierarchy:<br>
Generates a protocol hierarchy chart that contains the statistical values of each protocol (Percent Packets and Percent Bytes):

| ![Protocol Hierarchy Window](/assets/images/threat-hunting/Tools/Wireshark/wireshark1.png) | 
|:--:| 
| *Protocol Hierarchy Window* |

📌 Conversations:<br>
This window shows all the established conversations between two endpoints alongside with other info like packet count, bytes, duration, etc. This option provides the list of the conversations in five base formats; ethernet, IPv4, IPv6, TCP and UDP. Thus analysts can identify all conversations and contact endpoints for the event of interest.

| ![Conversation Window](/assets/images/threat-hunting/Tools/Wireshark/wireshark2.png) | 
|:--:| 
| *Conversation Window* |

📌 I/O Graph: <br>
A Wireshark I/O Graph is one of the basic diagrams that is created using the packets present in the capture file. Useful for viewing packet and log data in a variety of ways.

| ![I/O Graph Window](/assets/images/threat-hunting/Tools/Wireshark/wireshark3.png) | 
|:--:| 
| *I/O Graph Window* |

📌 Endpoints: <br>
This window shows statistics about the endpoints captured. The endpoints option is similar to the conversations option. The only difference is that this option provides unique information for a single information field (Ethernet, IPv4, IPv6, TCP and UDP ). Thus analysts can identify the unique endpoints in the capture file and use it for the event of interest

| ![Endpoints Window](/assets/images/threat-hunting/Tools/Wireshark/wireshark4.png) | 
|:--:| 
| *Endpoints Window* |

*For more options, you can visit wireshark official documentation*
## Filters
<table>
  <tr style="border:2px solid #b3adad;">
    <th style="border:2px solid #b3adad;">Filter</th>
    <th style="border:2px solid #b3adad;">Symbol</th>
    <th style="border:2px solid #b3adad;">Example</th>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">equal</td>
    <td style="border:2px solid #b3adad;"> ==</td>
    <td style="border:2px solid #b3adad;">ip.src == 192.168.12.2</td>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">not equal</td>
    <td style="border:2px solid #b3adad;"> !=</td>
    <td style="border:2px solid #b3adad;">ip.src != 192.168.12.2</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">AND</td>
    <td style="border:2px solid #b3adad;"> &&</td>
    <td style="border:2px solid #b3adad;">ip.src==10.0.0.1 and tcp.flags.syn</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;"> OR</td>
    <td style="border:2px solid #b3adad;"> ||</td>
    <td style="border:2px solid #b3adad;">ip.src==10.0.0.1 or tcp.flags.syn</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">greater than </td>
    <td style="border:2px solid #b3adad;"> ></td>
    <td style="border:2px solid #b3adad;">ip.ttl > 250</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">less than </td>
    <td style="border:2px solid #b3adad;"> <</td>
    <td style="border:2px solid #b3adad;">frame.len < 100</td> 
  </tr>
</table>
<br>
<table>
  <tr style="border:2px solid #b3adad;">
    <th style="border:2px solid #b3adad;">Protocol</th>
    <th style="border:2px solid #b3adad;">Filter</th>
    <th style="border:2px solid #b3adad;">Description</th>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">ARP</td>
    <td style="border:2px solid #b3adad;">- Arp.dst.hw</td> 
    <td style="border:2px solid #b3adad;">- Hardware Address</td> 
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">HTTP</td>
    <td style="border:2px solid #b3adad;">- http.response.code == 200<br>- http.request.method == "GET"</td>
    <td style="border:2px solid #b3adad;">-  packets with HTTP response code "200"<br>- Show all HTTP GET requests</td> 
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">FTP</td>
    <td style="border:2px solid #b3adad;">- ftp.command<br>- ftp.active.cip</td>
       <td style="border:2px solid #b3adad;">- filter FTP commands<br>- filter active IP address</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;"> TCP</td>
    <td style="border:2px solid #b3adad;">- tcp.port == 80<br>- tcp.ack</td>
    <td style="border:2px solid #b3adad;">- Show all TCP packets with port 80<br>- Show acknowledgement packets</td>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;"> UDP</td>
    <td style="border:2px solid #b3adad;">- udp.port == 53<br>- udp.srcport== 1234</td>
    <td style="border:2px solid #b3adad;">- Show all UDP packets with port 53<br>- Show all UDP packets originating from port 1234</td>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;"> DNS</td>
    <td style="border:2px solid #b3adad;">- dns.flags.response == 0<br>- dns.flags.response == 1<br>
    - dns.qry.type == 1</td>
    <td style="border:2px solid #b3adad;">- Show all DNS requests<br>- Show all DNS responses<br>
    - Show all DNS "A" records</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">ICMP </td>
    <td style="border:2px solid #b3adad;"> - icmp.code<br>- icmp.data_time<br>- icmp.type</td>
    <td style="border:2px solid #b3adad;">- filter ICMP code<br>- filter ICMP data timestamp<br>
       - filter ICMP packets types</td>
  </tr>
</table>

## Advanced Filtering
<table>
  <tr style="border:2px solid #b3adad;">
    <th style="border:2px solid #b3adad;">Filter</th>
    <th style="border:2px solid #b3adad;">Description</th>
    <th style="border:2px solid #b3adad;">Example</th>
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">contains</td>
    <td style="border:2px solid #b3adad;"> Search a value inside packets</td>
    <td style="border:2px solid #b3adad;">- http.server contains "Apache" => Find all "Apache" servers</td>
   
  </tr>
  <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">matches</td>
    <td style="border:2px solid #b3adad;"> Search a pattern of a regular expression</td>
    <td style="border:2px solid #b3adad;">- http.host matches "\.(php|html)" => Find all .php and .html pages</td>
  </tr>
   <tr style="border:2px solid #b3adad;">
    <td style="border:2px solid #b3adad;">in</td>
    <td style="border:2px solid #b3adad;"> Search a value or field inside of a specific scope/range</td>
    <td style="border:2px solid #b3adad;">- tcp.port in {80 443 8080} => Find all packets that use ports 80, 443 or 8080</td>
  </tr>
</table>

# Hunting with Wireshark 
## TCP Malicious Traffic
There are multiple patterns for malicious TCP traffic, for example, we can hunt for port scans by searching for:
- SYN without SYN/ACK.
- SYN/ACK without SYN before. 
- ACK without a SYN/ACK before.<br>

📍 <span style="color:#cad2ed">Nmap TCP SYN Scans :</span> Usually have a size less than or equal to 1024 bytes as the request is not finished and it doesn't expect to receive data<br>
↪ `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024`<br>
📍 <span style="color:#cad2ed">Nmap TCP Connect Scan :</span> Usually has a windows size larger than 1024 bytes as the request expects some data due to the nature of the protocol<br>
↪ `tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size > 1024`<br>
📍 <span style="color:#cad2ed">Nmap Zombie Scan :</span> It is a TCP port Scan method used to send a spoofed source address to a computer to find out what services are available and offers blind scanning of a remote host. This is accomplished by impersonating another computer. No packet is sent from its own IP address, instead, another host is used called Zombie.

| ![Nmap Zombie Scan](/assets/images/threat-hunting/Tools/Wireshark/wireshark5.png) | 
|:--:| 
| *Nmap Zombie Scan* |

The screenshot below shows the phases in which scan happens :<br>
- The first slot show communication between attacker and zombie.
- The second slot is where the actual scan takes place. The zombie communicates with
the target.
- The third slot is communication between zombie and attacker to verify port status.<br>

## HTTP Malicious Traffic
HTTP traffic should be monitored carefully because various attacks are conducted over HTTP.<br>
For example, signs of SQL Injection attacks or XSS can be shown in HTTP traffic. Also, web shells and exploits can be uploaded over HTTP.<br>

📍 <span style="color:#cad2ed">Hunting Nmap in HTTP traffic :</span> `http.user_agent contains "nmap"`

## DNS Malicious Traffic
📍 DNS Exfiltration : <br>
Data can be exfiltrated using DNS in many formats, for example, data chunks can be included with the subdomains for a domain name or can be transferred inside malformed packets.

| ![DNS Exfiltration](/assets/images/threat-hunting/Tools/Wireshark/wireshark6.png) | 
|:--:| 
| *DNS Exfiltration* |

## Exfiltration through ICMP
ICMP is a supporting protocol in the Internet protocol suite and is widely known for its applications such as ping or traceroute. Malicious actors can use ICMP to exfiltrate data, by taking advantage of organizations that allow outbound ICMP traffic.

| ![ICMP Exfiltration](/assets/images/threat-hunting/Tools/Wireshark/wireshark7.png) | 
|:--:| 
| *ICMP Exfiltration* |

# Hunt cleartext credentials :
 Some Wireshark dissectors (FTP, HTTP, IMAP, pop and SMTP) are programmed to extract cleartext passwords from the capture file. You can view detected credentials using Wireshark under the `Tools --> Credentials` menu. This feature works only after specific versions of Wireshark (v3.1 and later). Since the feature works only with particular protocols, it is suggested to have manual checks and not entirely rely on this feature to decide if there is a cleartext credential in the traffic.

# Example: Log4j Hunting 
## What is Log4j Vulnerability
Log4j is an open-source logging framework maintained by Apache used to log messages within software and has the ability to communicate with other services on a system. This communication functionality is where the vulnerability exists, providing an opening for an attacker to inject malicious code into the logs so it can be executed on the system. <br>
This zero-day vulnerability in the Apache Log4j logging utility has been allowing easy-to-exploit remote code execution (RCE). Attackers can use this security vulnerability in the Java logging library to insert text into log messages that load the code from a remote server.<br>

💡 The targeted server by attackers can execute a code via calls to the Java Naming and Directory Interface (JNDI), which connects its interface with several services such as Lightweight Directory Access Protocol (LDAP), Domain Name Service (DNS), Java’s Remote Interface (RMI). Attackers will then exploit LDAP, DNS, RMI, and URLs by redirecting to an external server.

## Wireshark Filters for Log4j Hunting
- `http.request.method == "POST"`
- `(ip contains "jndi") or (ip contains "Exploit")`
- `(frame contains "jndi") or (frame contains "Exploit")`
- `(http.user_agent contains "$") or (http.user_agent contains "==")`

# Conclusion
Wireshark is a great tool for Security analysts, Threat hunters and all professionals in general to identify cyber network attacks and conduct threat hunt at the packet level. This can be done starting from network scans hunting, next discovering Web attacks through malicious HTTP traffic and data exfiltration. And last, discover how to spot indicators of compromise in case of malware infections.
<hr>
<!-- - <span style="color:#cad2ed"> Phishing: </span> <br> -->
 
> "To beat a hacker, you have to think like a hacker" 💙
<hr>
<p align="center">
  <img src="/assets/images/icons/cat.jpg" alt="Terminal Shortcuts" style="width:420px;height:320px;">
</p>
---
