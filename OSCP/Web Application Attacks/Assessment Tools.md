[Web API Pentesting - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/web-api-pentesting)
### **NMAP**

sudo nmap -p80  -sV 192.168.50.20
sudo nmap -p80 --script=http-enum 192.168.50.20
sudo nmap -p80 --script=http-enum 192.168.50.20

$ ls -l /usr/share/nmap/scripts/http*                                     ----to see all the http scripts

### **WAPPALYZER**

https://www.wappalyzer.com/

### **Gobuster!**


[Gobuster CheatSheet - 3os](https://3os.org/penetration-testing/cheatsheets/gobuster-cheatsheet/#dns-mode)


gobuster dir -u 192.168.50.20 -w /usr/share/wordlists/dirb/common.txt -t 5

### **BURPSUITE**

┌──(hollacosta㉿kali1)-[~]
└─$ burpsuite                                                                                       ---- to start the app
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Your JRE appears to be version 17.0.9-ea from Debian
Burp has not been fully tested on this platform and you may experience problems.



