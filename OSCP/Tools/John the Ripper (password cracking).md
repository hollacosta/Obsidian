[John The Ripper Hash Formats | pentestmonkey](https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats)

[example_hashes [hashcat wiki]](https://hashcat.net/wiki/doku.php?id=example_hashes)

john [options] [path to file to hash]

john hash2.txt 

john --wordlist=[path to wordlist] [path to file to hash]

john hash2.txt --wordlist=/usr/share/wordlists/rockyou.txt 
''

John is smart enough to detect the type of hash it is given. If you know what hashing algorithm was used you can use the format flag:

john --wordlist=[path to wordlist] --format=[format identifier] [path to file to hash]
if you know the type exact hash you are dealing with

john --format=phpass-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash2.tx

Putting it all together with example values you get the following:

john --wordlist=/usr/share/wordlists/rockyou.txt --format=md5 hash.txt