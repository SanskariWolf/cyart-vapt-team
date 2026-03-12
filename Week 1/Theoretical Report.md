# Understanding Security Assessment
[Reference](https://www.resilientx.com/blog/the-step-by-step-guide-for-vulnerability-assessment-with-nist-cybersecurity-framework)
[NIST CSF](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf)
#### About NIST Framework
1. NIST Framework consist of 5 core functions - Identify, Protect, Detect, Respond, and Recover
2. These functions further have categories and sub-categories
3. For Vulnerability Assessment, first function i.e. Identity is put into focus. It is supported by Asset Management, Risk Assessment, and Risk Management Strategy.
![](Images/Pasted%20image%2020260410190153.png)
#### Using it for youself
1. It begin with the identification of assets and systems we have and needs protection
2. It includes physical devices, networks, software applications and data
3. Questiosn that needs to be asked
	1. What are the critical assets and systems within your organization?
	2. What are the potential threats to these assets and systems?
	3. What are the potential vulnerabilities that could be exploited by these threats?
4. Inventory for assets and systems, and priority should be given based on their importance.

#### Performing a Vulnerability Scan
1. It's an automated process that identities potential weakness in the system and networks.
2. Tools - OpenVAS

#### Analysing Scans
1. Identifying true positives(actual and genuine vulnerability) and false positives.
2. Verifying scanner findings and risk associated with it.
3. Questions that need to be asked
	1. What are the potential consequences if the vulnerability if exploited?
	2. What is the likelihood that the vulnerability will be exploited?
	3. What are the possible attack vectors for this vulnerability?
4. Prioritizing vulnerablity based on the potential of impact and likelihood of exploitation.

#### Remediate and Mitigation
1. The time has come to develop the plan to remediate and mitigate the risks associated with them.
Remediation means fixing the vulnerability while mitigation is reducing the likelihood or impact of the vulnerability expected.
2. Strategies that are followed
	1. Patching
	2. Configuration changes
	3. Access Control
	4. Network segmentation
	5. Monitoring and Detection
3. Everything should be documented and well-planned in advance

#### Monitor and Review 
As cyber security posture changes every seconds, it's necessary to update everything to keep things up to date and prevent things from future attack.

---
# VAPT Methodology

### Report and Evidence Collection Tools - Dradis CE
![](Images/Pasted%20image%2020260410194044.png)

### Nmap (network scanning)
Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime.

Syntax - `nmap [Scan Type...] [Options] {target specification}`
![](Images/Pasted%20image%2020260410194330.png)

### OWASP Zap (An Alternative to BurpSuit & Caido)(web scanning)
Zed Attack Proxy (ZAP) by Checkmarx is a free, open-source penetration testing tool. ZAP is designed specifically for testing web applications and is both flexible and extensible.

At its core, ZAP is what is known as a “manipulator-in-the-middle proxy.” It stands between the tester’s browser and the web application so that it can intercept and inspect messages sent between browser and web application, modify the contents if needed, and then forward those packets on to the destination. It can be used as a stand-alone application, and as a daemon process.

![](Images/Pasted%20image%2020260410195314.png)

### Metasploit Framework

 The world’s most used penetration testing framework
 Knowledge is power, especially when it’s shared. A collaboration between the open source community and Rapid7, Metasploit helps security teams do more than just verify vulnerabilities, manage security assessments, and improve security awareness; it empowers and arms defenders to always stay one step (or two) ahead of the game.

![](Images/Pasted%20image%2020260410195358.png)

### [OWASP Web Security Testing Framework](https://owasp.org/www-project-web-security-testing-guide/v42/3-The_OWASP_Testing_Framework/0-The_Web_Security_Testing_Framework)
This section describes a typical testing framework that can be developed within an organization. It can be seen as a reference framework comprised of techniques and tasks that are appropriate at various phases of the software development life cycle (SDLC). Companies and project teams can use this model to develop their own testing framework, and to scope testing services from vendors. This framework should not be seen as prescriptive, but as a flexible approach that can be extended and molded to fit an organization’s development process and culture.

![](Images/Pasted%20image%2020260410203929.png)


### Security Standard & Compliance

There are few standard that come into acions
- [GDPR](https://gdpr-info.eu/)
- [HIPAA](https://www.hhs.gov/hipaa/index.html)
- [ISO27001](https://www.iso.org/standard/27001)
	- The ISO/IEC 27001 standard provides companies of any size and from all sectors of activity with guidance for establishing, implementing, maintaining and continually improving an information security management system.

### Risk Assessment
[NVD CVSS Calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
![](Images/Pasted%20image%2020260410205720.png)
### Common Vulnerabilities

How to identify flaws in labs/tools
1. Network Vulnerabilities - Misconfiguration, open port(can be detected by using Nmap, Nikto)
2. Web Vulnerabilities - OWASP Web Top 10

### Documentation
For Documentation I use Obsidian.
Template
```markdown
# 🛡️ Penetration Testing Assessment Report

**Client:** [Company Name]  
**Date of Report:** [Month DD, YYYY]  
**Assessment Period:** [Start Date] to [End Date]  
**Prepared By:** [Your Name / Consultancy Name]  
**Version:** 1.0  

---

## Table of Contents
1. [Executive Summary](#1-executive-summary)
2. [Scope of Engagement](#2-scope-of-engagement)
3. [Methodology](#3-methodology)
4. [Findings Summary](#4-findings-summary)
5. [Detailed Technical Findings](#5-detailed-technical-findings)
6. [Conclusion](#6-conclusion)
7. [Appendix](#7-appendix)

---

## 1. Executive Summary

### 1.1 Engagement Overview
Between **[Start Date]** and **[End Date]**, **[Consultancy Name]** performed a [White/Grey/Black]-box penetration test against the applications and infrastructure owned by **[Company Name]**. The primary objective was to identify exploitable vulnerabilities and assess the overall security posture of the target environments before malicious threat actors could exploit them.

### 1.2 Risk Posture Statement
Overall, the security posture of the assessed environment is considered **[Excellent / Good / Fair / Poor]**. We identified a total of **[X]** vulnerabilities, including **[X]** Critical and **[X]** High severity issues that require immediate attention.

### 1.3 Key Strategic Recommendations
* **[Recommendation 1]:** Briefly describe the highest impact strategic fix (e.g., Implement Multi-Factor Authentication across all external-facing portals).
* **[Recommendation 2]:** Explain the second major strategic fix (e.g., Institute a regular patch management schedule for all web-facing servers).
* **[Recommendation 3]:** (e.g., Enforce strict input validation on all user-supplied data to prevent injection attacks).

---

## 2. Scope of Engagement

The following assets were explicitly included in the scope of this assessment:

| Asset Type | Target/URL/IP | Description/Role |
| :--- | :--- | :--- |
| Web Application | `https://api.example.com` | Primary Customer API |
| External Network | `192.168.1.0/24` | Public-facing DMZ |
| Credentials | `test_user1`, `test_user2` | Standard user role accounts |

*Note: Any assets not explicitly listed above were considered out of scope.*

---

## 3. Methodology

The assessment was conducted using industry-standard frameworks, aligning closely with the **OWASP Top 10** and the **PTES (Penetration Testing Execution Standard)**. The phases included:
1.  **Reconnaissance & OSINT:** Passive information gathering.
2.  **Vulnerability Scanning:** Automated discovery of known misconfigurations.
3.  **Manual Exploitation:** Verifying false positives and chaining vulnerabilities to demonstrate maximum impact.
4.  **Post-Exploitation:** Assessing the potential for lateral movement and data exfiltration.
5.  **Reporting:** Documenting findings and remediation guidelines.

---

## 4. Findings Summary

The vulnerabilities discovered during the engagement have been classified based on the **CVSS v3.1** scoring system.

| Severity | Count | Definition |
| :--- | :---: | :--- |
| 🔴 **Critical** | **[X]** | Immediate threat to the business. Can be exploited trivially by an unauthenticated attacker. |
| 🟠 **High** | **[X]** | Serious threat. Exploitation could lead to significant data compromise or system takeover. |
| 🟡 **Medium** | **[X]** | Exploitable under specific conditions. May require authenticated access or user interaction. |
| 🔵 **Low** | **[X]** | Minimal direct impact, but could be chained with other vulnerabilities. |
| 🟢 **Info** | **[X]** | Security best practice deviations or informational notes. |

---

## 5. Detailed Technical Findings

> *This section details the specific vulnerabilities identified, including evidence and actionable remediation steps.*

### 🔴 PENTEST-001: [Vulnerability Title, e.g., SQL Injection in Login Portal]

**Severity:** Critical (CVSS: 9.8)  
**Status:** Open  
**Affected Asset:** `https://api.example.com/v1/login`  

#### Description
The application fails to properly sanitize user-supplied input in the `username` parameter of the login endpoint. This allows an attacker to inject arbitrary SQL queries into the backend database, potentially leading to a complete bypass of authentication mechanisms and unauthorized access to sensitive user data.

#### Impact
An attacker can extract, modify, or delete any data within the database. This could lead to a complete compromise of customer PII and administrative credentials.

#### Proof of Concept (PoC)
1. Navigate to the login portal at `https://api.example.com/v1/login`.
2. Intercept the login request using a proxy like Burp Suite.
3. Modify the `username` payload as follows:
   
   ```http
   POST /v1/login HTTP/1.1
   Host: api.example.com
   Content-Type: application/json

   {
     "username": "admin' OR '1'='1",
     "password": "randompassword"
   }
```
