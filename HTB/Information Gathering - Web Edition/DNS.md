# How DNS works

![image](https://mermaid.ink/svg/pako:eNptkk1uwjAQha8y8rpcIItWkAAtUNQmlSrksDDxlEQQT-QfJIS4ex2nNG1arzx-n5-ex3NhBUlkEdtr0ZSwSnMFfhm36w425DTEVDfOou60do15XGJxMBCLosQtjEb3MLk8vcCMnJIP156ceA3WFIiYZ6ikgWSdwatDfQZLkKKh4wn1dnBngyZceuQxKYWFNS39jjtTWfyCvdsgb2t9c-wN4-CU_A7dy8mPjFOeYuG0qU4IK6KDa4bgLdjck9ZpZcC_20e7dWmYbRroGU-JLKxFjZCh7h88C_KCv62Sf9RFUJd87GxJurLCtsH-cssuUlfMu8blit2xGnUtKul_-NKKObMl1pizyG-l0Iec5erqOeEsZWdVsMhqh3dMk9uXLPoQR-Mr10hhMamE73L9fYqysqSfuwEKc3T9BOe0sj4)

<ol>
  <li>
    Your Computer Asks for Directions (DNS Query): When you enter the domain name, your computer first checks its memory (cache) to see if it remembers the IP address from a previous visit. If not, it reaches out to a DNS resolver, usually provided by your internet service provider (ISP).
  </li>
  <li>
    The DNS Resolver Checks its Map (Recursive Lookup): The resolver also has a cache, and if it doesn't find the IP address there, it starts a journey through the DNS hierarchy. It begins by asking a root name server, which is like the librarian of the internet.
  </li>
  <li>
    Root Name Server Points the Way: The root server doesn't know the exact address but knows who does – the Top-Level Domain (TLD) name server responsible for the domain's ending (e.g., .com, .org). It points the resolver in the right direction.
  </li>
  <li>
    TLD Name Server Narrows It Down: The TLD name server is like a regional map. It knows which authoritative name server is responsible for the specific domain you're looking for (e.g., example.com) and sends the resolver there.
  </li>
  <li>
    Authoritative Name Server Delivers the Address: The authoritative name server is the final stop. It's like the street address of the website you want. It holds the correct IP address and sends it back to the resolver.
  </li>
  <li>
    The DNS Resolver Returns the Information: The resolver receives the IP address and gives it to your computer. It also remembers it for a while (caches it), in case you want to revisit the website soon.
  </li>
  <li>
    Your Computer Connects: Now that your computer knows the IP address, it can connect directly to the web server hosting the website, and you can start browsing.
  </li>
</ol>

# DNS Concepts

<table>
  <tr>
    <th>DNS Concept</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  <tr>
    <td>Domain Name</td>
    <td>A human-readable label for a website or other internet resource.</td>
    <td>www.example.com</td>
  </tr>
  <tr>
    <td>IP Address</td>
    <td>A unique numerical identifier assigned to each device connected to the internet.</td>
    <td>192.2.0.1</td>
  </tr>
  <tr>
    <td>DNS Resolver</td>
    <td>A server that translates domain names into IP addresses</td>
    <td>Your ISP's (Internet Service Providers) DNS server or public resolvers like Google DNS (8.8.8.8)</td>
  </tr>
  <tr>
    <td>Root Name Server</td>
    <td>The top-level servers in the DNS hierarchy</td>
    <td>There are 13 root servers worldwide, named A-M: a.root-servers.net</td>
  </tr>
  <tr>
    <td>TLD Name Server</td>
    <td>Servers responsible for specific top-level domains (e.g., .com, .org)</td>
    <td>Verisign</td>
  </tr>
  <tr>
    <td>Authoritative Name Server</td>
    <td>The server thet holds the actual IP address for a domain</td>
    <td>Often managed by hosting providers or domain registrars</td>
  </tr>
  <tr>
    <td>DNS Record Types</td>
    <td>Different types of information stored in DNS</td>
    <td>A, AAAA, CNAME, MX, NS, TXT, etc.</td>
  </tr>
</table>

# DNS Record Types

<table>
  <tr>
    <th>Record Type</th>
    <th>Full Name</th>
    <th>Description</th>
    <th>Zone File Example</th>
  </tr>
  <tr>
    <td>A</td>
    <td>Address Record</td>
    <td>Maps a hostname to its IPv4 address</td>
    <td>www.example.com. IN A 192.0.2.1</td>
  </tr>
  <tr>
    <td>AAAA</td>
    <td>IPv6 Address Record</td>
    <td>Maps a hostname to its IPv6 address</td>
    <td>www.example.com. IN AAAA 2001:db8:85a3::8a2e:370:7334</td>
  </tr>
  <tr>
    <td>CNAME</td>
    <td>Canonical Record Name</td>
    <td>Creates an alias for a hostname, pointing it to another hostname.	</td>
    <td>blog.example.com. IN CNAME webserver.example.net.</td>
  </tr>
  <tr>
    <td>MX</td>
    <td>Mail Exchange Record</td>
    <td>Specifies the mail server(s) responsible for handling email for the domain</td>
    <td>example.com. IN MX 10 mail.example.com</td>
  </tr>
  <tr>
    <td>NS</td>
    <td>Name Server Record</td>
    <td>Delegates a DNS zone to a specific authoritative name server</td>
    <td>example.com. IN NS ns1.example.com.</td>
  </tr>
  <tr>
    <td>TXT</td>
    <td>Text Record</td>
    <td>Stores a arbitrary text information, often used for domain verification of security policies</td>
    <td>example.com. IN TXT "v=spf1 mx -all" (SPF record)</td>
  </tr>
  <tr>
    <td>SOA</td>
    <td>Start of Authority Record</td>
    <td>Specifies administrative information about a DNS zone, including the primary name server, responsible person's email and other parameters</td>
    <td>example.com. IN SOA ns1.example.com. admin.example.com. 2002460301 10800 3600 604800 86400</td>
  </tr>
  <tr>
    <td>SRV</td>
    <td>Service Record</td>
    <td>Defines the hostname and port number for specific services</td>
    <td>_sip._udp.example.com. IN SRV 10 5 5060 sipserver.example.com</td>
  </tr>
  <tr>
    <td>PTR</td>
    <td>Pointer Record</td>
    <td>Used ro reverse DNS lookups, mapping an IP address for a hostname</td>
    <td>1.2.0.192.in-addr.arpa. IN PTR www.example.com</td>
  </tr>
</table>
