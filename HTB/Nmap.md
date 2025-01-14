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

nmap <scan types> <options> <target>

# Host Discovery

# Scan Network Range

sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
10.129.2.4
10.129.2.10
10.129.2.11
10.129.2.18
10.129.2.19
10.129.2.20
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
