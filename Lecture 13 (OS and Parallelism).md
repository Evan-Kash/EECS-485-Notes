> [!info] Processes and Threads
> 
> > [!important] P4: MapReduce
> > - [[Lecture 11 (MapReduce)#^715559| MapReduce]] : divide computation among many computers
> > - P4: simulate this on one computer
> > 	- Multiple programs (processes): manager and workers
> 
> > [!info] Processes
> > - A running program
> > 
> > > [!info]- The Process Abstraction
> > > - The process abstraction for execution
> > > 	- Also sometimes called a job or a task 
> > > - A process is a program in execution
> > > 	- Programs are static entities with potential for execution
> > > - Process consists of:
> > > 	- A unique process ID (PID)
> > > 	- An address space (memory)
> > > 	- 1 or more threads (sequences of computation)
> > > 	- Some other resources (file handles, open sockets, ...)
> > > 
> > > ![[Pasted image 20241017032803.png]]
> > 
> > > [!question]- When Are Processes Useful?
> > > - Multiple things happening at once
> > > - Different programs running on the same machine
> > > - Same program running on different machines
> 
> > [!info]- Threads
> > - Multiple functions in a program running simultaneously
> >   
> > ![[Pasted image 20241017032955.png]]
> > ![[Pasted image 20241017033026.png]]
> 
> > [!info] Operating Systems Scheduling
> > - Each CPU core can run one thread at at time
> > - Every ~1-10ms, the OS can switch
> > 
> > ![[Pasted image 20241017033120.png]]
> 
> > [!question]- When Are Threads Useful?
> > - Multiple things happening at once
> > 	- Within one program
> > - May need to share data in memory
> > - Usually some slow resource
> > 	- Network server
> > 	- Controlling a physical system
> > 	- Window system
> > 	- Parallel programming
> > 
> > > [!example] Web Server Example
> > > - Receives multiple simultaneous requests
> > > - Reads web pages from disk to satisfy each request
> > >   
> > >   ![[Pasted image 20241017033402.png]]
> 
> > [!important] When to Use Processes vs. Threads
> > - **Threads** have lower overhead than processes
> > 	- Often used when threads share data with one another
> > - **Processes** provide separate address space
> > 	- Useful when there is not complete trust 
> > 	- Useful to limit the damage caused by buggy code
> > 	- Needed when threads are on different computers

> [!info] Synchronization
> - Synchronization: threads agree on ordering constraints
> - Don't allow read and write to be separated
> 	- <span style="color:rgb(255, 0, 0)">**atomic**</span> operation
> - Lock: make a region where only one thread can be inside at at time
> 
> ![[Pasted image 20241017033713.png]]

> [!info] Sockets
> 
> > [!info] Networking: OS vs. your Program
> > ![[Pasted image 20241017033826.png]]
> 
> - A process sends messages to its <span style="color:rgb(0, 112, 192)">**socket**</span> 
> - A process receives messages from its **<span style="color:rgb(0, 112, 192)">socket</span>**
> 
> > [!info]- Socket Client in Python
> > ![[Pasted image 20241017034023.png]]
> 
> > [!info]- Socket Server in Pseudo-Python
> > ![[Pasted image 20241017034053.png]]
> > ![[Pasted image 20241017034132.png]]
> 
> > [!info] Socket Server Picture
> > ![[Pasted image 20241017034124.png]]
> 
> > [!important] Sockets and P4
> > - P4 uses processes, threads, and sockets to implement a MapReduce server
> > - We need to do multiple things in parallel
> > 	- & Example: a manager and N workers
> > 		- $N + 1$ processes
> > 	- & Example: a workers task (map function) and a workers heartbeat ("I'm alive" message)
> > - Communicate between several machines
> > 	- Manager communicates with workers using sockets