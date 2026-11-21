# Footprinting and Reconnaissance Lab

Everything an attacker can learn about an organisation before touching a single one of its systems. I used only public sources, including search engines, WHOIS, DNS, theHarvester, Maltego and Shodan, to see how much of a company's infrastructure is already out in the open.

The full write-up with screenshots is in [report.pdf](report.pdf).

## What I did

**Google hacking**
- Compared `site:`, `inurl:`, `link:`, `related:` and `info:` against a news site to see how each operator narrows the results
- Used Google Advanced Search, and worked out how its form fields map to URL parameters (`as_q`, `as_epq`, `as_sitesearch`…) so queries can be built straight in the address bar
- Ran dork categories against a retail domain: login pages, exposed config files, database files, logs, backups, SQL and PHP errors, and `phpinfo()`. Most came back clean, but `robots.txt` listed paths like `/admin` and `/config`, which is exactly the kind of hint an attacker looks for.

**WHOIS**
- Looked up registrar, creation and expiry dates, name servers and the `clientTransferProhibited` lock
- Compared a company that uses a privacy service with universities whose WHOIS records list real contact names and emails

**DNS recon**
- `host` and `dig` for A, MX, NS, TXT, CNAME and SOA records, plus reverse lookups and `+trace` to follow a lookup from the root servers down
- TXT records were surprisingly chatty. They revealed which third-party services the company uses through their domain verification strings.
- Performed a full zone transfer (`dig axfr`) against `zonetransfer.me`, a domain set up for practising this, to show why open zone transfers need to be locked down

**theHarvester and Maltego**
- Collected hostnames and email addresses tied to the target domain
- Ran Maltego's Company Stalker and Footprint L1 machines to map out domains, IPs, mail servers and staff email addresses as a graph

**Shodan**
- Searched for devices still using default passwords, old Apache servers, webcams and end-of-life IIS 5.0 and 6.0 servers
- One result was a Redis server with no password on the default user, open to the internet

## What I took away from it

- A lot of reconnaissance needs no hacking at all. It's just reading what organisations publish about themselves.
- DNS TXT records and `robots.txt` leak more than people expect
- Shodan makes it very clear how many devices are still exposed with default settings

## Tools

Google, who.is, Domain Dossier, host, dig, theHarvester, Maltego CE, Shodan

This was a college assignment for my Master's in Cybersecurity at Illinois Tech. Only passive techniques and publicly available information were used.
