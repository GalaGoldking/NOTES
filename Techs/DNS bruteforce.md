# ffuf 
ffuf -w [wordlist] -H "HOST: FUZZ.[URL]" -u [URL] 

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.domain.com" -u http(s)://domain.com -t 300

# exclude specific file size
ffuf -w [wordlist] -H "HOST: FUZZ.[URL]" -u [URL] -fs [file size]

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: Fuzz.domain.com" -u http(s)://domain.com -t 300 -fs 2395
# gobuster
gobuster vhost -u [URL] -w [wordlist] --no-error --append-domain

gobuster vhost -u http(s)://domain.com -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -t 300 --no-error --append-domain
