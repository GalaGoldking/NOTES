# Use Cases

The tool is one of the most used tools by network administrators and IT security specialists.
It is used to:
<ul>
  <li>Audit the security aspects of networks</li>
  <li>Simulate penetration tests</li>
  <li>Check firewall and IDS settings and configurations</li>
  <li>Types of possible connections</li>
  <li>Network mapping</li>
  <li>Response analysis</li>
  <li>Identify open ports</li>
  <li>Vulnerability assessment as well.</li>
</ul>

# Nmap Architecture

Nmap offers many different types of scans that can be used to obtain various results about
our targets. Basically, Nmap can be divided into the following scanning techniques:

<ul>
  <li>Host discovery</li>
  <li>Port scanning</li>
  <li>Service enumeration and detection</li>
  <li>OS detection</li>
  <li>Scriptable interaction with the target service (Nmap Scripting Engine)</li>
</ul>

# Syntax

nmap [scan types] [options] [target]

# Host Discovery

# Scan Network Range

sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5 <br>
10.129.2.4 <br>
10.129.2.10 <br>
10.129.2.11 <br>
10.129.2.18 <br>
10.129.2.19 <br>
10.129.2.20 <br>
10.129.2.28

<table>
  <tr>
    <th>Scanning Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>10.129.2.0/24</td>
    <td>Target network range</td>
  </tr>
  <tr>
    <td>-sn</td>
    <td>Disables port scanning</td>
  </tr>
  <tr>
    <td>-oA tnet</td>
    <td>Stores the results in all formats starting with the name 'tnet'</td>
  </tr>
</table>

# Filter nmap output to show only IP addresses

nmap [Target network range] -sn -oA tnet | grep for | cut -d" " -f5

# Scan IP List

cat hosts.lst <br>
10.129.2.4 <br>
10.129.2.10 <br>
10.129.2.11 <br>
10.129.2.18 <br>
10.129.2.19 <br>
10.129.2.20 <br>
10.129.2.28

sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5 <br>
10.129.2.18 <br>
10.129.2.19 <br>
10.129.2.20

<table>
  <tr>
    <th>Scanning Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>-sn</td>
    <td>Disables port scanning</td>
  </tr>
  <tr>
    <td>-oA tnet</td>
    <td>Stores the results in all formats starting with the name 'tnet'</td>
  </tr>
  <tr>
    <td>-iL</td>
    <td>Performs defined scans against targets in provided 'hosts.lst' file</td>
  </tr>
</table>

# Scan Multiple IPs

sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20| grep for | cut
-d" " -f5

10.129.2.18 <br>
10.129.2.19 <br>
10.129.2.20

If these IP addresses are next to each other, we can also define the range in the respective octet.

sudo nmap -sn -oA tnet 10.129.2.18-20| grep for | cut -d" " -f5

10.129.2.18 <br>
10.129.2.19 <br>
10.129.2.20

# Scan single IP

If we disable port scan ( -sn ), Nmap automatically ping scan with ICMP Echo Requests ( -PE ). Once such a request is sent, we usually expect an ICMP reply if the pinging host is alive. The more interesting fact is that our previous scans did not do that because before Nmap could send an ICMP echo request, it would send an ARP ping resulting in an ARP reply . We can confirm this with the " --packet-trace " option. To ensure that ICMP echo requests are sent, we also define the option ( -PE ) for this.

sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-14 23:59 CEST <br>
Nmap scan report for 10.129.2.18 <br>
Host is up (0.087s latency). <br>
MAC Address: DE:AD:00:00:BE:EF <br>
Nmap done: 1 IP address (1hide01.ir host up) scanned in 0.11 seconds

<table>
  <tr>
    <th>Scanning Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>-sn</td>
    <td>Disables port scanning</td>
  </tr>
  <tr>
    <td>-oA host</td>
    <td>Stores the results in all formats starting with the name 'host'</td>
  </tr>
  <tr>
    <td>-PE</td>
    <td>Performs the ping scan by using 'ICMP Echo requests' against the target.</td>
  </tr>
  <tr>
    <td>--packet-trace</td>
    <td>Shows all packets sent and received</td>
  </tr>
</table>

Another way to determine why Nmap has our target marked as "alive" is with the " --
reason " option.

sudo nmap 10.129.2.18 -sn -oA host -PE --reason <br>
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:10 CEST <br>
SENT (0.0074s) ARP who-has 10.129.2.18 tell 10.10.14.2 <br>
RCVD (0.0309s) ARP reply 10.129.2.18 is-at DE:AD:00:00:BE:EF <br>
Nmap scan report for 10.129.2.18 <br>
Host is up, received arp-response (0.028s latency). <br>
MAC Address: DE:AD:00:00:BE:EF <br>
Nmap done: 1 IP address (1 host up) scanned in 0.03 seconds 

<table>
  <tr>
    <th>Scanning Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>-sn</td>
    <td>Disables port scanning</td>
  </tr>
  <tr>
    <td>-oA host</td>
    <td>Stores the results in all formats starting with the name 'host'</td>
  </tr>
  <tr>
    <td>-PE</td>
    <td>Performs the ping scan by using 'ICMP Echo requests' against the target.</td>
  </tr>
  <tr>
    <td>--reason</td>
    <td>Displays the reason for specific result.</td>
  </tr>
</table>

We see here that Nmap does indeed detect whether the host is alive or not through the ARP request and ARP reply alone. To disable ARP requests and scan our target with the desired ICMP echo requests , we can disable ARP pings by setting the " --disable-arpping " option. Then we can scan our target again and look at the packets sent and received.

sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping <br>
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:12 CEST <br>
SENT (0.0107s) ICMP [10.10.14.2 > 10.129.2.18 Echo request (type=8/code=0) <br>
id=13607 seq=0] IP [ttl=255 id=23541 iplen=28 ] <br>
RCVD (0.0152s) ICMP [10.129.2.18 > 10.10.14.2 Echo reply (type=0/code=0) <br>
id=13607 seq=0] IP [ttl=128 id=40622 iplen=28 ] <br>
Nmap scan report for 10.129.2.18 <br>
Host is up (0.086s latency). <br>
MAC Address: DE:AD:00:00:BE:EF <br>
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds

# Host and Port Scanning

There are a total of 6 different states for a scanned port we can obtain:

<table>
  <tr>
    <th>State</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>open</td>
    <td>This indicates that the connection to the scanned port has been established. These connections can be TCP connections, UDP datagrams as well as SCTP associations.
</td>
  </tr>
  <tr>
    <td>closed</td>
    <td>When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an RST flag. This scanning method can also be used to determine if our target is alive or not.
</td>
  </tr>
  <tr>
    <td>filtered</td>
    <td>Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.</td>
  </tr>
  <tr>
    <td>unfiltered</td>
    <td>This state of a port only occurs during the TCP-ACK scan and means that the port is accessible, but it cannot be determined whether it is open or closed.</td>
  </tr>
</table>

# Discovering Open TCP Ports

By default, Nmap scans the top 1000 TCP ports with the SYN scan ( -sS ). This SYN scan is set only to default when we run it as root because of the socket permissions required to create raw TCP packets. Otherwise, the TCP scan ( -sT ) is performed by default. This means that if we do not define ports and scanning methods, these parameters are set automatically. We can define the ports one by one ( -p 22,25,80,139,445 ), by range ( -p 22-445 ), by top ports ( --top-ports=10 ) from the Nmap database that have been signed as most frequent, by scanning all ports ( -p- ) but also by defining a fast port scan, which contains top 100 ports ( -F ).


# Nmap - Trace the Packets

sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping 

Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 15:39 CEST <br>
SENT (0.0429s) TCP 10.10.14.2:63090 > 10.129.2.28:21 S ttl=56 id=57322 <br>
iplen=44 seq=1699105818 win=1024 <mss 1460> <br>
RCVD (0.0573s) TCP 10.129.2.28:21 > 10.10.14.2:63090 RA ttl=64 id=0 <br>
iplen=40 seq=0 win=0 <br>
Nmap scan report for 10.11.1.28 <br>
Host is up (0.014s latency). <br>

PORT STATE SERVICE <br>
21/tcp closed ftp <br>
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds 

<table>
  <tr>
    <th>Scanning Options</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>10.129.2.28</td>
    <td>Scans the specified target.</td>
  </tr>
  <tr>
    <td>-p 21</td>
    <td>Scans only the specified port.</td>
  </tr>
  <tr>
    <td>--packet-trace</td>
    <td>Shows all packets sent and received.</td>
  </tr>
  <tr>
    <td>-n</td>
    <td>Disables DNS resolution.</td>
  </tr>
  <tr>
    <td>--disable-arp-ping</td>
    <td>Disables ARP ping.</td>
  </tr>
</table>







