[Web API Pentesting - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/web-api-pentesting)

**NMAP**

sudo nmap -p80  -sV 192.168.50.20
sudo nmap -p80 --script=http-enum 192.168.50.20
sudo nmap -p80 --script=http-enum 192.168.50.20

$ ls -l /usr/share/nmap/scripts/http*                                     ----to see all the http scripts

**WAPPALYZER**

https://www.wappalyzer.com/

**Gobuster!**

gobuster dir -u 192.168.50.20 -w /usr/share/wordlists/dirb/common.txt -t 5


