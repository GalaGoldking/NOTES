# Username Enumaration
ffuf -w [wordlist] -X [method] -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u [URL] -mr "[output message]"

ffuf -w /usr/share/wordlists/seclists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=geb@gmail.com&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http(s)://domain.com -mr "An account with this username already exists" -t 300
# DNS bruteforce
ffuf -w [wordlist] -H "Host: FUZZ.[URL]" -u [URL]

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.domain.com" -w http(s)://domain.com -t 300
<h3>Exclude file size</h3>
ffuf -w [wordlist] -H "Host: FUZZ.[URL]" -u [URL] -fs [file size]

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.domain.com" -u [URL] -fs 2222
