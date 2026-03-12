
# 1. Setup Testing Environment

### Kali Linux Already installed (Already Installed)
![](Images/Pasted%20image%2020260410141145.png)

### [Metasploitable 3 Installation](https://github.com/rapid7/metasploitable3?tab=readme-ov-file#building-metasploitable-3)
First Install all these
```
Requirements:

- [Packer](https://www.packer.io/intro/getting-started/install.html)
- [Vagrant](https://www.vagrantup.com/docs/installation/)
- [Vagrant Reload Plugin](https://github.com/aidanns/vagrant-reload#installation)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads), libvirt/qemu-kvm, or vmware (paid license required), or parallels (paid license required)
```
#### Packer
- `└─$ curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg`
- `└─$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com bookworm main" | sudo tee /etc/apt/sources.list.d/hashicorp.list`
- `└─$ sudo apt-get update                                      `
- `└─$ sudo apt-get install packer`

![](Images/Pasted%20image%2020260410152709.png)
#### Vagrant
- `└─$ curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor --yes -o /usr/share/keyrings/hashicorp-archive-keyring.gpg`
- `└─$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com bookworm main" | sudo tee /etc/apt/sources.list.d/hashicorp.list`
- `└─$ sudo apt update`
- `sudo apt install vagrant`

![](Images/Pasted%20image%2020260410153003.png)
#### Virtual Box Installation
- `└─$ sudo apt install -y virtualbox virtualbox-ext-pack virtualbox-dkms`
![](Images/Pasted%20image%2020260410153412.png)
#### Metasploit 3
- `curl -O https://raw.githubusercontent.com/rapid7/metasploitable3/master/Vagrantfile && vagrant up`
![](Images/Pasted%20image%2020260410151326.png)
## 2. Vulnerability Scanning
### Nikto Scan
![](Images/Pasted%20image%2020260410153741.png)
```
└─$ nikto -h http://172.28.128.3
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          172.28.128.3
+ Target Hostname:    172.28.128.3
+ Target Port:        80
+ Start Time:         2026-04-10 15:36:53 (GMT5.5)
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
+ End Time:           2026-04-10 15:37:03 (GMT5.5) (10 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

### Nmap Scan
![](Images/Pasted%20image%2020260410154149.png)
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
|   date: 2026-04-10T10:10:22
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
|_  System time: 2026-04-10T10:10:24+00:00
|_clock-skew: mean: 1s, deviation: 2s, median: 0s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.29 seconds
```

### OpenVAS Scan
![](Images/Pasted%20image%2020260410222740.png)

## 3. Documentation of Findings
| **Ref ID**   | **Port** | **Service**   | **Vulnerability**                        | **CVSS 3.1** | **Priority** |
| ------------ | -------- | ------------- | ---------------------------------------- | ------------ | ------------ |
| **VULN-001** | 21       | ProFTPD 1.3.5 | **Unauthenticated File Copy (mod_copy)** | 10           | **Critical** |
| **VULN-002** | 80       | Apache 2.4.7  | **Outdated Web Server (Multiple CVEs)**  | 7.5          | **High**     |
| **VULN-003** | 80       | HTTP          | **Directory Indexing Enabled**           | 5.3          | **Medium**   |
| **VULN-004** | 445      | Samba 4.3.11  | **SMB Signing Disabled**                 | 5.1          | **Medium**   |
| **VULN-005** | 3306     | MySQL         | **Unauthorized Access Attempt**          | 9.8          | **Critical** |

### Risk Findings
| **Vulnerability**           | **CVSS Score** | **Impact** | **Likelihood** | **Risk Category** |
| --------------------------- | -------------- | ---------- | -------------- | ----------------- |
| **ProFTPD 1.3.5 mod_copy**  | 10             | High       | High           | **CRITICAL**      |
| **Outdated Apache 2.4.7**   | 7.5            | High       | Medium         | **HIGH**          |
| **Directory Indexing**      | 5.3            | Medium     | High           | **MEDIUM**        |
| **Samba Signing Disabled**  | 5.1            | Medium     | Medium         | **MEDIUM**        |
| **Missing X-Frame-Headers** | 3.5            | Low        | Low            | **LOW**           |


##### Calculation of CVSS Score (**ProFTPD 1.3.5 mod_copy**)
![](Images/Pasted%20image%2020260410155010.png)
