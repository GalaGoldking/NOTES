# Running nikto scan

nikto -h [HOST] 

# Passing cookie to nikto 

nano /etc/nikto.conf

Find STATIC-COOKIE and change to whatever you need

![image](https://github.com/user-attachments/assets/f750747b-3df0-4a36-831b-c8ad806176af)

Comment the row if you no longer need it or change it when you need to 

https://security.stackexchange.com/questions/184910/nikto-authentication 

# Using proxy to forward nikto with burp

nano /etc/nikto.conf

![image](https://github.com/user-attachments/assets/6c99033e-f019-4fc0-87f5-0f6685b29728)

Uncomment Proxyhost and Proxyport and make sure that they are correct with your proxy config

To run nikto with burp use this command nikto -h [HOST] -useproxy

Possible error

ERROR: Proxy error: opening stream: can't connect: proxy connect failed: proxy connect to 127.0.0.1:8080 failed: Invalid argument at 

/var/lib/nikto/plugins/LW2.pm line 5254.

; Invalid argument at /var/lib/nikto/plugins/LW2.pm line 5254.

: Invalid argument

Find LW_SSL_ENGINE in /etc/nikto.conf and change the parameter from auto to SSLeay 

![image](https://github.com/user-attachments/assets/f701213f-264f-4668-b51f-b8e27e1c13e4)

https://security.stackexchange.com/questions/184910/nikto-authentication

# Overriding /etc/nikto.conf parameters in terminal without changing them

## Example 

nikto -h [HOST] -O STATIC-COOKIE="name=value";"other=value"

# Scanning https

nikto -h https://[target] -ssl

