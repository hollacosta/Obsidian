As an additional note, the way Module exercises are implemented allows us to use the same remote IP and port multiple times. On the Module Exercise VMs that require an SSH connection, we suggest issuing the SSH command with a couple of extra options as follows:

```
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" learner@192.168.50.52
```

https://github.com/OWASP/wstg/tree/master/document/4-Web_Application_Security_Testing
Important information for Web Application Security Testing

	ls -lh /usr/bin
	# a list where all my commands are located

Chmod Cheat Sheet
![[Pasted image 20230924101458.png]]

A GENERAL PENETRATION TEST comprises the following stages:

- Defining the Scope
- Information Gathering
- Vulnerability Detection
- Initial Foothold
- Privilege Escalation
- Lateral Movement
- Reporting/Analysis
- Lessons Learned/Remediation

**SETTING UP A LISTENER FOR THE TARGET MACHINE TO SEE DATA SIZE IN IPTABLES**
┌──(hollacosta㉿kali1)-[~]
└─$ sudo iptables -I OUTPUT 1 -d **192.168.234.52** -j ACCEPT
┌──(hollacosta㉿kali1)-[~]
└─$ sudo iptables -I INPUT 1 -s **192.168.234.52** -j ACCEPT     


****FIREFOX SETTINGS FOR BURPSUITE
![[Pasted image 20230926204532.png]]

Always check your working directory when you are trying to do some commands


for remotedesktop use **xfreerdp or rdesktop**

