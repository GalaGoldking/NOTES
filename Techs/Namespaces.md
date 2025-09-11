# Base info
Knowing nameservers if vulnerable can lead to zone transfer and reveal all subdomains of a target

# Nameserver Providers – Reference Table

| Provider Type         | Provider         | Example Nameservers / Pattern                     | Notes (Why It Matters) |
|-----------------------|-----------------|---------------------------------------------------|-------------------------|
| **Domain Registrar**  | Namecheap       | `dns1.registrar-servers.com`, `dns2.registrar-servers.com` | Registrar DNS often means minimal security features (no advanced DDoS/WAF), and spotting them can reveal the registrar directly. |
|                       | GoDaddy         | `nsXX.domaincontrol.com` (e.g., `ns13.domaincontrol.com`) |  |
|                       | Google Domains  | `ns-cloud-XX.googledomains.com`                  |  |
|                       | Hover (Tucows)  | `ns1.hover.com`, `ns2.hover.com`                 |  |
| **Cloud Hosting Providers**   | AWS Route53     | `ns-XXXX.awsdns-XX.com/.net/.org/.co.uk`          | Ties the target directly to cloud infrastructure. If DNS is in AWS/Azure/GCP, the application may also be hosted there. |
|                       | Microsoft Azure | `ns1-XX.azure-dns.com/.net/.org/.info`           |  |
|                       | Google Cloud DNS| `ns-cloud-XX.googledomains.com`                  |  |
|                       | Oracle Cloud    | `nsXX.oracledns.com`                             |  |
| **CDN / DDoS Protection / WAF Providers**         | Cloudflare      | Random names: `abby.ns.cloudflare.com`, `jack.ns.cloudflare.com` | Detects if the target is behind a CDN/WAF (hiding the real IP). Knowing this allows you to search for origin IP leaks. |
|                       | Akamai          | `aX-XX.akam.net`                                 |  |
|                       | Fastly          | `ns1.fastly.net`, `ns2.fastly.net`               |  |
|                       | Imperva (Incapsula) | `ns1.impervadns.net`, `ns2.impervadns.net`    |  |
| **Web Hosts**         | Bluehost        | `ns1.bluehost.com`, `ns2.bluehost.com`           | These often indicate small-to-medium businesses that rely on default web hosting DNS—possible low maturity in security posture. |
|                       | HostGator       | `nsXXXX.hostgator.com` (e.g., `ns3151.hostgator.com`) |  |
|                       | DreamHost       | `ns1.dreamhost.com`, `ns2.dreamhost.com`, `ns3.dreamhost.com` |  |
|                       | SiteGround      | `ns1.siteground.net`, `ns2.siteground.net`       | Enterprise-grade DNS often suggests a more security-aware organization, but can also show reliance on third-party availability. |
| **Enterprise DNS**    | Oracle DynDNS   | `ns1.pXX.dynect.net`                             |  |
|                       | NS1             | `dns1.p01.nsone.net`, `dns2.p01.nsone.net`       |  |
|                       | UltraDNS        | `pdns1.ultradns.net`, `pdns2.ultradns.org`       |  |

---

