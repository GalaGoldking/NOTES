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

# Password spraying

<h3>Password spraying</h3>

crackmapexec [SERVICE] [HOST] -u [user_list.txt] -p [password_list.txt] 

To continue all variations even though one combination was successful use this flag --continue-on-success

crackmapexec [SERVICE] [HOST] -u [user_list.txt] -p [password_list.txt] --continue-on-success

<h3>Check credentials</h3>

crackmapexec [SERVICE] [HOST] -u [USERNAME] -p [PASSWORD]

If credentials are correct

![image](https://github.com/user-attachments/assets/d282eefd-0ad3-4026-abec-06f40de9dc2b)

If credentials are incorrect

![image](https://github.com/user-attachments/assets/9736e240-d0dc-4970-b72a-e9131864852c)

