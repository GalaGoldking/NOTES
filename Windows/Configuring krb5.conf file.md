# Kerberos Configuration (/etc/krb5.conf)

```
sudo nano /etc/krb5.conf
```

Add this configuration to file, also change domain.ltd and target-ip with target domain and ip respectively without ignoring letter case. If DOMAIN.LTD is all uppercase then it must be RUSTYKEY.HTB if .domain.ltd then it must be .rustykey.htb

```code
[libdefaults]
   default_realm = DOMAIN.TLD
   dns_lookup_realm = false
   dns_lookup_kdc = true
   ticket_lifetime = 24h
   forwardable = true

[realms]
   DOMAIN.TLD = {
       kdc = target-ip
       admin_server = target-ip
       default_domain = DOMAIN.TLD
   }

[domain_realm]
   .domain.tld = DOMAIN.TLD
   domain.tld = DOMAIN.TLD
```
