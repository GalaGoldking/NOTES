# First Steps For Exploiting Windows Machines

<h3>Find open ports</h3>

nmap -sC -sV -Pn -p- [HOST]

<h3>Enumerate with crackmapexec</h3>

crackmapexec [SERVICE] [HOST] -u [USERNAME] -p [PASSWORD]

[Link for crackmapexec notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/crackmapexec.md)

<h3>If SMB found</h3>

Try connecting to smb with smbclient

smblient //[HOST]/[SHARE] -U [USERNAME] 

[Link for SMBclient notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/smbclient.md)
[Link for SMB notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/smb.md)

<h3>If credentials are found</h3>

Try password spraying

crackmapexec [SERVICE] [HOST] -u [user_list.txt] -p [password_list.txt] --continue-on-success

<h3>MSSQL</h3>

Connect to mssql if credentials are found

impacket-mssqlclient [HOST]/[USER]:[PASSWORD]@[IP-ADDRESS]

