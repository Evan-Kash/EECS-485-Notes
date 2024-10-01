> [!info] JSON
> - JavaScript Object Notation
> 
> ![[Pasted image 20240929211022.png]]

> [!info] Using a REST API
> 
> ![[Pasted image 20240929211122.png]]
>
> > [!important]- P3 Info
> >
> > ![[Pasted image 20240929211144.png]]
> 
> > [!info] REST API Actions
> > - Things the client-side dynamic page is able to d 
> > - Reading
> > 	- Information about a post
> > 	- Information about a user
> > - Writing
> > 	- Adding a new post
> > 	- Adding a comment
> > 	- Delete a post
> > - Updating
> > 	- Liking or unliking a post
> 
> > [!info] REST API Verbs
> > 
> > > [!info] `POST`
> > > >[!info]-  Request
> > > > - `POST` **creates** an object
> > > > - Request includes JSON body
> > > > 
> > > >  ![[Pasted image 20240929211539.png]]
> > >
> > > > [!info]- Response
> > > > - `POST` returns `201 CREATED` on success
> > > > - Response includes a copy of the created object
> > > > 	- Object usually includes a link to itself
> > > > 	
> > > >![[Pasted image 20240929211810.png]]
> > >
> > > > [!info]- Redirecting after `POST`
> > > > - `POST` endpoints are sometimes used for web forms
> > > > 
> > > > ![[Pasted image 20240929211851.png]]
> > > > 
> > > > - In this case, sometimes the `POST` endpoint will return a 302 redirect to help the user get to a logical place
> > 
> > > [!info] `PATCH`
> > > 
> > > > [!info]- Request
> > > > - `PATCH` modifies **part of** an existing object
> > > > - Request URL includes an ID
> > > > - Request includes JSON body
> > > >   
> > > >   ![[Pasted image 20240929212105.png]]
> > > 
> > > > [!info]- Response
> > > > - `PATCH` returns `200 OK` on success
> > > > - Response includes a copy of the **entire** modified object
> > > >   
> > > >   ![[Pasted image 20240929212204.png]]
> > 
> > > [!info] `PUT`
> > > 
> > > > [!info]- Request
> > > > - `PUT` replaces an entire existing object
> > > > - Request URL includes an ID
> > > > - Request includes JSON body
> > > > - & Example: replace an entire post
> > > > - The JSON body is long, and contains a replacement value for every field
> > > > 
> > > > ![[Pasted image 20240929212320.png]]
> > > 
> > > > [!info]- Response
> > > > - `PUT` returns `200 OK` on success
> > > > - Response includes a copy of the **entire** modified object
> > > > 
> > > > ![[Pasted image 20240929212418.png]]
> > 
> > > [!info] `DELETE`
> > > 
> > > > [!info]- Request
> > > > - Request URL includes an ID
> > > > - No body in request
> > > >
> > > > ![[Pasted image 20240929212503.png]]
> > > 
> > > > [!info]- Response
> > > > - `DELETE` returns `204 NO CONTENT` on success
> > > > - No body in response
> > > > 
> > > > ![[Pasted image 20240929212622.png]]
> 
> 
> > [!info]- `NOT FOUND` Response
> >  ![[Pasted image 20240929212700.png]]
> 
> > [!info]- Status Codes
> > ![[Pasted image 20240929212807.png]]

> [!info] Safety and Idempotency
> - <span style="color:rgb(0, 112, 192)">**Safe**</span>: technical term
> 	- Read-only request
> 	- Well designed `GET` or `HEAD` request
> 	- No change to state on server
> - <span style="color:rgb(0, 112, 192)">**Idempotent**</span>
> 	- Sending the request multiple times leads to the same <span style="color:rgb(0, 112, 192)">**result**</span> on the server as sending it once
> 	- ? "If  I ask this twice, will the same thing have happened as if I asked it once?"
> 		- & Ex: deleting a file
> 
> > [!question]- Why does this matter?
> > - The Internet is a messy place - lots of network failures, network handovers, other people making requests
> > - When something is idempotent, we can retry the request
> 
> > [!info] HTTP Verbs and Idempotency
> > 
> > ![[Pasted image 20240929213248.png]]
> > ![[Pasted image 20240929213255.png]]
> > ![[Pasted image 20240929213301.png]]
> 
> > [!important] Idempotent
> > - Multiple identical requests should have the same effect *on the server* as a single request 
> > - The same request can be made twice with no negative consequences *on the server*
> > - ^ Does **not** mean that the same request always returns the same response
> > - ^ **Does** mean that a request has NO side effects
> >  - If a request fails, we can automatically try again if it is idempotent
