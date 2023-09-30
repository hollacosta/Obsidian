
[80,443 - Pentesting Web Methodology - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web)

[80,443 - Pentesting Web Methodology - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web#initial-checks) -INITIAL CHECKS

### INSPECTION

Use the inspect option to see valuable HTML information

![[Pasted image 20230927075239.png]]
Debugger options gives use the Jquery Syntax (use the pretty print source option)

![[Pasted image 20230927075343.png]]
use the network tab to inspect Headers from the page

**CURL**
use curl to get information from the page 
┌──(hollacosta㉿kali1)-[~]
└─$ curl https://www.google.com/robots.txt
User-agent: *
Disallow: /search

### ENUMERATING APIS

**Initial checks**

**Default pages with interesting info:**
- /robots.txt    
- /sitemap.xml 
- /crossdomain.xml 
- /clientaccesspolicy.xml    
- /.well-known/
- Check also comments in the main and secondary pages.

Create pattern wordlist

┌──(hollacosta㉿kali1)-[~]
└─$ gobuster dir -u http://192.168.202.16:5002 -w /usr/share/wordlists/dirb/big.txt -p pattern                                                                                               ----to find patterns


