# Cybersecurity Incident Report: Network Traffic Analysis

## Table of contents
1. [Scenario](#1-scenario)
2. [Incident overview](#2-incident-overview)

## 1. Scenario
You are a cybersecurity analyst working at a company that specializes in providing IT services for clients. Several customers of clients reported that they were not able to access the client company website www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 
You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you attempt to visit the website and you also receive the error “destination port unreachable.” To troubleshoot the issue, you load your network analyzer tool, tcpdump, and attempt to load the webpage again. To load the webpage, your browser sends a query to a DNS server via the UDP protocol to retrieve the IP address for the website's domain name; this is part of the DNS protocol. Your browser then uses this IP address as the destination IP for sending an HTTPS request to the web server to display the webpage  The analyzer shows that when you send UDP packets to the DNS server, you receive ICMP packets containing the error message: “udp port 53 unreachable.” 

## 2. Incident overview

### 2.1 Executive summary
The network protocol analyzer showed that queries for yummyrecipesforme.com domain  were sent to DNS Server over UDP protocol but there wasn’t any response from server.  Only an error message was received via the ICMP protocol - udp port 53 unreachable. It happened three times so one-time packet loss can be excluded. Port 53 is used by the DNS service, which is responsible for translating domain names. It suggests that DNS Server could be disabled, damaged, overloaded (e.g. DoS attack) or something blocking traffic on this port. Without this service the browser can’t connect to the site.

### 2.2 Time incident

| Date & time | Source IP | Destination IP | Protocol | Info / Message |
| :---: | :---: | :---: | :---: | :---: |
| 13:24:32.192571 | 192.51.100.15 | 203.0.113.2 | UDP (DNS) | DNS Query: [ID 35084+] A? yummyrecipesforme.com |
| 13:24:36.098564 | 203.0.113.2 | 192.51.100.15 | ICMP | ICMP error: udp port 53 unreachable (length 254) |
| 13:26:32.192571 | 192.51.100.15 | 203.0.113.2 | UDP (DNS) | DNS Query: [ID 35084+] A? yummyrecipesforme.com |
| 13:27:15.934126 | 203.0.113.2 | 192.51.100.15 | ICMP | ICMP error: udp port 53 unreachable (length 320) |
| 13:28:32.192571 | 192.51.100.15 | 203.0.113.2 | UDP (DNS) | DNS Query: [ID 35084+] A? yummyrecipesforme.com |
| 13:28:50.022967 | 203.0.113.2 | 192.51.100.15 | ICMP | ICMP error: udp port 53 unreachable (length 150) |

### 2.3 Incident Detection
The IT department became aware of the incident after receiving user reports. Users stated that they were unable to access the website yummyrecipesforme.com. They experienced a browser error message indicating "destination port unreachable" after waiting for the page to load. 

### 2.4 Investigative Actions
After confirming the error, the network traffic analysis tool (tcpdump) was used. Tcpdump captured network traffic while the page was loading. The logs were analyzed in terms of used protocols, source and destination addresses, and port numbers. UDP (DNS queries) and ICMP (error messages) protocols were identified. The incident was reported to the direct supervisor and referred to the security engineering team, which is taking further action to restore access to the site.

### 2.4 Conclusion
The investigation shows that the root cause of the incident is the unavailability of the DNS server with the IP address 203.0.113.2. The server was most likely shut down or overloaded, making a DoS / DDoS attack highly probable. Alternatively, a recent change in the firewall configuration could be blocking network traffic on port 53.


