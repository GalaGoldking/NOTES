# Usage
grep [string] [file]

Do not specify file name to search starting from current pwd

# Filter nmap output to show only IP addresses

nmap [Target network range] -sn -oA tnet | grep for | cut -d" " -f5

# Find specific combination from directory

grep -r [STRING] [DIRECTORY]

# Find specific combination case-insensitively

grep -i [STRING] [DIRECTORY]

