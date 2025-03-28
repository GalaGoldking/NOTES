# First Steps For Exploiting Windows Machines

<h3>Find open ports</h3>

nmap -sC -sV -Pn -p- [HOST]

<h3>Enumerate with crackmapexec</h3>

crackmapexec [SERVICE] [HOST] -u [USERNAME] -p [PASSWORD]

[Link for crackmapexec notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/crackmapexec.md)

<h3>Check credentials</h3>

crackmapexec [SERVICE] [HOST] -u [USERNAME] -p [PASSWORD]

If credentials are correct

![image](https://github.com/user-attachments/assets/d282eefd-0ad3-4026-abec-06f40de9dc2b)

If credentials are incorrect

![image](https://github.com/user-attachments/assets/9736e240-d0dc-4970-b72a-e9131864852c)

<h3>If credentials are found</h3>

Try password spraying

crackmapexec [SERVICE] [HOST] -u [user_list.txt] -p [password_list.txt] --continue-on-success

<h3>SMB</h3>

Try connecting to smb with smbclient

smblient //[HOST]/[SHARE] -U [USERNAME] 

[Link for SMBclient notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/smbclient.md)
[Link for SMB notes](https://github.com/GalaGoldking/NOTES/blob/main/Techs/smb.md)

<h3>MSSQL</h3>

Connect to mssql if credentials are found

impacket-mssqlclient [HOST]/[USER]:[PASSWORD]@[IP-ADDRESS]

<h3>WINRM</h3>

Connect to winrm if credentials are found

evil-winrm -i [HOST] -u [USERNAME] -p [PASSWORD]




