After we connect using netcat we use python to upgrade to full TTY

```
python -c 'import pty; pty.spawn("/bin/bash")'
```

After we run this command we will hit `Ctrl + Z` to background our shell and get back to out local terminal, and use this command:

```bash
stty raw -echo
fg
```

Once we use `fg` command it will bring out our shell to foreground

Now we need to setup terminal variables, first we need to get the output of this variables on our local terminal

```
echo $TERM

xterm-256color
```

```
stty size

67 318
```

The first command showed us the TERM variable, and the second shows us the values for rows and columns. And now on out remote shell:

```
export TERM=xterm-256 color
stty rows 67 columns 318
```

