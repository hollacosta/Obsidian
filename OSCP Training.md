As an additional note, the way Module exercises are implemented allows us to use the same remote IP and port multiple times. On the Module Exercise VMs that require an SSH connection, we suggest issuing the SSH command with a couple of extra options as follows:

```
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no" learner@192.168.50.52
```

https://github.com/OWASP/wstg/tree/master/document/4-Web_Application_Security_Testing
Important information for Web Application Security Testing

	ls -lh /usr/bin
	# a list where all my commands are located

