# First make hash from zip file
/usr/sbin/zip2john [FILE.ZIP] > [HASH_NAME]
# Attack hash with wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt [HASH_NAME]

# EXAMPLE
/usr/sbin/zip2john cyber.zip > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
