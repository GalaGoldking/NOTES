# hydra
base usage: hydra -l user -P passlist.txt [address] protocol
# using parallel connection to get faster result
hydra -t [number of parallel connections] -l user -P passlist.txt [address] protocol \n
hydra -t 16 -l administrator -P /usr/share/wordlists/rockyou.txt 10.10.10.10 ssh
