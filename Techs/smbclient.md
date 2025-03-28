# Basic Usage

smbclient //[HOST]/[SHARE]/ -U [USERNAME]

smbclient //10.10.10.10/SHARENAME -U 'user'

# SMB enumeration

smbclient -L //[HOST]/

smbclient -L //10.10.10.10/
