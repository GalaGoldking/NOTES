# Directory brute-forcing
ffuf -w [wordlist] -u [URL]/FUZZ

ffuf -w [wordlist] -u http(s)://example.com/FUZZ

# VHOST enumeration
ffuf -w [wordlist] -H "Host: FUZZ.[URL]" -u [URL]

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.domain.com" -w http(s)://domain.com -t 300

# Subdomain enumeration
ffuf -w [wordlist] -u FUZZ.[URL]

ffuf -w [wordlist] -u http(s)://FUZZ.example.com

# Username Enumaration
ffuf -w [wordlist] -X [method] -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u [URL] -mr "[output message]"

ffuf -w /usr/share/wordlists/seclists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=geb@gmail.com&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http(s)://domain.com -mr "An account with this username already exists" -t 300

# Password Brute-Forcing
ffuf -w [Username wordlist]:W1 -w [Password wordlist]:W2 -X [method] -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http(s)://[URL] -fc [HTTP status]

ffuf -w /usr/share/wordlists/seclists/Usernames/Names/names.txt:W1 -w /usr/share/wordlists/seclists/Password/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://domain.com -fc [200]

# Flags

### Recursive scanning

-recursive 

ffuf -w [wordlist] -u [URL]/FUZZ -recursive

#### Specify depth for recursion

-recurion-depth

ffuf -w [wordlist] -u [URL]/FUZZ -recursive -recursive-depth 1

### Filtering

#### Filter file size

-fs

ffuf -w [wordlist] -H "Host: FUZZ.[URL]" -u [URL] -fs [file size]

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.domain.com" -u [URL] -fs 2222

#### Filter HTTP status code

-fc

ffuf -w [wordlist] -u [URL] -fc [status code]

ffuf -w [wordlist] -u [URL] -fc 404

#### Filter line count

ffuf -w [wordlist] -u [URL] -fl [line count]

ffuf -w [wordlist] -u [URL] -fl 10

#### Filter amount of words

ffuf -w [wordlist] -u [URL] -fw [word count]

ffuf -w [wordlist] -u [URL] -fw 23

### Specify extension

-e .[extension]

ffuf -w [wordlist] -u [URL]/FUZZ -e .php
