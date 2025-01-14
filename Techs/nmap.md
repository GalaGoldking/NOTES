# Usage 
nmap [OPTIONS] [IP Adress]

nmap -sC -sV 10.10.10.10
# Scan Network Range
nmap [Target Network Range] -sn
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
# nmap as dirbuster
nmap --script http-enum -p80 <target>
# Find vulnerabilities with nmap
nmap --script vuln -sC -sV <target>
