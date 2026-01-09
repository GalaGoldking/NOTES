# Creating ssh key

run as root

```
ssh-keygen -t ed25519 -C "email@example.com"
ssh-add ~/.ssh/id_ed25519
ssh-add -l
cat ~/.ssh/id_ed25519
ssh -T git@github.com
```

After that add id_ed25519.pub contents to GitHub profile's settings
