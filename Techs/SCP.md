# Basic Usage
```
scp /path/to/local/file username@remote_server:/path/to/remote/directory
```
 
Used to send/share/copy files through ssh

# Sending file using scp
```
scp file.txt username@remote_server:/home/username/directory
```

# Sending files recursively
```
scp -r /path/to/local/directory/ username@remote_server:/path/to/remote/directory
```

# Getting files from remote server
```
scp username@remote_server:/path/to/remote/file /path/to/local/directory
```

# Getting files recursively from remote server
```
scp -r username@remote_server:/path/to/remote/directory /path/to/local/directory
```

# Copying files between two remote servers
```
scp username1@remote_server1:/path/to/file.txt username2@remote_server2:/path/to/directory
```
