> [!info] Cloudflare Outage
> - Cloudflare: company involved in serving at least 20% of all websites
> 	- Content Distribution Network: put static files on it
> 	- Entry point for requests to dynamic pages
> - Parts of their service had a large outage last year
> 
> > [!info]- Avoiding outages
> > - Reliability is measured in "nines"
> > 	- 1 nine = 90% = **36 days**/year downtime
> > 	- 2 nines = 99% = **88 hours**/year
> > 	- ...
> > 	- 5 nines = **5 minutes**/year
> > - You can design your system to achieve different levels
> > 	- ? Do you have one data center or multiple?
> > 	- ? Can you shut down your service to update it?
> > - You can charge much more if you promise to be reliable
> 
> > [!info]- Cloudflare analytics cloud design
> > ![[Pasted image 20241120131820.png]]
> 
> > [!info]- What happened
> > - 3 redundant data centers
> > - redundant power feeds
> > - one power feed was cut
> > - generator were started
> > - then the transformer for other power feed went out
> > 	- generator feed was cut by circuit breaker
> > - 10 minutes of battery lie to get generators back online
> > 	- but only lasted for 4
> > - They discovered there were services only run in the one data center which were lost

> [!info] DNS
> 
> > [!info]- etc/hosts
> > - Text file mapping names to IP addresses
> > 
> > ![[Pasted image 20241120132126.png]]
> 
> > [!info]- Name servers
> > - Provide a domain name, they will give back information about it
> > 
> > ![[Pasted image 20241120132154.png]]
> 
> > [!question]- Which DNS server to use?
> > - When connect to network, DHCP gives you an IP address and says what your DNS server is
> 
> > [!info]- DNS hierarchy
> > - Don't want Comcast to need a list of all names and IP addresses
> > 
> > ![[Pasted image 20241120132256.png]]
> 
> > [!info]- DNS resolution
> > - Iterative resolution process: finding IP address for a name
> > 
> > ![[Pasted image 20241120132322.png]]
> 
> > [!info]- DNS caching
> > ![[Pasted image 20241120132355.png]]
> > 
> > - My computer only talks to Comcast
> > - DNS mappings change very rarely, so cached a long time

> [!info] DNS Lookup
> 
> > [!info]- Parts of DNS record
> > - Main goal:
> > 	- name → IP address
> > - But also can encode more information
> > 	- Name servers for subdomains
> 
> > [!info]- Iterative DNS query procedure
> > ![[Pasted image 20241120132623.png]]
> 
> > [!info]- How its actually done
> > ![[Pasted image 20241120132732.png]]

> [!info] Content Delivery Networks
> 
> > [!info]- Reducing website load
> > - Server-side dynamic websites can be costly to run
> > 	- Pay for CPU time and bandwidth
> > - Become \#1 link on reddit
> > 	- Your web traffic goes up from 10 people/day to 10 million
> > - Servers get overwhelmed and stop taking new connections
> > - ! This is bad!
> > 	- Nobody can see your page
> > 	- Expensive
> 
> > [!info]- Website caching
> > - Wikipedia: frequent changes, but once an hour, not once a day
> > - Lots of work for a dynamic site to re-compute HTML
> > - Save the HTML
> > 
> > ![[Pasted image 20241120132954.png]]
> 
> > [!info]- Edge cache: Netflix Open Connect
> > ![[Pasted image 20241120133034.png]]
> > 
> > - Advantage: keep traffic near ISP, not over longer-distance cables
> > 	- ISP likes this because they pay for transit
> > 	- Netflix likes this because load times go way down for customers
> 
> > [!info]- Content Delivery Network
> > ![[Pasted image 20241120133227.png]]
> > 
> > - Reddit pays a CDN to handle most of its traffic
> > - The CDN caches Reddit pages and only sends a request to the real Reddit servers when not in cache
> > - One CDN serves ~30% of all Internet traffic
> 
> > [!info] Advantages to CDN
> > - Cheaper than paying for bandwidth
> > 	- AWS bandwidth is incredibly expensive
> > 	- Edge caches don't use real Internet bandwidth
> > - Faster load times
> > - Resilience against attacks
> 
> > [!info]- Protecting against DDOS attacks
> > - Be an expert on how to redirect Internet traffic
> > - Have ore bandwidth than attackers
> > - Limit impact to small area 
> > - CDNs are great for all of these!

