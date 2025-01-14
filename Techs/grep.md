# Usage
grep [string] [file]

# Filter nmap output to show only IP addresses

nmap [Target network range] -sn -oA tnet | grep for | cut -d" " -f5
