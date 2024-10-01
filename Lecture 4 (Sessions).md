> [!abstract] Learning Objectives
> - Describe the problem that **<span style="color:rgb(0, 112, 192)">sessions</span>** solve
> - Descirbe the implementation details of sessions using **<span style="color:rgb(0, 112, 192)">cookies</span>**
> - Write `INSERT` and `SELECT` **<span style="color:rgb(0, 112, 192)">SQL database queries</span>**

> [!info] Session Solutions
> 
> > [!question]- What are sessions?
> > - How a website knows multiple requests came from the same user
> 
> > [!warning]- Challenge
> > - HTTP is <span style="color:rgb(0, 112, 192)">**stateless**</span>
> > - Solution: every HTTP request includes some data that the server gives the client (**<span style="color:rgb(0, 112, 192)">cookie</span>**)
> 
> > [!info]- Client Perspective on Session
> > ![[Pasted image 20240914161614.png]]
> 
> > [!info]- Server Perspective on Session
> > ![[Pasted image 20240914161640.png]]

> [!info] Creating Sessions
> - **<span style="color:rgb(0, 112, 192)">Server</span>** is in charge of creating sessions by setting a **<span style="color:rgb(0, 112, 192)">cookie</span>**
> 
> ![[Pasted image 20240914162402.png]]

> [!info] Cookies
> 
> > [!info]- How Cookies Work
> > ![[Pasted image 20240914162329.png]]
> 
> > [!info]- Cookies in Flask
> ![[Pasted image 20240914162532.png]]
> 
> > [!info] Securing Cookies
> > 
> > > [!info]- Cookies in Transit
> > > ![[Pasted image 20240914162618.png]]
> > 
> > > [!info]- HTTPS: Securing Connection
> > > ![[Pasted image 20240914162919.png]]
> > 
> > > [!info]- Signed/Encrypted Cookies
> > > - Adds something to the cookie so that the server can verify it wasn't changed
> > > - **Signature:** add a number to the end that only server knows how to generate/check
> > > - **Encryption:** scramble cookie so client can't read or change it
> > 
> > > [!example]- Cookie Example
> > > ![[Pasted image 20240914163212.png]]

> [!info] Digging Databases
> 
> > [!question]- Where is a Database Used?
> > - Data
> > 	- Users and passwords
> > 	- Posts, likes, comments
> > - Can't store these in variables
> > 	- ? What if program is restarted
> > 	- 
> > - sqlite3: package for storing data in **SQL database**
> 
> > [!info] Idea Behind SQL
> > - **<span style="color:rgb(0, 112, 192)">SQL</span>**: structured query language
> > - Code to tell database 
> > 	- What your data looks likesWhat data to put into database
> > 	- What data you want to read
> > - **<span style="color:rgb(0, 112, 192)">Query</span>**: statement in this language
> 
> > [!info] SQL Commands 
> > 
> > > [!info]- CREATE TABLE: describe data
> > > ![[Pasted image 20240914165621.png]]
> > 
> > > [!info]- INSERT: put data in 
> > > ![[Pasted image 20240914165645.png]]
> > 
> > > [!info]- SELECT: ask for data
> > > ![[Pasted image 20240914165712.png]]
> > 
> > > [!info]- JOIN: combine two tables
> > > ![[Pasted image 20240914165744.png]]
> 
> > [!info] JOIN vs. Python Loop
> > - Bad pseudocode
> >   
> > ![[Pasted image 20240914165826.png]]
> > 
> > - Databases are faster than your code