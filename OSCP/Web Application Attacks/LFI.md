##[File Inclusion/Path traversal - HackTricks](https://book.hacktricks.xyz/pentesting-web/file-inclusion#remote-file-inclusion)

The /usr/share/webshells/ has several webshells for RFI
```
kali@kali:**/usr/share/webshells/**php/$ cat simple-backdoor.php
...
```
##Location of all th#

/usr/share/webshells/asp:
cmd-asp-5.1.asp  cmdasp.asp

/usr/share/webshells/aspx:
cmdasp.aspx

/usr/share/webshells/cfm:
cfexec.cfm

/usr/share/webshells/jsp:
cmdjsp.jsp  jsp-reverse.jsp

/usr/share/webshells/perl:
perlcmd.cgi  perl-reverse-shell.pl

/usr/share/webshells/php:
findsocket        php-reverse-shell.php  simple-backdoor.php
php-backdoor.php  qsd-php-backdoor.php

usr/share/webshells/php/findsocket:
findsock.c  php-findsock-shell.php
