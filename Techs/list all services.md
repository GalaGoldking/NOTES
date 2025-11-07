# List all loaded services and their status 

```
systemctl list-units --type=service --all
```

# List only running services

```
systemctl list-units --type=service --state=running
```

# List all enabled services

```
systemctl list-unit-files --type=service --state=enabled
```

# Check the status of individual services

```
systemctl status <service-name>
```
