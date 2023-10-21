1. **MD5 Hash Mode**:
    
    - Hash Mode: `-m 0` (MD5)
    - Hash File: `hashes.txt`
    - Wordlist: `rockyou.txt`
    - Example Command:
        
        Copy code
        
        `hashcat -m 0 hashes.txt rockyou.txt`
        
2. **SHA-256 Hash Mode**:
    
    - Hash Mode: `-m 1400` (SHA-256)
    - Hash File: `sha256_hashes.txt`
    - Wordlist: `common-passwords.txt`
    - Example Command:
        
        yamlCopy code
        
        `hashcat -m 1400 sha256_hashes.txt common-passwords.txt`
        
3. **bcrypt Hash Mode**:
    
    - Hash Mode: `-m 3200` (bcrypt)
    - Hash File: `bcrypt_hashes.txt`
    - Wordlist: `top1000-passwords.txt`
    - Example Command:
        
        yamlCopy code
        
        `hashcat -m 3200 bcrypt_hashes.txt top1000-passwords.txt`
        
4. **Rule-Based Attack**:
    
    - Hash Mode: `-m 1000` (NTLM)
    - Hash File: `ntlm_hashes.txt`
    - Wordlist: `custom-wordlist.txt`
    - Rule File: `best64.rule`
    - Example Command:
        
        vbnetCopy code
        
        `hashcat -m 1000 ntlm_hashes.txt custom-wordlist.txt -r best64.rule`
        
5. **Combination Attack**:
    
    - Hash Mode: `-m 1000` (NTLM)
    - Hash File: `ntlm_hashes.txt`
    - Wordlist 1: `common-passwords.txt`
    - Wordlist 2: `custom-wordlist.txt`
    - Example Command:
        
        cssCopy code
        
        `hashcat -m 1000 ntlm_hashes.txt -a 1 common-passwords.txt custom-wordlist.txt`
        
6. **Mask Attack**:
    
    - Hash Mode: `-m 0` (MD5)
    - Hash File: `md5_hashes.txt`
    - Mask Attack: Trying all 6-character alphanumeric combinations
    - Example Command:
        
        cssCopy code
        
        `hashcat -m 0 md5_hashes.txt -a 3 ?a?a?a?a?a?a`
        
7. **Incremental Mode**:
    
    - Hash Mode: `-m 1800` (WPA/WPA2)
    - Hash File: `wifi-hashes.hccapx`
    - Incremental Attack: Trying all possible combinations
    - Example Command:
        
        cssCopy code
        
        `hashcat -m 1800 wifi-hashes.hccapx -a 6`
        
8. **Performance Tuning**:
    
    - Hash Mode: `-m 1000` (NTLM)
    - Hash File: `ntlm_hashes.txt`
    - Wordlist: `common-passwords.txt`
    - Workload Profile: High-speed attack (Workload 4) with optimized kernels
    - Example Command:
        
        mathematicaCopy code
        
        `hashcat -m 1000 ntlm_hashes.txt common-passwords.txt -w 4 -O`
        

These are just examples, and you should replace the file names and hash modes with the actual values you have for your penetration testing engagement. Always ensure you have the proper authorization to perform password cracking.

hashcat --help | grep -i "KeePass" to find the hashcat type!

[rule_based_attack [hashcat wiki]](https://hashcat.net/wiki/doku.php?id=rule_based_attack)

to see the rules needed for it 

THERE ARE RULES ALREADY PREDETERMINED! FOR A FULL LIST, GO TO 
/usr/share/hashcat/rules/

![[Pasted image 20231021060313.png]]

