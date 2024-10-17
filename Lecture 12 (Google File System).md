> [!info] How Facial Recognition Works
> ![[Pasted image 20241017025725.png]]
> 
> > [!info] Clearview AI
> > - Build database of faces on the Internet and make ti searchable by picture
> > - Sell access to that database to law enforcement and others
> > - ACLU v. Clearview AI
> > 	- Settlement: "*permanently bann[ed] Clearview from making its faceprint database available to most businesses and other private entities nationwide*"
> 
> > [!question] What Can We Do as Web Developers
> > - ? Do we encourage people to overshare?
> > - ? Is user data public or private by default? Can it be crawled by outsiders
> > - ? Is user data permanent? 

> [!info] Google File System
> - ^ Goal: store more data than fits on one computer
> 
> > [!info]- Inside a Datacenter
> > - What it's like
> > 	- Very loud fan noise
> > 	- Hot in some spots and really cold in others
> > 	- Unique smell
> > - Lots of computers means lots of failures
> > 
> > > [!info] Datacenter Failures
> > > - Old strategy: buy a small number of expensive servers
> > > - New strategy: buy lots of unreliable cheap servers
> > > 	- Use software to make them look reliable and fast
> 
> > [!question] Why GFS?
> > - Store enormous amount of data
> > - In a way that data is not lost when some servers crash or stop working
> > - $ Solution:
> > 	- Store multiple copies of everything
> > 	- Keep track of where those copies are
> 
> > [!question] Why Learn About This?
> > - GFS is a **distributed system**
> > 	- No one computer is in charge of everything
> > - MapReduce: distributed computation
> > - GFS: distributed storage
> > - Why distributed system in 485: see what the challenges are and what solutions look like

> [!info] GFS Structure and Reading
> 
> > [!info]- GFS Terms
> > - Files are divided into **chunks**
> > 
> > ![[Pasted image 20241017030804.png]]
> > 
> > - There is one **manager** that knows where chunks are
> > - There are many **chunkservers** that store data
> 
> > [!info]- GFS Design - Read
> > ![[Pasted image 20241017030909.png]]
> > ![[Pasted image 20241017030935.png]]

> [!info] GFS Writes
> 
> > [!info] Data Duplication
> > - Because chunkservers can fail, GFS makes backups of itself
> > - Each chunk is stored on multiple chunkservers
> > - That means that when the data inside a chunk updates, every copy needs to be updated
> 
> > [!info] Writing
> > - There are some problems with handling writes the same way as reads 
> >   
> > ![[Pasted image 20241017031125.png]]
> 
> > [!info]- Consistency
> > - Consistent: every chunkserver writes a given chunk <span style="color:rgb(0, 112, 192)">**in the same order**</span> as other chunkservers
> > - This sin't the same as "consistent" in English
> > - Consistency **does not** guarantee each chunkserver has the same valeu for the chuk at every instant
> > 
> > ![[Pasted image 20241017031303.png]]
> 
> > [!info]- Defined
> > - *Defined*: changes from different writers did not get mixed up together **for a file made up of multiple chunks**
> > 
> > > [!info] Undefined
> > > 
> > > ![[Pasted image 20241017031451.png]]
> 
> > [!info] GFS Guarantee
> > - GFS is designed for consistency
> > 	- Every chunkserver has same data for one chunk
> > - Applications need to detect and handle undefined parts of files
> > 	- At Google: did this by appending, not writing
> > - ? Why not guarantee more?
> > 	- In a distributed system, this is really, really hard

> [!info] Consistency Using Write Forwarding
> 
> > [!info] Write Forwarding
> > - To guarantee consistency, writes need to be ordered in one place
> > 
> > ![[Pasted image 20241017031714.png]]
> 
> > [!question] How This Produces Consistency
> > - Goal is an ordering of which client wrote the chunk in which order
> > - There is only one primary for a chunk at once
> > - The primary decides on an order
> > 
> > ![[Pasted image 20241017031829.png]]
> > - @ Note: this is a simplication, in real GFS:
> > 	- Writers send data first to all chunkservers, then primary commits them in a logical order
> 
> > [!info] Record Append
> > - We had to give up the "defined" property
> > - But we can still get a guaranteed ordering if we only allow appending
> > 
> > ![[Pasted image 20241017031950.png]]

> [!info] GFS Fault Tolerance
> - Failed chunkserver
> - Failed manager
> 
> > [!info] Chunkserver Fault Tolerance
> > - Chunkserver report to manager every few seconds
> > 	- *Heartbeat* message
> > - If the manager loses the heartbeat, marks the server as down
> > - Manager asks chunkservers to reduplicate data
> > - Typically 3 copies of every chunk
> 
> > [!info] Manager Failure
> > - Manger maintains critical data structures
> > 	- filename → chunkid map
> > 	- chunkid → location map
> > - Manager writes a log to disk when data structures change
> > - **Shadow manager** consumes log and keeps copies of these data structures up-to-date
> > - If manager goes down, shadow manager provides read-only access until manager restart

> [!abstract] GFS Summary
> 
> > [!success] GFS Strengths
> > - Store lots of data
> > - Fault tolerant
> > 	- Too big to back up!
> > - High *throughput*
> > 	- Can read lots of data from many chunkservers at same time
> 
> > [!error] GFS Weaknesses
> > - Bad for small files
> > 	- Chunks are ~64 MB
> > - Manager node single point of failure
> > - High *latency*
> > 	- Talk to two servers to fetch any data, might need multiple chunks