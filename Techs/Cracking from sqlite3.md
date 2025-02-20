# pbkdf2$50000$50

sqlite3 [FILE].db "select passwd,salt,name from user" | while read data; do digest=$(echo "$data" | cut -d'|' -f1 | xxd -r -p | base64); salt=$(echo "$data" | cut -d'|' -f2 | xxd -r -p | base64); name=$(echo $data | cut -d'|' -f 3); echo "${name}:sha256:50000:${salt}:${digest}"; done | tee [OUTPUT].hashes

# Cracking

hashcat [OUTPUT].hashes --user

Using --user flag because in output file hash starts with username and seperates with :

#Checking output

hashcat [OUTPUT].hashes --show --user
