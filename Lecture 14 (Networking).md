> [!abstract] Agenda
> - Motivation
> - IP: Internet Protocol 
> - TCP: Transmission Control Protocol
> 	- Flow control and congestion control
> - UDP: User Datagram Protocol
> - Summary

> [!info] Distributed Systems
> - Distributed system: multiple computers cooperating on a task
> - & MapReduce: distributed system for compute
> 	- Run a program that would be too slow on one computer
> - & Google File System: distributed system for storage
> 
> > [!info]- Implementation
> > - ? How are distributed systems implemented?
> > - Threads and processes for parallelization
> > 	- Last time
> > - Networking for communication
> > 	- Today
> 
> > [!info]- Networking in a MapReduce Framework
> > - ? How does the MapReduce Manager send a new task to a worker
> > 	- Send a message over the network
> > 	- & Ex: JSON blob over TCP/IP
> > 	  
> > ![[Pasted image 20241118084708.png]]
> 
> > [!info]- Networking in Google File System
> > - ? How do chunkservers send a heartbeat message to the Main server to tell it "I'm alive"?
> > 	- Send a message over the network
> > 	- JSON blob over UDP in P4 heartbeat implementation 
> > 
> > ![[Pasted image 20241118084814.png]]


> [!note] IP: Internet Protocol
> - ? How to get a message from one computer to another computer?
> 	- $ Solution: Internet Protocol (IP)
> - & Examples of messages:
> 	- MapReduce Manager server assigns task to Worker
> 	- GFS chunkserver tells Main server "I'm alive"
> 	- `GET` request from a client web browser to an HTTP server
> 
> ![[Pasted image 20241118102421.png]]
> 
> 
> 
> > [!info]- IP Address
> > - There are lots of computers connected to the internet
> > - ! Problem: how to tell them apart?
> > 	- $ Solution: IP Address
> > - Every computer on the Internet has an address
> > 	- & Google: 172.217.5.14
> > - Newer version: longer addresses
> > 	- IPv4: 32 bits = 4 billion computers
> > 	- IPv6 bits is way more
> > - ? How do you turn a URL into an IP address?
> > 	- $ Domain Name Service (DNS)
> > 	  
> > > [!question]- What is My IP Address?
> > > - Your internet service provider gives you an IP address when you connect to the wifi (or wired) network
> > > - Popular search engines provide your externally visible IP address
> > > 	- If you're on a home network, this is likely the UP address of your router
> > > - At the command line:
> > > 	 - `$ curl ipinfo.io/ip`
> 
> > [!info]- Routers
> > - ? How do we connect all the computers on the Internet?
> > 	- $ Routers
> > - A *router* forwards data from one network to the next
> > - Usually a purpose-built Linux computer withe multiple network connections
> > 
> > ![[Pasted image 20241118103029.png]]
> > 
> > > [!info] Routing
> > > - A router is connected with many other routers
> > > - ! Problem: where to send data?
> > > - Solution: one step closer to the destination
> > > - Each router has a *routing table*
> > > 	- Map groups of IP addresses to destination
> > > 	- Destination could be another router
> > > - Look up first few bits of destination IP address in routing table
> > > 	- *Longest prefix matching*
> > 
> > > [!info]- Tracing A Route
> > > - See the route from your computer to aws.amazon.com
> > > 	- Each step is called a *hop*
> > > 
> > > ![[Pasted image 20241118103310.png]]
> > 
> > > [!info]- Internet Geolocation
> > > - *Internet geolocation* tells us where a device is located
> > > - Database maps IP address to approximate location
> > > - At the command line:
> > > 	- Get `API_KEY` from ipgeolocation.io dashboard
> > > 
> > > ![[Pasted image 20241118103427.png]]
> 
> > [!info]- Packets
> > - Message broken down into packets by sender
> > 	- ~1,000 - 1,500 B each
> > 
> > > [!question] Why Packets?
> > > - Multiple programs on one computer can share one connection
> > > 
> > > 	  ![[Pasted image 20241118103553.png]]
> > > 	  
> > > - Multiple computers can share one connection
> > >   
> > > 	  ![[Pasted image 20241118103619.png]]
> 
> > [!important] IP Summary
> > - ? How to get a message from one computer to another computer?
> > 	- $ Internet Protocol (IP)
> > - ? How to tell computers connected to the internet apart?
> > 	- $ IP Address
> > - ? How are computers connected?
> > 	- $ Routers
> > - ? How are long messages broken up? How do multiple computers share one network link?
> > 	- $ Packets


> [!note] TCP: Transmission Control Protocol
> 
> > [!error] IP is not reliable
> > - ! Problems with IP:
> > 	- Packets may arrive out of order
> > 	- Packets may disappear
> > 	- Packets may be repeated
> > - TCP: abstraction to make it look like these problems don't exist
> > - TCP/IP: TCP along with IP
> 
> > [!warning]- Packets may arrive out of order
> > - ! Problem: packets may arrive out of order
> > 	- $ Solution:
> > 		1. Sender assigns a *sequence number* to each packet
> > 		2. Receiver reassembles packets in order by *sequence number*
> > 		3. Receiver gives data to application (e.g. browser) in order
> >
> > > [!example]- Out of Order
> > >  
> > >  ![[Pasted image 20241118104114.png]]
> > 
> > > [!example]- In Order
> > > 
> > > ![[Pasted image 20241118104206.png]]
> 
> > [!warning]- Packets may disappear
> > - ! Problem: packets may disappear
> > 	- $ Solution: sender stores data in buffer until receiver `ACK`
> > 		1. Sender stores a copy of each packet
> > 		2. Sender sets a timer for each packet
> > 		3. Receiver sends an `ACK` (acknowledgement) for each packet
> > 		4. Sender resends the packet if the timer expires
> > 			1. Delete the packet upon receiving `ACK`
> > 
> > > [!example]- Packet `ACK` example
> > > 
> > > ![[Pasted image 20241118104419.png]]
> > 
> > - ? What happens if the packet disappears?
> > 	- $ Sender resends the packet if the timer expires
> > 	  
> > > [!example]- Disappearing packet example
> > > 
> > > ![[Pasted image 20241118104517.png]]
> 
> > [!warning]- Packets may be repeated
> > - ! Problem: packets may be repeated
> > 	- $ Solution: receiver ignores sequence numbers it has seen before
> > - ? Why would a packet be repeated?
> > 	- `ACK` is dropped
> > 	- Packet is slow
> > -  @ Let's look at an example of a slow packet
> > 
> > > [!example]- Repeated/slow packet example
> > > 
> > > ![[Pasted image 20241118104738.png]]
> 
> > [!important] TCP Summary
> > - ! Problem: IP is not reliable
> > 	- $ Solution: TCP along with IP (TCP/IP)
> > - ! Problem: packets may arrive out of order
> > 	- $ Solution: TCP buffers reassemble packets using *sequence numbers*
> > - ! Problem: packets may disappear
> > 	- $ Solution: TCP resends lost packets
> > - ! Problem: packets may be repeated
> > 	- $ Solution: TCP receiver ignores duplicate sequence numbers

> [!info] Flow and Congestion Control
> 
> > [!warning]- Fast sender, slow receiver
> > - ! Problem: fast sender overloads a slow receiver
> > - For example, sender is an AWS datacenter server and receiver is a smart watch
> > 
> > ![[Pasted image 20241118175424.png]]
> 
> > [!info]- Flow Control
> > - ! Problem: fast sender overloads a slow receiver
> > 	- $ Solution: *flow control*
> > - Receiver tells the sender it has N empty buffer entries
> > - Sender puts N packets on the network at one time
> > - This is called the *sliding window*
> > 	- AKA *receiver window*
> > 	- AKA *RWND*
> > 
> > ![[Pasted image 20241118175630.png]]
> > 
> > > [!example]- Exercise
> > > - ? If the sender has lots of data to send, which of these situations will occur when the sliding window is working properly
> > >   
> > > 	- **A. The receiver's queue will usually be almost full**
> > > 	- B. The receiver's queue will usually be about half full
> > > 	- C. The receiver's queue will usually be almost empty
> > > - ^ Goal: maximize the use of resources (receiver buffer) without overloading it
> 
> > [!info]- Congestion Control
> > - ! Problem: many senders overload a network center
> > 	- Routers have buffers
> > 	- Router drops packets when buffer is full
> > 
> > ![[Pasted image 20241118180042.png]]
> > 
> > > [!example]- Example
> > > 
> > > ![[Pasted image 20241118180119.png]]
> > 
> > > [!info]- TCP Congestion Window
> > > - Sender maintains a *congestion window*
> > > 	- Maximum packets awaiting acknowledgements
> > > 	- AKA *CWND*
> > > - Decrease congestion window when sender loses a packet
> > > 	- Assumes that a router dropped a packet because it was too busy
> > > - Increase congestion window when sender receives an `ACK`
> > > 	- Packet got there safely, maybe there's room to send more
> 
> > [!important] Summary
> > - Flow control (AKA sliding window)
> > 	- Keep a *fast sender* from overloading a *slow receiver*
> > - Congestion control
> > 	- Keep a *set of senders* from overloading the *network*
> > - ^ We need both!
> > 	- TCP flow control: receiver window (RWND)
> > 	- TCP congestion control: congestion window (CWND)
> > - @ TCP window: `min(RWND, CWND)`
> > <br>
> > - ! Problem: fast sender overloads a slow receiver
> > 	- Solution: *TCP Flow control* AKA *sliding window*
> > 		- Sender limits number of packets
> > - ! Problem: many senders overload a network router
> > 	- $ Solution: *TCP Congestion control*
> > 		- Sender limits number of packets

> [!info] UDP: User Datagram Protocol
> 
> > [!error]- TCP isn't good for everything
> > - TCP's reliability mechanism can cause packets to be late
> > 	- "Better late than never"
> > - ? What will happen in a video chat app that uses TCP if packets 0 and 2-100  have been received but packet 1 has not?  
> > 	 -  ![[Pasted image 20241118180840.png]]
> >  - @ Application waits for packets 2-100, laggy video
> 
> > [!error]- TCP: "Better never than late"
> > - ! Problem: sometimes never is better than late
> > - ? What kinds of applications?
> > 	 - Voice chat ("Voice over IP" AKA VOIP)
> > 	 - Video chat
> > 	 - Video games
> > 	 - Heartbeat messages from Workers to Main in GFS or MapReduce
> > 	 - Anything real-time
> 
> > [!info]- UDP
> > - ! Problem: sometimes never is better than late
> > 	- $ Solution: UDP "User Datagram Protocol"
> > - Don't handle:
> > 	- Packets out of order
> > 	- Dropped packets
> > - Let application decide what to do
> > - Better for real-time applications like video chat

> [!note] Sockets
> 
> > [!abstract]- Recall: TCP Buffer
> > ![[Pasted image 20241118181328.png]]
> 
> > [!info]- Socket API
> > - ? How does an application sue TCP or UDP?
> > - *Socket API*: OS functions that let applications use the network
> > - Provides the TCP buffers that store packets
> > - Implements the TCP sliding window
> 
> > [!info]- Two Programs Share the Network
> > - ! Problem: two programs use the network at the same time
> > 	- $ Solution: two sockets, each with its own buffer
> > 
> > ![[Pasted image 20241118181548.png]]
> 
> > [!info]- Ports
> > - ! Problem: how to tell sockets apart?
> > 	- $ Solution: each socket gets a unique *port number*
> > 
> > ![[Pasted image 20241118181720.png]]
> > 
> > > [!example] Example ports
> > > - One server (host) runs two programs (processes) that use the network
> > > 	- Nginx listens for incoming HTTP requests on port 80
> > > 	- SSHD listens for incoming connections on port 22
> > > - Both processes run on the same host using *different ports*

