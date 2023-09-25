


trivera:$apr1$A0vSKwao$GV3sgGAj53j.c3GkS4oUC0
xamps.users information found in github

└─$ host www.megacorpone.com
www.megacorpone.com has address 149.56.244.87

└─$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done | grep "has address"                                         1 ⨯
www.megacorpone.com has address 149.56.244.87
mail.megacorpone.com has address 51.222.169.212
admin.megacorpone.com has address 51.222.169.208
test.megacorpone.com has address 51.222.169.219
vpn.megacorpone.com has address 51.222.169.220
router.megacorpone.com has address 51.222.169.214

┌──(hollacosta㉿kali1)-[~]
└─$ for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"     
200.169.222.51.in-addr.arpa domain name pointer ip200.ip-51-222-169.net.
201.169.222.51.in-addr.arpa domain name pointer ip201.ip-51-222-169.net.
202.169.222.51.in-addr.arpa domain name pointer ip202.ip-51-222-169.net.
203.169.222.51.in-addr.arpa domain name pointer ip203.ip-51-222-169.net.
204.169.222.51.in-addr.arpa domain name pointer ip204.ip-51-222-169.net.

└─$ dnsrecon -d megacorpone.com -t std
/usr/lib/python3/dist-packages/requests/__init__.py:87: RequestsDependencyWarning: urllib3 (1.26.16) or chardet (5.2.0) doesn't match a supported version!
  warnings.warn("urllib3 ({}) or chardet ({}) doesn't match a supported "
[*] std: Performing General Enumeration against: megacorpone.com...
[-] DNSSEC is not configured for megacorpone.com
[*]      SOA ns1.megacorpone.com 51.79.37.18
[*]      NS ns2.megacorpone.com 51.222.39.63
[*]      Bind Version for 51.222.39.63 "9.11.5-P4-5.1+deb10u2-Debian"
[*]      NS ns1.megacorpone.com 51.79.37.18
[*]      Bind Version for 51.79.37.18 "9.11.5-P4-5.1+deb10u2-Debian"
[*]      NS ns3.megacorpone.com 66.70.207.180
[*]      Bind Version for 66.70.207.180 "9.11.5-P4-5.1+deb10u2-Debian"
[*]      MX spool.mail.gandi.net 217.70.178.1
[*]      MX mail.megacorpone.com 51.222.169.212
[*]      MX fb.mail.gandi.net 217.70.178.215
[*]      MX fb.mail.gandi.net 217.70.178.217
[*]      MX fb.mail.gandi.net 217.70.178.216
[*]      MX mail2.megacorpone.com 51.222.169.213
[*]      MX spool.mail.gandi.net 2001:4b98:e00::1
[*]      MX fb.mail.gandi.net 2001:4b98:dc4:8::217
[*]      MX fb.mail.gandi.net 2001:4b98:dc4:8::215
[*]      MX fb.mail.gandi.net 2001:4b98:dc4:8::216
[*]      TXT megacorpone.com Try Harder
[*]      TXT megacorpone.com google-site-verification=U7B_b0HNeBtY4qYGQZNsEYXfCJ32hMNV3GtC0wWq5pA
[*] Enumerating SRV Records

└─$ dnsenum megacorpone.com           
dnsenum VERSION:1.2.6

-----   megacorpone.com   -----                                                                                                   
                                                                                                                                  
                                                                                                                                  
Host's addresses:                                                                                                                 
__________________                                                                                                                
                                                                                                                                  
                                                                                                                                  
                                                                                                                                  
Name Servers:                                                                                                                     
______________                                                                                                                    
                                                                                                                                  
ns1.megacorpone.com.                     202      IN    A        51.79.37.18                                                      
ns2.megacorpone.com.                     202      IN    A        51.222.39.63
ns3.megacorpone.com.                     202      IN    A        66.70.207.180

                                                                                                                                  
Mail (MX) Servers:                                                                                                                
___________________                                                                                                               
                                                                                                                                  
fb.mail.gandi.net.                       60       IN    A        217.70.178.215                                                   
fb.mail.gandi.net.                       60       IN    A        217.70.178.216
fb.mail.gandi.net.                       60       IN    A        217.70.178.217
spool.mail.gandi.net.                    83       IN    A        217.70.178.1
mail2.megacorpone.com.                   203      IN    A        51.222.169.213
mail.megacorpone.com.                    34       IN    A        51.222.169.212

                                                                                                                                  
Trying Zone Transfers and getting Bind Versions:                                                                                  
_________________________________________________                                                                                 
                                                                                                                                  
                                                                                                                                  
Trying Zone Transfer for megacorpone.com on ns1.megacorpone.com ... 
AXFR record query failed: REFUSED

Trying Zone Transfer for megacorpone.com on ns2.megacorpone.com ... 
megacorpone.com.                         300      IN    SOA               (
megacorpone.com.                         300      IN    TXT            "Try
megacorpone.com.                         300      IN    TXT               (
megacorpone.com.                         300      IN    MX               10
megacorpone.com.                         300      IN    MX               20
megacorpone.com.                         300      IN    MX               50
megacorpone.com.                         300      IN    MX               60
megacorpone.com.                         300      IN    NS       ns1.megacorpone.com.
megacorpone.com.                         300      IN    NS       ns2.megacorpone.com.
megacorpone.com.                         300      IN    NS       ns3.megacorpone.com.
admin.megacorpone.com.                   300      IN    A        51.222.169.208
beta.megacorpone.com.                    300      IN    A        51.222.169.209
fs1.megacorpone.com.                     300      IN    A        51.222.169.210
intranet.megacorpone.com.                300      IN    A        51.222.169.211
mail.megacorpone.com.                    300      IN    A        51.222.169.212
mail2.megacorpone.com.                   300      IN    A        51.222.169.213
ns1.megacorpone.com.                     300      IN    A        51.79.37.18
ns2.megacorpone.com.                     300      IN    A        51.222.39.63
ns3.megacorpone.com.                     300      IN    A        66.70.207.180
router.megacorpone.com.                  300      IN    A        51.222.169.214
siem.megacorpone.com.                    300      IN    A        51.222.169.215
snmp.megacorpone.com.                    300      IN    A        51.222.169.216
support.megacorpone.com.                 300      IN    A        51.222.169.218
syslog.megacorpone.com.                  300      IN    A        51.222.169.217
test.megacorpone.com.                    300      IN    A        51.222.169.219
vpn.megacorpone.com.                     300      IN    A        51.222.169.220
www.megacorpone.com.                     300      IN    A        149.56.244.87
www2.megacorpone.com.                    300      IN    A        149.56.244.87

Trying Zone Transfer for megacorpone.com on ns3.megacorpone.com ... 
AXFR record query failed: REFUSED





