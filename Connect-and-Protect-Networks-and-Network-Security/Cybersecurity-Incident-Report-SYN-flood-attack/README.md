# Cybersecurity Incident Report: SYN flood attack

## Table of contents
1. [Scenario](#1-scenario)
2. [Incident overview](#2-incident-overview)
3. [Conclusions](#3-conclusions)

## 1. Scenario
You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like. 
One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor. 

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

## 2. Incident overview
### 2.1 Executive summury

The web server fell victim to a SYN flood attack - a type of DoS attack targeting the transport layer of the TCP/IP model. The attacker floods the server with TCP packets containing the SYN flag without ever completing the three-way handshake. The server's pending connection table fills up with half-open connections. As a result, there are no resources available to handle user requests. The visitor's browser waits for a response until the timeout is reached.

### 2.2 Logs analisis
* A large number of packets with the [SYN] flag originate from a single source address (203.0.113.0) and are directed to port 443 on server 192.0.2.1.
* All malicious packets originate from the same source port (54770) and share identical parameters.
* At the start of the traffic capture, legitimate client requests were processed normally, involving a full three-way handshake and resulting in a 200 status code.
* A few seconds later, the server begins rejecting connections with [RST] packets.
* At timestamp 20.81377, the server sends its final response and then goes silent.

### 2.3 Actions taken
Restart the machine and configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests

## 3. Conclusions

The server treats every incoming SYN packet as the start of a legitimate connection: it allocates memory, creates an entry in the connection table, sends back a SYN-ACK packet, and waits for the final ACK confirmation. The attacker never sends this confirmation—often spoofing the source address so that the response never arrives. Each such connection remains half-open until the timeout expires, consuming resources.

Possible protection methods:
*  Enabling the SYN cookies mechanism on the server—the server does not reserve resources for the connection until it receives a valid ACK packet, preventing a SYN flood from filling the queue.
*  Reducing the timeout for half-open connections and increasing the size of the pending connection queue (backlog).
*  Limiting the number of new connections from a single source address (rate limiting) at the firewall.
*  Deploying an IDS/IPS with rules designed to detect SYN flood patterns.
