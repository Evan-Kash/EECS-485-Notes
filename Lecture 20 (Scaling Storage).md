> [!info] Distributed Databases
>  
> > [!abstract]- Review: Scaling dynamic pages
> > ![[Pasted image 20241124203731.png]]
> 
> > [!info] Network database 
> > - Many dynamic pages servers make network requests to one network database
> > - *Network database*: database software runs on a different server on the network
> > 	- & Ex: PostgreSQL, MySQL, et al.
> > - *Centralized network database*: one server
> > - *Distributed network database*: multiple servers
> 
> > [!info] Distributed network database
> > - *Distributed network database*: many network database servers
> > - ! Problem: how to keep database servers in sync?
> > 	- $ Solution: data consistency is hard, depends on which servers contain which data
> > - ! Problem: which servers contain which data?
> > 	- $ Solution 1: sharding by content
> > 	- $ Solution 2: database replication
> 
> > [!note]- Sharding by content
> > - Different rows or tables on different DB servers
> > - ! Weaknesses:
> > 	- Increase latency (might need to go through a master, might need to search multiple shards)
> > 	- Some searches slow
> > 
> > ![[Pasted image 20241124204356.png]]
> 
> > [!note]- Database replication
> > - Multiple copies of the entire database
> > - ! Downside: all copies need to maintain same state
> > 	- Write to one needs to propagate to all the others
> > 	- Moments of inconsistency: post shows up for some people and not others
> > 
> > ![[Pasted image 20241124204521.png]]
> 
> > [!example] Practical database examples
> > - We'll compare 3 widely used software packages:
> > 	 - SQLite
> > 	 - PostgreSQL
> > 	 - MongoDB
> > 
> > > [!info]- SQLite
> > > - Database for one program/user
> > > - Competitor: text files
> > > - Many programs have a credits or "open source licenses" screen where they list libraries they use
> > > 	- Cars, TVs, ...
> > > 	- sqlite is on basically all of them
> > > 
> > > > [!info]- Testing SQLite
> > > > - You have to really trust your database
> > > > - Fuzz testing:
> > > > 	- Generate lots of random SQL statements
> > > > 	- Guided fuzzing: track which sides of if/else statements random statements activate to make better random test cases
> > 
> > > [!info]- PostgreSQL
> > > - Networked SQL server
> > > 	- Program doing the query doesn't need to be same machine as stores database
> > > - Multi-user
> > > 	- Users can have permissions to read vs. write, and different permissions for different tables
> > > - Can do sharding and replication among multiple servers
> > > 
> > > > [!info]- Replication with Postgres
> > > > - Log shipping: similar to GFS manager fallback
> > > > 	- ![[Pasted image 20241124205006.png]]
> > > > - Streaming replication
> > > > 	- ![[Pasted image 20241124205023.png]]
> > > 
> > > > [!info]- Preventing data loss
> > > > - Synchronous replication: guarantee a write to a replica before client sees success
> > > > 	 - ![[Pasted image 20241124205132.png]]
> > > > - Asynchronous: faster, less safe
> > > > 	- ![[Pasted image 20241124205241.png]]
> > 
> > > [!info]- MongoDB
> > > - NoSQL: instead of rows/columns, store JSON data
> > > 	- Schema (list of columns) is optional
> > > - Advantage: remove the tedious SQL → JSON step
> > > - Disadvantage: SQL column structure helps keep data clean
> > > 
> > > > [!info] MongoDB queries
> > > > ![[Pasted image 20241124205614.png]]

> [!info] CAP Theorem
> 
> > [!info]- CAP theorem overview
> > - CAP theorem describes options when designing a distributed database
> > 
> > ![[Pasted image 20241124205837.png]]
> 
> > [!info] CAP theorem
> > - 3 properties we might want our database to have:
> > 	- **Consistency**: every read receives the most recent write or an error
> > 	- **Availability**: every request receives a (non-error) response, without the guarantee that it contains the most recent write
> > 	- **Partition-tolerance**: the system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes
> > - CAP Theorem: you can have CP or AP but not CAP
> 
> > [!info]- Network working correctly
> > - When the network is working correctly, you get Consistency and Availability
> > - Database serves can synchronize
> > - There is no partition
> > 
> > ![[Pasted image 20241124210156.png]]
> 
> > [!info]- Network partition
> > - When a network failure occurs, database servers cannot synchronize
> > 	- This is a partition
> > - We have a choice:
> > 	- Return an incorrect value: AP
> > 	- Return an error: CP
> > 
> > ![[Pasted image 20241124210329.png]]
> 
> > [!question] Which to choose?
> > - Prioritize consistency over scaling (CP)
> > 	- Relational databases (AKA RDBMS AKA SQL)
> > 	- PostgreSQL: synchronous replication
> > - Prioritize scaling over consistency (AP)
> > 	- Many NoSQL databases
> > - Avoid the problem:
> > 	- Buy a giant server for your DB so there's only one
> > 	- *Centralized network database*

> [!info] Distributed File Systems
> 
> > [!info]- Media uploads and the database
> > - Media uploads: Instagram photos, TikTok videos, etc.
> > - ! Problem: media uploads are expensive to store in a database
> > 	- $ Solution: store to disk
> > - Write once, read many times. Don't need a database to maintain consistency
> > 
> > > [!info]- Scaling media uploads
> > > - Different dynamic pages servers on every request
> > > 	- Physical machines, virtual machines, containers
> > > - ! Problem: how do dynamic pages server disks stay in sync?
> > > 	- $ Solution: dynamic pages servers are stateless. Store media uploads on network storage
> > 
> > > [!info]- Properties of media uploads
> > > - Media uploads have something in common with both static pages and dynamic pages
> > > - Media uploads are like static pages
> > > 	- Once they're uploaded, they never change
> > > - Media uploads are like dynamic pages
> > > 	- Content created by users
> > > 	- Access permissions per-user
> 
> > [!info]- Media storage implementation
> > - Two subproblems for media storage
> > - ! Problem 1: store the files
> > 	- Many files
> > 	- Large size
> > 	- Exabytes of data $(10^{18})$
> > - ! Problem 2: serve the files
> > 	- Many requests
> > 	- Permissions control per-user
> > 
> > > [!info]- Store the files
> > > - ! Problem 1: store files
> > > 	- $ Solution 1: network file system
> > > 		- & E.g. CAEN home directory
> > > 	- $ Solution 2: distributed file system
> > > 		- & E.g. GFS
> > > 
> > > > [!success]- Solution 1: Network file system
> > > > - *Network file system*: access files over the network much like local storage (hard drive)
> > > > ![[Pasted image 20241124211250.png]]
> > > > 
> > > > > [!important] Network file system pros and cons
> > > > > - Network file system acts like a local file system
> > > > > 	- Near zero code changes
> > > > > - ! Problem 1: speed and scalability
> > > > > - ! Problem 2: fault tolerance
> > > > > 	- ? What happens when the network file system server goes down?
> > > > > - Network file systems weren't designed with the scale of the web in mind
> > > 
> > > > [!success]- Solution 2: Distributed file system
> > > > - *Distributed file system*: access files over the network, often with a special API
> > > > - Reliable, scalable file storage implemented with commodity hardware
> > > > - & GFS is an historical example
> > > > 
> > > > > [!important] Distributed file system pros and cons
> > > > > - Distributed file systems are more scalable and fault tolerant than network file systems
> > > > > - Distributed file systems often use a special API
> > > > > 	- Requires code changes
> 
> > [!important] Network FS vs. Distributed FS
> > - Technically, both are distributed systems
> > - Optimized for different things
> > - *Network file system* is optimized to be as similar as possible to traditional file system
> > - *Distributed file system* is optimized for scale and reliability on unreliable hardware
> 
> > [!info]- Connecting dynamic pages servers to distributed file system
> > - Our data is now stored in a distributed file system
> > 	- User connects to dynamic pages web server
> > - ! Problem: how do we upload and download?
> > 	- $ Solution 1: dynamic pages server is a middleman between client and distributed file system
> > 	- $ Solution 2: client connects directly to distributed file system
> > 
> > > [!success]- Solution 1: Media upload proxy
> > > ![[Pasted image 20241124212222.png]]
> > 
> > > [!success]- Solution 2: Direct upload
> > > ![[Pasted image 20241124212247.png]]