# PF-04 — Personal Website Live

## Live Website

https://minaibrahim.tech

The site is deployed publicly over HTTPS and contains my positioning, selected work, GitHub, LinkedIn, CV, contact options, and a booking link.

## Booking

https://calendly.com/minaibrahim190/30-minute-meeting-with-mina-ibrahim

## DNS Walkthrough

DNS is the system that connects a domain name to the place where a website is hosted.

For example, when someone types minaibrahim.tech into a browser, the browser does not already know where that website lives. It asks a DNS resolver to look up the domain. The resolver checks the DNS system and reaches the authoritative nameserver responsible for the domain. That nameserver returns the DNS record that tells the resolver where the request should go.

An A record can map a domain directly to an IP address. A CNAME record works differently: it points one hostname to another hostname instead of directly to an IP address.

After the DNS lookup is complete, the browser knows which host it needs to contact. It then connects to that host and requests the website. Because my site uses HTTPS, the connection between the browser and the host is encrypted before the page is delivered.

The important thing I learned is that the domain name and the hosting server are separate parts. DNS is the layer that connects them. Without DNS, users would need to know the server address instead of simply typing a readable domain name.
