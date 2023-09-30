
**PASSIVE INFORMATION GATHERING** - CHECK FAVORITES TAB

- -   
     1.1.1. Whois Enumeration
    - 1.1.2. Google Hacking
    - 1.1.3. Netcraft
    - 1.1.4. Open-Source Code
    - 1.1.5. Shodan
    - 1.1.6. Security Headers and SSL/TLS

[Ultimate OSINT with Shodan: 100+ great Shodan queries – osintme.com](https://www.osintme.com/index.php/2021/01/16/ultimate-osint-with-shodan-100-great-shodan-queries/)

[Search Web by Domain | Netcraft](https://searchdns.netcraft.com/)
# **Whois**: Provides information about a domain name and registar.

[43 - Pentesting WHOIS - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/43-pentesting-whois)

PORT 43
whois -h <HOST> -p <PORT> "domain.tld"

echo "domain.ltd" | nc -vn <HOST> <PORT>

**SQL INJECTION ON WHOIS**

whois -h 10.10.10.155 -p 43 "a') or 1=1#"

**SHODAN**
port:43 whois


**IF DIFFERENT PORT (KNOWN)**
whois -p 4343 example.com

### **GOOGLE HACKING**

[External Recon Methodology - HackTricks](https://book.hacktricks.xyz/generic-methodologies-and-resources/external-recon-methodology#google-dorks)

[Google Hacking Database (GHDB) - Google Dorks, OSINT, Recon (exploit-db.com)](https://www.exploit-db.com/google-hacking-database)

1. **site:** - Limits search results to a specific website or domain    
    Example: `site:example.com`
2. **filetype:** - Searches for specific file types or extensions.
    Example: `filetype:pdf confidential`
3. **intitle:** - Finds web pages with specific words in their titles    
    Example: `intitle:"login page"` 
4. **inurl:** - Locates web pages with specific words in their URLs.
    Example: `inurl:admin` 
5. **intext:** - Searches for pages with specific text in their content.  
    Example: `intext:password` 
6. **cache:** - Shows Google's saved version of a web page. 
    Example: `cache:example.com`  
7. **link:** - Finds pages that link to a specific URL. 
    Example: `link:example.com`
8. **related:** - Identifies websites related to a given domain. 
    Example: `related:example.com`
9. **ext:** - Searches for specific file extensions.
    Example: `ext:conf OR ext:ini`
10. **info:** - Retrieves information about a domain.
    Example: `info:example.com`

**https://searchdns.netcraft.com**
Netcraft is a company known for its internet security and research services, including website analysis and monitoring.

Shodan.io

[Special HTTP headers - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/special-http-headers)
















