# Botium Toys Security Audit

## Table of contents
1. [Introduction](#1-introduction)
2. [Scenario](#2-scenario)
3. [Audit goals](#3-audit-goals)
4. [Controls assessment](#4-controls-assessment)
5. [Recommendations](#5-Recommendations)

---

## 1. Introduction
This internal security audit was completed for Botium Toys, a fictional toy company, as part of the Google Cybersecurity Professional Certificate program. 

The main goal of this audit is to assess and improve the company's current security level. As Botium Toys grows, it is crucial to protect its infrastructure, employee devices and customer data from new cyber threats. 

This assessment compares the company's security polices with the NIST CSF. The ultimate goal is to identify vulnerabilities, assess compliance risks, and provide recommendations to build a strong security system.

## 2. Scenario
Botium Toys is a small U.S. business that develops and sells toys. The business has a single physical location, which serves as their main office, a storefront, and warehouse for their products. However, Botium Toy’s online presence has grown, attracting customers in the U.S. and abroad. As a result, their information technology (IT) department is under increasing pressure to support their online market worldwide. 

The manager of the IT department has decided that an internal IT audit needs to be conducted. She's worried about maintaining compliance and business operations as the company grows without a clear plan. She believes an internal audit can help better secure the company’s infrastructure and help them identify and mitigate potential risks, threats, or vulnerabilities to critical assets. The manager is also interested in ensuring that they comply with regulations related to internally processing and accepting online payments and conducting business in the European Union (E.U.).   

The IT manager starts by implementing the National Institute of Standards and Technology Cybersecurity Framework (NIST CSF), establishing an audit scope and goals, listing assets currently managed by the IT department, and completing a risk assessment. The goal of the audit is to provide an overview of the risks and/or fines that the company might experience due to the current state of their security posture.

## 3. Audit goals

The main goals of this internal IT security audit are to:
* **Assess** Botium Toy's current alignment with the
    * National Institute of Standards and Technology Cybersecurity Framework (NIST CSF)
    * Payment Card Industry Data Security Standard (PCI DSS)
    * General Data Protection Regulation (GDPR)
* **Identify** existing vulnerabilities, gaps, and compliance risks within the IT infrastructure.
* **Evaluate** how effective current security controls are.
* **Review** existing security polices, procedures, and incident response playbooks.
* **Provide** recommendations for system hardening and future compliance with regulations.

## 4. Controls Assessment
This section evaluate the current security status of Botium Toys. It lists the company's key assets and analyzes how well the existing defense mechanisms protect them. Security Controls are divided into technical, administrative, and physical categories to identify critical vulnerabilities and compliance risks that need correction.

### 4.1 Asset Inventory
To define what needs protection, this section presents the company's assets. Below is the list of assets provided by the IT Manager, followed by the additional critical assets identified during this security audit.

#### 4.1.1 Assets Provided by the IT Manager
* **On-premises & Employee Equipment:** End-user devices (desktops, laptops, smartphones), remote workstations, headsets, cables, and keyboards.
* **Physical Inventory & Infrastructure** Storefront products in the adjoining warehouse, internet access, and internal network.
* **Management Systems:** Software for accounting, telecommunication, database, e-commerce, and inventory management.
* **Legacy Systems:** End-of-life systems that require manual human monitoring.

#### 4.1.2 Additional Critical Assets Identified by the Audit
These assets were missing from the initial IT inventory but are critical for GDPR, PCI DSS, and overall business continuity:
* **Customer & Financial Data:** Personal Identifiable Information (PII) including customer names, shipping addresses, emails, and credit card data.
* **Human Capital:** Internal employees and system administrators who access corporate systems and need security awareness training.

### 4.2 Security control matrix

| Control | Control Category | Immediate Action 🔴 | Needs Improvement 🟡 | Secure 🟢 |
| :---: | :---: | :---: | :---: | :---: |
| Least Privilege | Administrative | | ❌ | | 
| Disaster recovery plan | Administrative | | ❌ | | 
| Password policies | Administrative | ❌ | | | 
| Separation of duties | Administrative | | ❌ | | 
| Firewall | Technical | | | ❌ | 
| Intrusion detection system | Technical | ❌ | | | 
| Backups | Technical | ❌ | | | 
| Antivirus software | Technical | | | ❌ | 
| Encryption | Technical | ❌ | | | 
| Password management system | Technical | | ❌ | | 
| Locks (offices, storefront, warehouse) | Physical | | | ❌ | 
| CCTV | Physical | | | ❌ | 
| Fire detection/prevention | Physical | ❌ | | | 
| Manual monitoring, maintenance, and intervention for legacy systems | Operational | | ❌ | | 

## 4.3 Compliance Summary
Based on the Security Control Matrix, Botium Toys currently does not meet the requirements of international privacy laws and industry standards:
* **GDPR:** Customer names, addresses, and emails are stored in plaintext. This is a severe data privacy violation. The company only complies with the 72-hour breach notification rule.
* **PCI DSS:** Credit card numbers and financial transactions are not encrypted, and unauthorized users can access them. The lack of a password management system also breaks payment standards.
* **SOC (Type 1 / Type 2):** Weak access controls, missing password policies, and the lack of automated monitoring tools mean that sensitive corporate data is not properly secured.

---

## 5. Recommendations

### 5.1 Critical Priority (Immediate Action Required)
* **Data Encryption**
    * **Risk:** Storing personal data and credit card numbers in plain text violates the GDPR and PCI DSS standards. This exposes the organization to administrative penalties and reputational damage due to data leaks.
    * **Recommendation:** Implement AES-256 encryption for SQL databases containing customer information. Install SSL/TLS certificates and enforce HTTPS throughout the online store.

* **Access Control and Authentication**
    * **Risk:** The lack of a password policy allows the use of weak passwords, opening the door to brute-force attacks and administrative account takeovers.
    * **Recommendation:** Configure Active Directory to enforce a new password policy (minimum 12 characters, requiring uppercase letters, numbers, and special characters). Immediately implement multi-factor authentication (MFA) for all administrative accounts.

* **Network Monitoring and Threat Detection**
    * **Risk:** A firewall protects the network from the outside. If this security measure is breached, the attacker can freely move through the network undetected.
    * **Recommendation:** Implement an intrusion detection system (IDS), such as Snort or Suricata. Configure rules to alert users about unauthorized traffic and integrate notifications with the IT ticketing system.

* **Physical and Environmental Security**
    * **Risk:** The lack of fire protection systems creates the risk of physical damage to IT infrastructure and assets, which can lead to permanent data loss and operational paralysis.
    * **Recommendation:** Install a fire alarm system.
 
### 5.2 Medium Priority

* **Business Continuity and Data Protection Strategy**
    * **Risk:** The lack of backups poses a critical risk of permanent data loss due to ransomware incidents or infrastructure failures, which can lead to total operational paralysis.
    * **Recommendation:** Implement a comprehensive backup strategy based on the 3-2-1 model (3 separate copies, stored on 2 different types of media, with 1 copy kept in a secure, alternate off-site or cloud location).

* **Legacy System Lifecycle Management**
    * **Risk:** Unsupported legacy systems are vector attack, facilitating network breaches and unauthorized intrusion.
    * **Recommendation:** Plan the decommissioning and replacement of these systems as soon as possible. Until these resources are completely replaced, isolate them from the main network and enforce manual log monitoring to detect anomalies.

* **Identity and Access Management (IAM)**
    * **Risk:** Excessive and unrestricted user permissions give employees access to sensitive financial and corporate data that they do not require for their daily work.
    * **Recommendation:** Conduct a thorough access permissions audit. Implement the Principle of Least Privilege by deploying a Role-Based Access Control model.

* **Lack of a disaster recovery plan**
    * **Risk:** The lack of procedures prevents effective crisis management and extends the time it takes for the company to return to its pre-attack state, resulting in higher costs.
    * **Recommendation:** Develop and implement a disaster recovery plan.
