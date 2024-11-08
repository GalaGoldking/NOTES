# The Domain Information Groper

The dig command (Domain Information Groper) is a versatile and powerful utility for querying DNS servers and retrieving various types of DNS records. Its flexibility and detailed and customizable output make it a go-to choice

# Common dig Commands

<table>
  <tr>
    <th>Command</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>dig domain.com</td>
    <td>Performs a default A record lookup for the domain</td>
  </tr>
  <tr>
    <td>dig domain.com A</td>
    <td>Retrieves the IPv4 address (A record) associated with the domain</td>
  </tr>
  <tr>
    <td>dig domain.com AAAA</td>
    <td>Retrieves the IPvv6 address (AAAA record) associated with the domain</td>
  </tr>
  <tr>
    <td>dig domain.com MX</td>
    <td>Finds the mail servers (MX records) responsible for the domain</td>
  </tr>
  <tr>
    <td>dig domain.com NS</td>
    <td>Identifies the authoritative name servers for the domain</td>
  </tr>
  <tr>
    <td>dig domain.com TXT</td>
    <td>Retrieves any TXT records associated with the domain</td>
  </tr>
  <tr>
    <td>dig domain.com CNAME</td>
    <td>Retrieves the canonical name (CNAME) record for the domain</td>
  </tr>
  <tr>
    <td>dig domain.com SOA</td>
    <td>Retrieves the start of authority (SOA) record for the domain</td>
  </tr>
  <tr>
    <td>dig @1.1.1.1 domain.com</td>
    <td>Specifies a specific name server to query; in this case 1.1.1.1</td>
  </tr>
  <tr>
    <td>dig +trace domain.com</td>
    <td>Shows the full path of DNS resolution</td>
  </tr>
  <tr>
    <td>dig -x 192.168.1.1</td>
    <td>Performs a reverse lookup on the IP address 192.168.1.1 to find the associated host name. You may need to specify a name server</td>
  </tr>
  <tr>
    <td>dig +short domain.com</td>
    <td>Provides a short, concise answer to the query</td>
  </tr>
  <tr>
    <td>dig +noall +answer domain.com</td>
    <td>Displays only the answer section of the query output</td>
  </tr>
  <tr>
    <td>dig domain.com ANY</td>
    <td>Retrieves all available DNS records for the domain (Note: Many DNS sercers ignore ANY queries to reduce load and prevent abuse, as per RFC 8482)</td>
  </tr>
</table>


# Groping DNS

GalaGoldking@htb$ dig google.com

; <<>> DiG 9.18.24-0ubuntu0.22.04.1-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             0       IN      A       142.251.47.142

;; Query time: 0 msec
;; SERVER: 172.23.176.1#53(172.23.176.1) (UDP)
;; WHEN: Thu Jun 13 10:45:58 SAST 2024
;; MSG SIZE  rcvd: 54


This output is the result of a DNS query the dig command for the domain google.com. The output can be broken down into four key sections.

<ol>
  <li>Header</li>
  <ul>
    <li>;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449: This line indicates the type of query (QUERY), the successful status (NOERROR), and a unique identifier (16449) for this specific query.</li>
        <ul>
          <li>;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0: This describes the flags in the DNS header:</li>
          <ul>
            <li>qr: Query Response flag - indicates this is a response.</li>
            <li>rd: Recursion Desired flag - means recursion was requested.</li>
            <li>ad: Authentic Data flag - means the resolver considers the data authentic.</li>
            <li>The remaining numbers indicate the number of entries in each section of the DNS response: 1 question, 1 answer, 0 authority records, and 0 additional records.</li>
          </ul>
        </ul>
      <li>;; WARNING: recursion requested but not available: This indicates that recursion was requested, but the server does not support it.</li>
  </ul>
  <li>Question Section</li>
      <ul>
        <li>;google.com. IN A: This line specifies the question: "What is the IPv4 address (A record) for google.com?"</li>
      </ul>
  <li>Answer Section</li>
      <ul>
        <li>google.com. 0 IN A 142.251.47.142: This is the answer to the query. It indicates that the IP address associated with google.com is 142.251.47.142. The '0' represents the TTL (time-to-live), indicating how long the result can be cached before being refreshed.</li>
      </ul>
  <li>Footer</li>
      <ul>
        <li>;; Query time: 0 msec: This shows the time it took for the query to be processed and the response to be received (0 milliseconds).</li>
        <li>;; SERVER: 172.23.176.1#53(172.23.176.1) (UDP): This identifies the DNS server that provided the answer and the protocol used (UDP).</li>
        <li>;; WHEN: Thu Jun 13 10:45:58 SAST 2024: This is the timestamp of when the query was made.</li>
        <li>;; MSG SIZE rcvd: 54: This indicates the size of the DNS message received (54 bytes).</li>
      </ul>
</ol>
