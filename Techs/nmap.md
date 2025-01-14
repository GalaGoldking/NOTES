# Usage 
nmap [OPTIONS] [IP Adress]

nmap -sC -sV 10.10.10.10
# Scan Network Range
nmap [Target Network Range] -sn
# Scan Multiple IPs
By specifying multiple addresses

sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20

If these IP addresses are next to each other, we can also define the range in the respective octet.

sudo nmap -sn -oA tnet 10.129.2.18-20

# Filter nmap output to show only IP addresses

nmap [Target network range] -sn -oA tnet | grep for | cut -d" " -f5

# Scan IP List

sudo nmap -sn -oA tnet -iL [File with IP addreses]

# Options
# -sn
nmap -sn 10.10.10.10

Disable port scan
# -A 
Aggresive mode
# -sC 
Runs safe scripts
# -T[number]
Specify number of threads running at the same time to increase speed of scan
# -n
No dns lookup
# -Pn
No ping
# -p
Specify ports <br>
To scan one or more ports: -p [PORT, PORT, ...] <br>
To scan interval of ports: -p 1000-1100 <br>
To scan all ports: -p- <br>
# -v
Verbose output level 1: -v <br>
Verbose output level 2: -vv
# -o
Save the output into file <br>
nmap -sC -sV -o nmap_result.txt 10.10.10.10
# -oA
nmap -oA 'tnet' 10.10.10.10

Store the results in all formats starting with the name 'tnet'
# -iL
nmap -iL [file with targets]

scan multiple targets from specified file
# nmap as dirbuster
nmap --script http-enum -p80 <target>
# Find vulnerabilities with nmap
nmap --script vuln -sC -sV <target>
