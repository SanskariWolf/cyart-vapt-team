HTB Machine - MonitorsFour
Done by: Tanush

## Connecting Hack The Box VPN

Command `sudo openvpn machines_sg-1.ovpn`

![](../../Pasted%20image%2020260411201434.png)

## Starting the Machine
![](../../Pasted%20image%2020260411201519.png)

## Scanning
### Nmap Scap for open ports
Command - `nmap -sC -sV 10.129.22.27`

![](../../Pasted%20image%2020260411202129.png)

Ports open

| Ports    | Services | Version                                 |
| -------- | -------- | --------------------------------------- |
| 80/tcp   | http     | nginx                                   |
| 5985/tcp | http     | Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP) |


Adding domain resolution to /etc/hosts
![](../../Pasted%20image%2020260411202559.png)


![](../../Pasted%20image%2020260411203341.png)

### Enumerating endpoints
Command - `ffuf -u http://monitorsfour.htb/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt`
![](../../Pasted%20image%2020260411204518.png)

Endpoints - `/.env`, `/contact`, `forgot-password`,`/login`, `/user`
Upon checking all the Endpoints manually, '/user' is exploitation to IDOR
![](../../Pasted%20image%2020260411204938.png)

Fiddling out around with it a bit
![](../../Pasted%20image%2020260411205012.png)

Got
`[{"id":2,"username":"admin","email":"admin@monitorsfour.htb","password":"56b32eb43e6f15395f6c46c1c9e1cd36","role":"super user","token":"8024b78f83f102da4f","name":"Marcus Higgins","position":"System Administrator","dob":"1978-04-26","start_date":"2021-01-12","salary":"320800.00"},{"id":5,"username":"mwatson","email":"mwatson@monitorsfour.htb","password":"69196959c16b26ef00b77d82cf6eb169","role":"user","token":"0e543210987654321","name":"Michael Watson","position":"Website Administrator","dob":"1985-02-15","start_date":"2021-05-11","salary":"75000.00"},{"id":6,"username":"janderson","email":"janderson@monitorsfour.htb","password":"2a22dcf99190c322d974c8df5ba3256b","role":"user","token":"0e999999999999999","name":"Jennifer Anderson","position":"Network Engineer","dob":"1990-07-16","start_date":"2021-06-20","salary":"68000.00"},{"id":7,"username":"dthompson","email":"dthompson@monitorsfour.htb","password":"8d4a7e7fd08555133e056d9aacb1e519","role":"user","token":"0e111111111111111","name":"David Thompson","position":"Database Manager","dob":"1982-11-23","start_date":"2022-09-15","salary":"83000.00"}]`

Here we have user and their hashes and we gotta crack the hashes now, from the looks of it, it looks like MD5 hash (from where i identify it, that's call CTF experience)

Cracking the admin hash
![](../../Pasted%20image%2020260411205208.png)
Well CrackStation is a great place to crack the hash rather than bruteforcing
### Enumerating subdomain
Command - `ffuf -u http://monitorsfour.htb -H "Host: FUZZ.monitorsfour.htb" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 138`

![](../../Pasted%20image%2020260411202936.png)

Using ffuf to enumerate the subdomain, I used `-fs 138` cause in previous scan, the whole list was having this size and we look for weird ones, Right? yes it is.

Result - Found a subdomain `cacti`

Adding it to the /etc/hosts

![](../../Pasted%20image%2020260411203546.png)

Finding - `Version 1.2.28 | (c) 2004-2026 - The Cacti Group`

Do this version 1.2.28 of The Cacti Group.
We gotta look for [exploit](https://github.com/Cacti/cacti/security/advisories/GHSA-c7rr-2h93-7gjf)
![](../../Pasted%20image%2020260411203813.png)

Using the credentials we found earlier let's login into the cacti,
`marcus:wonderful1`

Following Poc Steps

Creating new device with the payload
![](../../Pasted%20image%2020260411210633.png)

