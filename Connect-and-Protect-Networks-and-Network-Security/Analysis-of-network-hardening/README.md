# Analysis of network hardening

## Table of contents
1. [Scenario](#1-scenario)
2. [Executive Summary](#2-executive-summary)
3. [Vulnerability Assessment & Risk Matrix](#3-vulnerability-assessment--risk-matrix)
4. [Incident Analysis & Threat Vector](#4-incident-analysis--threat-vector)
5. [Mitigation & Network Hardening Strategies](#5-mitigation--network-hardening-strategies)
6. [Conclusion & Next Steps](#6-conclusion--next-steps)

## 1. Scenario
You are a security analyst working for a social media organization. The organization recently experienced a major data breach, which compromised the safety of their customers’ personal information, such as names and addresses. Your organization wants to implement strong network hardening practices that can be performed consistently to prevent attacks and breaches in the future. 

After inspecting the organization’s network, you discover four major vulnerabilities. The four vulnerabilities are as follows:
* The organization’s employees' share passwords.
* The admin password for the database is set to the default.
* The firewalls do not have rules in place to filter traffic coming in and out of the network.
* Multifactor authentication (MFA) is not used. 

If no action is taken to address these vulnerabilities, the organization is at risk of experiencing another data breach or other attacks in the future. 
In this activity, you will write a security risk assessment to analyze the incident and explain what methods can be used to further secure the network.

## 2. Executive Summary
After a recent major data breach that exposed customers’ personal information (PII), including names and addresses, the company carried out a full network security review. The review showed serious weaknesses in the current security setup. Four key vulnerabilities were found in identity management and network protection. If these issues are not fixed quickly, the company is at very high risk of another breach, possible regulatory fines, and long-term loss of customer trust.

## 3. Vulnerability Assessment & Risk Matrix

To prioritize remediation efforts, the discovered vulnerabilities have been mapped based on their likelihood of exploitation and potential impact.

| Vulnerability | Likelihood | Impact | Risk Level | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Shared Employee Passwords** | High | High | **Critical** | When employees share passwords, it is impossible to know who accessed the data, and it makes it easier for attackers to move through the network. |
| **Default Database Admin Password** | High | Critical | **Critical** | The database uses standard, default passwords, which allows attackers to easily steal customer personal data if they get into the network. |
| **Misconfigured / Open Firewalls** | High | High | **High** | Because there are no traffic filtering rules, harmful internet traffic can enter and leave the network without being properly monitored or restricted. |
| **Lack of Multi-Factor Authentication (MFA)** | High | High | **High** | Single-factor authentication makes phishing attacks highly effective. |

## 4. Incident Analysis & Threat Vector

The recent data breach, which resulted in the theft of customer names and addresses, happened because the organization lacked basic security controls.
* **Attack Surface:** Because the firewall did not properly filter traffic, an external attacker could easily scan the network. This enabled them to reach the main customer database and gain access using the default login credentials.
* **Lateral Movement:** After entering the network, the attacker could move across other systems with little chance of detection. This was largely due to the lack of MFA and the common practice of employees sharing passwords.

## 5. Mitigation & Network Hardening Strategies

To protect the network and stop future attacks, the organization must implement the following security practices immediately:

### 5.1 Identity & Access Management (IAM)
* **Enforce Unique Accounts:** Stop the practice of sharing passwords immediately. Every employee must have their own account. The organization should also introduce a password manager tool to help staff store credentials safely.
* **Mandatory Multi-Factor Authentication (MFA):** Require MFA for all employee accounts. Priority must be given to IT administrators and staff who access the customer database.
* **Change Default Passwords:** Change the default database administrator password immediately. The new password must be long, complex, and changed regularly.

### 5.2 Network Security
* **Configure Firewall Rules:** Set up clear rules on all firewalls to filter network traffic. The firewalls should only allow safe, necessary connections and block all suspicious traffic from entering or leaving the network.
* **Network Segmentation:** Divide the internal network into separate zones. The database containing customer personal data must be isolated from the general employee network.

## 6. Conclusion & Next Steps
The recent data breach shows that the organization needs to update its security practices immediately. By implementing MFA, enforcing strict password policies, changing default credentials, and configuring firewall rules, the company will significantly reduce its attack surface and protect customer data in the future.

**Immediate Action Plan:**
* **Next 24 Hours:** Change the default database administrator password.
* **Next 3 Days:** Create and deploy the new firewall filtering rules.
* **Next Week:** Roll out mandatory MFA, starting with administrative accounts.
