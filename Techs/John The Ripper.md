# Usage
john --wordlist=/usr/share/wordlists/rockyou.txt -format=[SELECT FORMAT] [HASH_FILE]

# Example
john --wordlist=/usr/share/wordlists/rockyou.txt -format=raw-sha256 hash

# Crack zip 
First we make a hash out of zip file <br>
/usr/sbin/zip2john [FILE.ZIP] > [HASH_FILE]

# Attack hash with wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt [HASH_FILE]
