> [!info] HTTP Versions
> 
> > [!info] HTTP 1.0
> > - New connection for every file 
> > - ? How many connections will a browser send to load this web page?
> > 	- Client needs to send one to load index.html to start
> 
> > [!info] HTTP 1.1
> > - Can reuse one connection for multiple requests and responses
> > - One request and response per file
> > - ? How many connections?
> > 	- One per client
> 
> > [!info] HTTP 2.0
> > - The server can tell that certain files always get sent together, and can respond with multiple files for one request


> [!info] Static vs. Dynamic Pages
> - "Static": stays the same
> - "Dynamic": can change 
> - Point of view: the client
> - In general,
> 	- If a file is read from disk verbatim: **static**
> 		- File can be generated ahead of time
> 	- If a program generates the file only when the client requests it: **dynamic**

> [!info] Static vs. Dynamic Content
> - Static content is same every time
> - Dynamic content changes
> - Things that are impossible with simple web pages

> [!info] Dynamic Server Content
> - In the old days, almost all requests were just disk loads
> - Each request calls a function in the server software, which generates the response
> 
> > [!question] Why is this useful?
> > - Most common pattern:
> > 	- Store data in a database
> > 	- Use jinja/templates to create HTML from that data
> > 	- This way, users can change the data
> > - Call a python function, merge w/ template, generate HTML

> [!info] Principle: data/computation duality
> - We think of data and computation as **separate**
> - But, they are really **two sides of the same coin**

> [!info] URL Routing in Flask
> - Dynamic pages are created by executing a function at the time of a request
> - When a client requests a URL, how does a server know which function to call?

> [!info] Python Decorators
> 
> > [!info] First Class Objects
> > - In Python, functions are *first class objects*
> > - Recall from 280, that first class objects can be:
> > 	- Passed as input 
> > 	- Returned as output
> > 	- Created at runtime
> > 	- Destroyed at runtime 
> 
> > [!info] 