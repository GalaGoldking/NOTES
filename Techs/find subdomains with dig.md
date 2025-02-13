# DIG

If DNS server is known we can use dig to get information about subdomains

dig axfr [host] @[DNS server]

# Example

dig axfr cronos.htb @10.10.10.13

![image](https://github.com/user-attachments/assets/3ff5bb83-3a19-43d6-9e00-37779642afdb)


Now add subdomains to /etc/hosts file
