# Launch
msfconsole
# base usage
search =-> use [search output] --> options --> set --> run
# Search for exploit
search mysql_schemadump
# Checking options
options
# changing directory
use auxiliary/smtp_enum
# set options
set RHOSTS [target IP address]
set RPORTS [target port]
# Run exploit
run
