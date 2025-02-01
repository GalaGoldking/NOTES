# no matching key exchange method found

-oKexAlgorithms

# Unable to negotiate with [IP] port 22: no matching key exchange method found. Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1

-oKexAlgorithms=+diffie-hellman-group1-sha1

# Unable to negotiate with [IP] port 22: no matching host key type found. Their offer: ssh-rsa,ssh-dss

-oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedAlgorithms=+ssh-rsa
