[SQLMap - Cheetsheat - HackTricks](https://book.hacktricks.xyz/pentesting-web/sql-injection/sqlmap)
[MySQL injection - HackTricks](https://book.hacktricks.xyz/pentesting-web/sql-injection/mysql-injection)

MySQL and Microsoft SQL Server (MSSQL) most common
Identify the port using NMAP

### MYSQL
sudo nmap -T5 --top-ports=500 -sS 192.168.238.16

Nmap scan report for 192.168.238.16
Host is up (0.045s latency).
Not shown: 496 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
3306/tcp open  mysql              ----HERE IS THE PORT #
8000/tcp open  http-alt
8080/tcp open  http-proxy

After seeing the port, go to mysql if username/password provided

$ mysql -u root **-p'root'** -h 192.168.238.16 -P 3306
**(-p = Password)  (-P= Port)**

MySQL [(none)]> 

SIMPLE VERSION/SYSTEM AND DATABASE INFO
-MySQL [(none)]> select version ();
+------------+
| version () |
+------------+
| 8.0.21     |
+------------+
-MySQL [(none)]> select system_user();
+---------------------+
| system_user()       |
+---------------------+
| root@192.168.45.181 |
+---------------------+
-MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+

Sample of using finding an authentication string from an user
![[Pasted image 20230930080712.png]]

### MSSQL 
Impacket
Run Nmap to identify the service
┌──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -T5 --top-ports=500 -sS 192.168.238.18                      
PORT     STATE SERVICE
53/tcp   open  domain
80/tcp   open  http
88/tcp   open  kerberos-sec
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
389/tcp  open  ldap
445/tcp  open  microsoft-ds
464/tcp  open  kpasswd5
593/tcp  open  http-rpc-epmap
636/tcp  open  ldapssl
**1433/tcp open  ms-sql-s**    -------HERE IS MSSQL
3268/tcp open  globalcatLDAP
3269/tcp open  globalcatLDAPssl

└─$ impacket-mssqlclient Administrator:Lab123@192.168.238.18 -windows-auth
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation


Encryption required, switching to TLS
 ENVCHANGE(DATABASE): Old Value: master, New Value: master
 ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
INFO(SQL01\SQLEXPRESS): Line 1: Changed database context to 'master'.
 INFO(SQL01\SQLEXPRESS): Line 1: Changed language setting to us_english.
ACK: Result: 1 - Microsoft SQL Server (150 7208) 
 Press help for extra shell commands
SQL> 

SQL> SELECT @@version;
Microsoft SQL Server 2019 (RTM) - 15.0.2000.5 (X64) 
        Sep 24 2019 13:48:23 
        Copyright (C) 2019 Microsoft Corporation
        Express Edition (64-bit) on Windows Server 2022 Standard 10.0 Build 20348: ) (Hypervisor)

SQL> SELECT name FROM sys.databases; -SHOWS DBS
name                                                                                         
master                                                                                       
tempdb                                                                                      
model                                                                                                
SQL> select * from offsec.dbo.users;    ---INFO ABOUT DB
username     password     

admin        lab          

guest        guest      

### DID IT WORK?







