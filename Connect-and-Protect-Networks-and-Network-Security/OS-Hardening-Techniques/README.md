# Apply OS hardening techniques

## Table of contents
1. [Scenario](#1-scenario)
2. [Executive summury](#2-executive-summary)
3. [Vulnerability Assessment & Risk Matrix](#3-vulnerability-assessment--risk-matrix)
4. [Incident Analysis & Threat Vector](#4-incident-analysis--threat-vector)
5. [Network Protocols & Log Timeline](#5-network-protocols--log-timeline)
6. [Mitigation & Hardening Strategies](6#-mitigation--hardening-strategies)
7. [Conclusion & Next Steps](#7-conclusion--next-steps)

## 1. Scenario
You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A former employee has decided to lure users to a fake website with malware. 
The former employee or hacker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After embedding the malware, the hacker changed the password to the administrative account. When customers download the file, they are redirected to a fake version of the website that contains the malware. 

Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to access free recipes. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly. 
In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. You and other cybersecurity analysts are tasked with investigating this security event.

To address the incident, you create a sandbox environment to observe the suspicious website behavior. You run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, you are prompted to download an executable file to update your browser. You accept the download and allow the file to run. You then observe that your browser redirects you to a different URL, greatrecipesforme.com, which contains the malware.  

The logs show the following process:
* The browser initiates a DNS request: It requests the IP address of the yummyrecipesforme.com URL from the DNS server.
* The DNS replies with the correct IP address.
* The browser initiates an HTTP request: It requests the yummyrecipesforme.com webpage using the IP address sent by the DNS server.
* The browser initiates the download of the malware.
* The browser initiates a DNS request for greatrecipesforme.com.
* The DNS server responds with the IP address for greatrecipesforme.com.
* The browser initiates an HTTP request to the IP address for greatrecipesforme.com.

A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 
The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled hacker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 

Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute force attacks in the future.

## 2. Executive summary
A major security incident was detected on yummyrecipesforme.com after several customers reported unusual website activity and performance problems on their computers. An investigation showed that someone carried out a successful brute-force attack against the admin account, which was protected only by a default password. The attacker changed the website's source code, added malicious JavaScript, and locked out the website owner.

## 3. Vulnerability Assessment & Risk Matrix
The investigation identified several security weaknesses that allowed this attack to succeed and amplify its impact.

| Vulnerability | Likelihood | Impact | Risk Level | Description |
| :---: | :---: | :---: | :---: | :---: |
| Default Admin Password | High | Critical | **Critical** | The administrative account used a standard default password, making it an easy target. |
| Lack of Brute-Force Controls | High | High | **High** | There were no rate-limiting or account lockout mechanisms to block repeated failed login attempts. |
| Unencrypted HTTP Protocol | High | High | **High** | The site used port 80 (HTTP) instead of port 443 (HTTPS), exposing credentials in plain text. |
| Single-Factor Authentication | High | High | **High** | The admin panel relied only on a password, providing no additional layer of defense. |

## 4. Incident Analysis & Threat Vector
The attacker used a simple method that was effective in this case to compromise the web server and attack the organization’s customers.
* **Attack Surface:** The administrative login page was publicly accessible over unencrypted HTTP with no protection against automated tools. The attacker repeatedly entered known default passwords until they guessed the correct one.
* **Malicious Modification:** After gaining access, the attacker altered the website's source code by adding a JavaScript function. Next, they changed the administrator password to prevent the owner from logging in.
* **User Impact:** When customers visited the legitimate website, the malicious JavaScript code prompted them to download an executable file. Once the users executed this file on their PCs, their systems began running more slowly, and their browsers automatically redirected them to the fake website containing further malware.

## 5. Network Protocols & Log Timeline
Analysis conducted in a sandbox environment using the `tcpdump` tool confirmed the following network process between 14:18:32 and 14:25:29:

* **DNS (Domain Name System):** The browser requested the IP address for `yummyrecipesforme.com` from `dns.google` (Query ID 35084). The server responded with the correct IP: `203.0.113.22`. Later, the malware triggered an unauthorized DNS request for `greatrecipesforme.com` (Query ID 21899), returning IP `192.0.2.17`.
* **TCP (Transmission Control Protocol):** A standard three-way handshake (`[S]`, `[S.]`, `[.]`) established connection on port 80 before any data was transferred.
* **HTTP (Hypertext Transfer Protocol):** The browser sent a `GET / HTTP/1.1` request to fetch the homepage. Because unencrypted HTTP on port 80 was used instead of HTTPS (port 443), all traffic and login details were sent in plain text.
* **Malware Delivery:** The browser downloaded the malicious file, which acted as a browser hijacker, redirecting all subsequent traffic to `greatrecipesforme.com`.

## 6. Mitigation & Hardening Strategies

To secure the website and prevent similar incidents, the following remediation steps must be implemented:

### 6.1. Primary Recommendation: Multi-Factor Authentication (MFA / 2FA)
* **Implementation:** Enforce mandatory 2FA for all administrative accounts using authenticator apps or hardware keys. 
* **Effectiveness:** Even if an attacker guesses or steals the password via brute-force or HTTP sniffing, they will be blocked without the physical second-factor token.

### 6.2. Secondary Technical Controls
* **Login Rate Limiting:** Implement account lockouts or temporary IP bans after a specific number of failed login attempts to stop automated brute-force tools.
* **Enforce HTTPS:** Migrate the entire website to HTTPS (port 443) and implement SSL/TLS encryption to protect communication and login credentials.
* **Password Policy:** Enforce a strict policy requiring long, complex, and unique passwords for all staff members.

## 7. Conclusion & Next Steps
The website was temporarily taken offline to stop the spread of malware, the original code was restored from a clean backup, and the admin password was reset. Moving forward, the company must focus on securing its authentication mechanisms.

**Immediate Action Plan:**
* **Next 24 Hours:** Deploy SSL/TLS certificates and force all traffic to use HTTPS.
* **Next 3 Days:** Enable Multi-Factor Authentication (MFA) on the web hosting panel.
* **Next Week:** Configure firewall and server rules to limit login attempts and block brute-force patterns
