
DNS

make sure you put the www in the website. see example below

┌──(hollacosta㉿kali1)-[~]
└─$ host megacorpcone.com
Host megacorpcone.com not found: 3(NXDOMAIN)

┌──(hollacosta㉿kali1)-[~]
└─$ host www.megacorpone.com                                             1 ⨯
www.megacorpone.com has address 149.56.244.87

Create a list of the possible hostnames
└─$ cat list.txt 
1. www
2. mail
3. ftp
4. admin
5. test
6. vpn
7. portal
8. exchange
9. router
10. api
11. webmail
12. database
13. git
14. login
15. ssh
16. backup
17. proxy
18. remote
19. monitoring
20. cloud


└─$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 149.56.244.87
Host ftp.megacorpone.com not found: 3(NXDOMAIN)
mail.megacorpone.com has address 51.222.169.212
Host owa.megacorpone.com not found: 3(NXDOMAIN)
Host proxy.megacorpone.com not found: 3(NXDOMAIN)
router.megacorpone.com has address 51.222.169.214

USING GREP TO JUST IDENTIFY THE ONES THAT ARE GOOD
└─$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done | grep "has address"                                                                   1 ⨯
www.megacorpone.com has address 149.56.244.87
mail.megacorpone.com has address 51.222.169.212
admin.megacorpone.com has address 51.222.169.208
test.megacorpone.com has address 51.222.169.219
vpn.megacorpone.com has address 51.222.169.220
router.megacorpone.com has address 51.222.169.214

for ip in $(seq 200 254); do host 51.222.169.$ip; done | grep -v "not found"
the ip bash loops in the ips 200-254 and is placed with the $

DNS RECON
the strongest parameters you can consider using:

1. **-d (Domain)**: Specify the target domain name to perform DNS reconnaissance on.
2. **-t (Type)**: Choose the type of DNS enumeration you want to perform. Common options include standard (A, AAAA, MX, NS, SOA, TXT, SRV), reverse (PTR), brute force (bruteforce), and more.
3. **-D (Dictionary File)**: Provide a custom wordlist or dictionary file for DNS brute forcing. A strong wordlist can significantly impact the effectiveness of brute force enumeration.
4. **-r (Range)**: Define a specific IP address range to scan for reverse DNS lookups.
5. **-c (Concurrency)**: Set the number of concurrent DNS queries to perform, which can speed up the enumeration process.
6. **-p (Port)**: Specify the DNS server port to query. The default is 53, but some DNS servers may use non-standard ports.
7. **-T (Thread Count)**: Configure the number of threads to use for DNS queries. Increasing this value can help speed up the enumeration process but be cautious not to overload DNS servers.
8. **-e (Exit After)**: Set a time limit (in seconds) for how long DNSRecon should continue its enumeration before exiting. 
9. **-j (JSON Output)**: Save the results in JSON format for easier parsing and analysis. 
10. **-z (Brute Force Reverse Lookup)**: Enable brute-force reverse DNS lookups, which can reveal additional hostnames associated with IP addresses.  
11. **-P (Permutations)**: Generate permutations of the domain name to discover potential subdomains.
12. **-D (DNS Servers)**: Specify a list of DNS servers to use for querying. This can help you test different DNS servers for the same domain.
13. **-w (Write to File)**: Save the results to a text file for later analysis.
14. **-f (Full Results)**: Display full results, including records with empty fields. 
15. **-R (Recurse)**: Recursively enumerate subdomains, allowing for deeper exploration    
16. **-n (No Recursion)**: Disable recursive querying to avoid hitting authoritative DNS servers.  
17. **-C (Cache Snooping)**: Attempt to retrieve cached DNS records from the target server.
    
18. **-A (All)**: Combine multiple types of enumeration (e.g., standard, reverse, brute force) in a single scan.


**NMAP**
──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -sS 192.168.234.52                                                  ---- STEALTH SCAN

┌──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -sT 192.168.234.52
Starting Nmap 7.91 ( https://nmap.org ) at 2023-09-25 06:57 EDT ---- TCP FULL CONNECT SCAN

┌──(hollacosta㉿kali1)-[~]
└─$ sudo nmap -sU 192.168.234.52                                                 ---- UDP Scan


