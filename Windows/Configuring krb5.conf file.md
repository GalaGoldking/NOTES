 - ### Kerberos Configuration (/etc/krb5.conf)
   Set up Kerberos authentication for domain
   - `sudo nano /etc/krb5.conf`

- Add this configuration to file, also change domain.ltd and target-ip with target domain and ip respectively without ignoring letter case. If DOMAIN.LTD is all uppercase then it must be RUSTYKEY.HTB if .domain.ltd then it must be .rustykey.htb
```ini
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
- ### Time synchronization
   Synchronized the attack machine's clock with the domain controller. Prevents Kerberos authentication failures due to clock skew.
  ```bash
   sudo timedatectl set-ntp off #To disable the Network Time Protocol from auto-updating
   sudo rdate -n [target-ip] #To match your date and time with target's date and time 
  ```
- ### Set Kerberos Ticket Environment Variable
   Exported the ticket for use in subsequent commands. Allows tools like evil-winrm to use the cached ticket for authentication.
  - `export KRB5CCNAME=USER.name.ccache #After getting TGT with impacket-getTGT`
