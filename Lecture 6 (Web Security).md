> [!info] Hash Functions
> 
> > [!info]- Hashing Passwords
> > -  ! Bad idea: server stores password in database
> > 	- User logs in, password plain text compared
> > - $ Better idea: server hashes password using one-way hash function
> > 	- If someone gets the database, they don't get the passwords
> > 	  
> > ![[Pasted image 20240929032634.png]]
> > 
> > > [!example]- 
> > > ![[Pasted image 20240929032655.png]]
> 
> > [!info]- Rainbow Tables
> > - Compute a table of passwords and hashes 
> > 
> > ![[Pasted image 20240929032829.png]]
> > 
> > - Can use this against many different databases
> >   
> > > [!success] Protecting Against Rainbow Tables
> > > - Make sure that different people in your database with the same password have different hashes
> > > 	- Add a random number to each password
> > > 	  
> > >  ![[Pasted image 20240929032932.png]]
> > >  
> > >  - The random number is called a **salt**
> > > 	 - Different one for every user
> > > 	- You don't need to keep it secret

> [!info] Network Attacks
> - Network attacks happen as information travels between client and server
> 
> ![[Pasted image 20240929033127.png]]
> 
> > [!info]- Attack 1/3: Eavesdropping
> > - Someone else listens to what you send
> > - HTTPS means they can't understand it
> > 
> > > [!info]- Governments and Encryption
> > > - US had strict export controls on cryptography in 90s
> > > 	- Government backdoor key installed inside applications (Lotus Nodes)
> > 
> > > [!info]- Data and Law Enforcement
> > > - Data that's collected about you can be searched with a warrant
> > > 	- Google knows everywhere you've been, so law enforcement does too (geofence warrant)
> > > 	- Lists of people who searched for topics
> > > 	- E-mails and chat messages
> > 
> > > [!info]- End-to-end Encryption
> > > - Some chat apps promise that the chat provider can't read your messages 
> 
> > [!info]- Attack 2/3: MITM
> > ![[Pasted image 20240929033537.png]]
> 
> > [!info]- Attack 3/3: Replay
> > - Memorize a message and send it multiple times
> > 
> > ![[Pasted image 20240929033606.png]]
> > 
> > > [!info] Replay Attack Defense
> > > - Make every message different
> > > - Incrementing number
> > > - Random number (nonce)
> > >
> > > > [!example]-
> > > > ![[6 - Web Security - Annotated (dragged).pdf]]

> [!info] Web Attacks
> 
> > [!info] Web Attacks vs. Network Attacks
> > - Network: information as it travels
> > - Web: design of our Flask app
> 
> > [!info]- Attack 1: SQL Injection
> > 
> > ![[Pasted image 20240929034553.png]]
> > 
> > ![[Pasted image 20240929034603.png]]
> > ![[6 - Web Security - Annotated (dragged) 2.pdf]]
> 
> > [!info] Code-Data Isolation
> > - Don't mix code and data 
> > 	- If you do, treat it as data
> > - Don't mix trusted and untrusted data
> > 	- If you do, entire thing is untrusted
> 
> > [!info] Attack 2: Cross-Site Scripting
> > - If you allow users to post comments or other text, they can put HTML tags
> > - \<script\> tag loads code that will run in other user's browsers
> >   
> > ![[Pasted image 20240929034923.png]]
> 
> > [!info] Attack 3: Sybil
> > - 1 real-life user pretends to be multiple online users
> > 	- Get around bans
> > 	- Vote more than once
> > 	- Fake reviews
> > - Defenses
> > 	- Require real phone numbers
> > 	- CAPTCHAs

> [!info] Database Anonymity
> 
> - Designing databases that resist data leaks:
> 	 - Store only the data you need
> 
> > [!info]- K-anonymity
> > - At least k-rows match for any given query
> > - Downsides:
> > 	- Lose information when you transform data 
> > 	- NP-hard to find optimal k-anonymization
> > 	- If everyone in a group has the same sensitive information, k-anonymity doesn't help
> 
> > [!info]- Differential Privacy
> > ![[Pasted image 20240929035623.png]]
> > ![[Pasted image 20240929035640.png]]
> > ![[Pasted image 20240929035652.png]]

> [!info]  Timing Attack
> ![[Pasted image 20240929210856.png]]