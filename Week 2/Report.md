# Practical

## 1. Vulnerability Scanning
### Nikto Scan
![](../Week%201/Images/Pasted%20image%2020260410153741.png)
```
└─$ nikto -h http://172.28.128.3
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          172.28.128.3
+ Target Hostname:    172.28.128.3
+ Target Port:        80
+ Start Time:         2026-03-10 15:36:53 (GMT5.5)
---------------------------------------------------------------------------
+ Server: Apache/2.4.7 (Ubuntu)
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /: Directory indexing found.
+ Apache/2.4.7 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ OPTIONS: Allowed HTTP Methods: GET, HEAD, POST, OPTIONS .
+ /./: Directory indexing found.
+ /./: Appending '/./' to a directory allows indexing.
+ //: Directory indexing found.
+ //: Apache on Red Hat Linux release 9 reveals the root directory listing by default if there is no index page.
+ /%2e/: Directory indexing found.
+ /%2e/: Weblogic allows source code or directory listing, upgrade to v6.0 SP1 or higher. See: http://www.securityfocus.com/bid/2513
+ ///: Directory indexing found.
+ /?PageServices: The remote server may allow directory listings through Web Publisher by forcing the server to show all files via 'open directory browsing'. Web Publisher should be disabled. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-0269
+ /?wp-cs-dump: The remote server may allow directory listings through Web Publisher by forcing the server to show all files via 'open directory browsing'. Web Publisher should be disabled. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-0269
+ /phpmyadmin/changelog.php: Retrieved x-powered-by header: PHP/5.4.5.
+ /phpmyadmin/ChangeLog: phpMyAdmin is for managing MySQL databases, and should be protected or limited to authorized hosts.
+ ///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////: Directory indexing found.
+ ///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////: Abyss 1.03 reveals directory listing when multiple /'s are requested. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2002-1078
+ /icons/README: Apache default file found. See: https://www.vntweb.co.uk/apache-restricting-access-to-iconsreadme/
+ /phpmyadmin/: phpMyAdmin directory found.
+ /phpmyadmin/Documentation.html: phpMyAdmin is for managing MySQL databases, and should be protected or limited to authorized hosts.
+ /phpmyadmin/README: phpMyAdmin is for managing MySQL databases, and should be protected or limited to authorized hosts. See: https://typo3.org/
+ 8911 requests: 0 error(s) and 22 item(s) reported on remote host
+ End Time:           2026-03-10 15:37:03 (GMT5.5) (10 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

### Nmap Scan
![](../Week%201/Images/Pasted%20image%2020260410154149.png)
```
Nmap scan report for 172.28.128.3
Host is up (0.00027s latency).
Not shown: 991 filtered tcp ports (no-response)
PORT     STATE  SERVICE     VERSION
21/tcp   open   ftp         ProFTPD 1.3.5
22/tcp   open   ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 2b:2e:1f:a4:54:26:87:76:12:26:59:58:0d:da:3b:04 (DSA)
|   2048 c9:ac:70:ef:f8:de:8b:a3:a3:44:ab:3d:32:0a:5c:6a (RSA)
|   256 c0:49:cc:18:7b:27:a4:07:0d:2a:0d:bb:42:4c:36:17 (ECDSA)
|_  256 a0:76:f3:76:f8:f0:70:4d:09:ca:e1:10:fd:a9:cc:0a (ED25519)
80/tcp   open   http        Apache httpd 2.4.7
|_http-server-header: Apache/2.4.7 (Ubuntu)
| http-ls: Volume /
| SIZE  TIME              FILENAME
| -     2020-10-29 19:37  chat/
| -     2011-07-27 20:17  drupal/
| 1.7K  2020-10-29 19:37  payroll_app.php
| -     2013-04-08 12:06  phpmyadmin/
|_
|_http-title: Index of /
445/tcp  open   netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
631/tcp  open   ipp         CUPS 1.7
|_http-title: Home - CUPS 1.7.2
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: CUPS/1.7 IPP/2.1
| http-methods: 
|_  Potentially risky methods: PUT
3000/tcp closed ppp
3306/tcp open   mysql       MySQL (unauthorized)
8080/tcp open   http        Jetty 8.1.7.v20120910
|_http-server-header: Jetty(8.1.7.v20120910)
|_http-title: Error 404 - Not Found
8181/tcp closed intermapper
MAC Address: 08:00:27:BC:69:04 (Oracle VirtualBox virtual NIC)
Service Info: Hosts: 127.0.1.1, UBUNTU; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-time: 
|   date: 2026-03-10T10:10:22
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: metasploitable3-ub1404
|   NetBIOS computer name: UBUNTU\x00
|   Domain name: \x00
|   FQDN: metasploitable3-ub1404
|_  System time: 2026-03-10T10:10:24+00:00
|_clock-skew: mean: 1s, deviation: 2s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.29 seconds
```

## Risk Assessment
| **Ref ID**   | **Port** | **Service**   | **Vulnerability**                        | **CVSS 3.1** | **Priority** |
| ------------ | -------- | ------------- | ---------------------------------------- | ------------ | ------------ |
| **VULN-001** | 21       | ProFTPD 1.3.5 | **Unauthenticated File Copy (mod_copy)** | 10           | **Critical** |
| **VULN-002** | 80       | Apache 2.4.7  | **Outdated Web Server (Multiple CVEs)**  | 7.5          | **High**     |
| **VULN-003** | 80       | HTTP          | **Directory Indexing Enabled**           | 5.3          | **Medium**   |
| **VULN-004** | 445      | Samba 4.3.11  | **SMB Signing Disabled**                 | 5.1          | **Medium**   |
| **VULN-005** | 3306     | MySQL         | **Unauthorized Access Attempt**          | 9.8          | **Critical** |

#### Developer Escalation Email
```
I identified a critical flaw (CVE-2015-3306) on the Ubuntu staging server (172.28.128.3). The ProFTPD 1.3.5 service allows unauthenticated users to copy arbitrary files to the webroot via the `mod_copy` module.

**PoC:** Using `SITE CPFR /etc/passwd` and `SITE CPTO /var/www/html/out.txt`, I successfully moved system files to the public web directory. This enables Remote Code Execution (RCE).

**Recommendation:** Immediately upgrade ProFTPD to v1.3.6 or disable `mod_copy`.
```

## 2. Reconnaissance Practice

Looking for services
### Shodan
![](Images/Pasted%20image%2020260410162255.png)

| **Timestamp**    | **Tool**   | **Finding**                                            |
| ---------------- | ---------- | ------------------------------------------------------ |
| 2026-03-10 16:10 | Shodan     | Found 11.097+ hosts running ProFTPD 1.3.5 globally.    |

## 3. Exploitation Lab 

**ProFTPD** vulnerability on Ubuntu machine (`172.28.128.3`) | **CVE-2015-3306**

Using MetaSploit
![](Images/Pasted%20image%2020260410163602.png)

##### Summary
Used Metasploit to epxloit ProFTPD** vulnerability with PoC of CVE-2015-3306


## 4. Post-Exploitation Practice

### 1. Host Information & Access Details

- **Target IP:** `172.28.128.3`    
- **Initial Access Vector:** Exploitation of ProFTPD 1.3.5 (mod_copy)
- **Access Level:** `www-data` (uid=33, gid=33)
- **Session Established:** 2026-04-10 16:33:54 +0530
![](Images/Pasted%20image%2020260410164418.png)
### 2. Evidence Collection & Data Exfiltration

During the post-exploitation phase, multiple sensitive files were accessed and analyzed to confirm the impact of the breach.

#### A. System User Enumeration

Analysis of `/etc/passwd` reveals a significant attack surface, including a local administrative user (`vagrant`) and several service accounts.
- **SHA256 Hash of `/etc/passwd`:** `9322b81652626c9f04d3e6d192a8fa2525b5e5d5113d6777deddb023fa887b97`
- **Notable Local Users:** `vagrant`, `mysql`, `han_solo`, `luke_skywalker`, `leia_organa`.   
![](Images/Pasted%20image%2020260410164451.png)
#### B. Database Credential Leakage

Sensitive application source code was audited, revealing hardcoded database credentials used across multiple platforms on the host.
![](Images/Pasted%20image%2020260410164607.png)

| **Application** | **File Path**                       | **DB Username** | **DB Password** | **Database Name** |
| --------------- | ----------------------------------- | --------------- | --------------- | ----------------- |
| **Payroll App** | `/var/www/html/payroll_app.php`     | `root`          | `sploitme`      | `payroll`         |
| **Drupal CMS**  | `drupal/sites/default/settings.php` | `root`          | `sploitme`      | `drupal`          |

**Security Concern:** The use of the `root` database user with a shared password (`sploitme`) across different applications represents a critical configuration failure, allowing for lateral movement within the database management system.

### . Risk Assessment (3x3 Matrix)

| **Finding**                     | **Likelihood** | **Impact** | **Overall Risk** |
| ------------------------------- | -------------- | ---------- | ---------------- |
| **RCE via ProFTPD**             | High           | High       | **CRITICAL**     |
| **Hardcoded DB Credentials**    | High           | High       | **CRITICAL**     |
| **Cleartext Password Exposure** | Medium         | High       | **HIGH**         |

### . Remediation Recommendations

1. **Immediate:** Patch ProFTPD to version 1.3.6+ or disable `mod_copy`.
2. **Configuration:** Change the MySQL `root` password immediately and create low-privileged users for specific applications.
3. **Code Security:** Refactor `payroll_app.php` to use **Prepared Statements** to prevent SQL Injection.
4. **Filesystem:** Restrict the `www-data` user's read permissions to prevent access to `/etc/passwd` and other sensitive configuration files.


# CapStone Project: Full VAPT Cycle

### Simulation: SQL Injection with `sqlmap`

payroll_app.php
![](Images/Pasted%20image%2020260410165106.png)

From the understanding the code, I got to know it's vulnerable to SQLi
using sqlmap to exploit it

![](Images/Pasted%20image%2020260410165216.png)- **Result:** `sqlmap` confirmed the `user` parameter was vulnerable to **UNION query** and **Time-based blind** injection.
![](Images/Pasted%20image%2020260410165532.png)

#### PTES
```
This assessment followed the PTES framework to evaluate the security posture of the Ubuntu-based Metasploitable3 environment. Following initial reconnaissance that identified an outdated Apache/2.4.7 web server, a focused manual audit was conducted on the 'Payroll' application. The audit uncovered a critical SQL Injection flaw within the authentication logic.

Automated exploitation using `sqlmap` successfully bypassed the login mechanism and facilitated a full database dump of the 'payroll' schema. The exfiltrated data included cleartext usernames and sensitive salary figures, proving a total loss of data confidentiality. This vulnerability exists because the application uses raw SQL queries rather than prepared statements, allowing malicious input to manipulate the database engine.

Furthermore, during the exploitation phase, a secondary Remote Code Execution (RCE) was achieved via ProFTPD 1.3.5, which allowed for unauthorized file system access. The combination of these flaws demonstrates a significant risk where an unauthenticated attacker could transition from web-layer exploitation to full server compromise. Remediation requires the immediate implementation of parameterized queries across all PHP modules and a comprehensive patch management cycle to address the underlying outdated service versions.
```

#### Non-Technical Summary
```
Our security test successfully simulated a real-world cyberattack on the company’s internal payroll system. We discovered that the system’s defenses are easily bypassed due to a common coding error known as 'SQL Injection.' Without needing any passwords, we were able to download the entire database, including employee names and salary information.

Because the server software is also several years out of date, a hacker could take full control of the entire machine. To protect our data, we must update the server software immediately and retrain developers to use secure coding methods that block these types of attacks.
```

