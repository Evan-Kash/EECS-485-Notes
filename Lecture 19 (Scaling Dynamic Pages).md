> [!info] Load Balancing
> - Website grows too big for one server to support
> 
> ![[Pasted image 20241120133626.png]]
> 
> > [!info]- Round robin DNS
> > - Multiple IP address for one domain name
> > - DNS server responds to a DNS request with a *list of IP addresses*
> > - Browser can choose the best one
> 
> > [!info]- Synchronizing front end servers 
> > - ! Problem: users might contact different front end servers on every request
> > 	- ? how do all the FEs/DBs stay in sync?
> > 	- FE: only dependent on database state
> > 	- Database: hard, hard problem
> > 
> > ![[Pasted image 20241120133833.png]]
> 
> > [!info]- Sharding by content
> > - Different users or tables in different DBs 
> > - Downside: hard to keep database consistent
> > 	- foreign keys
> > 	- need to know which DB to talk to for which thing
> > 
> > ![[Pasted image 20241120133937.png]]
> 
> > [!info]- Database replication
> > - Have multiple copies of the entire database
> > - Downside: all copies need to maintain same state
> > 	- Write to one needs to propagate to all the others
> > 	- Moments of inconsistency: post shows up for some people and not others
> >
> > ![[Pasted image 20241120134104.png]]

> [!info] Data Centers
> - Buildings full of computers
> - Glass windows in BBB: can look into research data centers
>   
> > [!info]- The Internet is physical
> > - Actual physical computers store data, run code
> > - Physical wires needed to move the data around the world
> 
> > [!question]- Where do you put a data center
> > - Closes to cheap electricity
> > 	- This can be coal!
> > - Cooling
> > - Low natural disaster risk
> 
> > [!example]- Data center design
> > ![[Pasted image 20241120134324.png]]
> 
> > [!info]- Inefficiencies in data centers
> > - Any money that isn't directly spent on computers and the electricity to run them
> > - Power conversion
> > - Air conditioning
> > - Utilization
> 
> > [!info]- Heat
> > - Servers account for barely half of power
> > 	- 1W of cooling per 1.5W of IT load
> > - Managing energy consumption means, to a large extent, managing heat
> 
> > [!info]- Data center efficiency
> > - Power Usage Effectiveness (PUE)
> > 	- Total Facility Power / IT Equipment Power
> > 	- ? For each watt, how much to computing?
> > 	- 1.0 means no extra cost at all

> [!info] Cloud Computing
> 
> > [!question]- Why cloud computing?
> > - Large tech companies are very good at running data centers
> > - ? Why have your own servers when you can use a large tech company's
> > 	- Your owns servers: have to but entire server, during low utilization don't have other work to do
> > 	- Someone else's servers: rent 1 today, 100 tomorrow, 1 the day after that
> > 	- You are a software expert, not a data center expert
> 
> > [!info]- Cloud computing
> > - Rent compute, storage, network
> > - Pay based on useage
> > 	- # of CPUs, GBs of RAM, GB of bandwidth/usage
> 
> > [!question]- What IS the cloud?
> > - Three rough "levels"
> > - **Infrastructure-as-a-service**, designed for admins
> > 	- Machines, storage, network capacity; most of AWS
> > - **Platform-as-a-service**, designed for developers
> > - **Software-as-a-service**, designed for users
> 
> > [!info]- Virtualization
> > - An AWS S3 instance, like for P2 and P3 is not an entire physical server
> > 	- Most servers do nothing most of the time
> > - Insight: use VMs to have multiple customers on same hardware
> > 
> > ![[Pasted image 20241120135116.png]]
> 
> > [!info]- Containerization: Docker
> > ![[Pasted image 20241120135140.png]]
> 
> > [!info] Virtualization vs. Containerization
> > ![[Pasted image 20241120135158.png]]
