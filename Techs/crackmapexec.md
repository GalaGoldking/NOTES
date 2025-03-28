# Check for services

crackmapexec [SERVICE] [HOST] -u [USERNAME] -p [PASSWORD]

Result if service is found

![image](https://github.com/user-attachments/assets/165691e6-0997-493c-8580-f1c890778372)

Result if service is not found

![image](https://github.com/user-attachments/assets/b159f1c6-f667-4e52-890b-7ccabad5c046)

# SMB

<h3>Enumerate shares</h3>

crackmapexec smb [HOST] -u [USERNAME] -p [PASSWORD] --shares

<h3>Enumerate users</h3>

crackmapexec smb [HOST] -u [USERNAME] -p [PASSWORD] --users

<h3>No cred enumeration</h3>

crackmapexec smb [HOST] -u guest -p '' --rid-brute
