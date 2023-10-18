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

### 14.3.3 Capstone Exercise

![[Pasted image 20231017202017.png]]


![[Pasted image 20231017202440.png]]
Download the 32 .exe file
