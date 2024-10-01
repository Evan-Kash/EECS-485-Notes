> [!abstract] Learning Objectives
> - Use python to access **<span style="color:rgb(0, 112, 192)">sqllite databases</span>**
> - Constrast **<span style="color:rgb(0, 112, 192)">symmetric and asymmetric encryption</span>**
> - Identify how **<span style="color:rgb(0, 112, 192)">certificate authorities</span>** enable **<span style="color:rgb(0, 112, 192)">HTTPS</span>** to work
> - Use **<span style="color:rgb(0, 112, 192)">hash functions and salts</span>** to securely store passwords

> [!info] Tuples and Commas
> ![[Pasted image 20240914170058.png]]

> [!info] Encryption Basics
>  
> > [!info]- Network Security
> >  - Two parties communciate over a network
> > - Assume powerful adversary
> > 	- Can read (eavesdrop on) all data transmitted
> > 	- Can modify or delete any data
> > 	- Can inject new data
> > 	  
> > ![[Pasted image 20240914170210.png]]
> > 
> > - Communication: what properties would you like?
> 
> > [!info] Desirable Properties
> > - Confidentiality
> > 	- Adversary should not understand message
> > - Sender authenticity
> > 	- Message is really from the purported sender
> > - Message integrity
> > 	- Message not modified between send and receive
> 
> > [!info]- Encryption Terminology
> > ![[Pasted image 20240914170508.png]]

> [!info] Symmetric vs. Asymmetric Ciphers
> 
> > [!info] Symmetric Encryption
> > - Encryption and decryption key are the same
> > 	- $k_{enc} = k_{dec}$
> > 
> > > [!info]- AES
> > > - "Advanced Encryption Standard"
> > > - Most common symmetric cipher
> > > - Block cipher (128 bits)
> > > <br>
> > > - Old symmetric cipher: DES 
> > > 	- Now insecure
> > 
> > > [!question]- What Makes a Good Symmetric Cipher?
> > > - Nobody knows how to break it
> > > - Break: if I have cipher, find the plaintext faster than guessing the keys
> > > - ? Is AES secure?
> > > 	- $ No formal proof, but we haven't found any effective attacks yet
> > 
> > > [!important]- Strengths and Weaknesses of Symmetric Encryption
> > > - **<span style="color:rgb(0, 176, 80)">Strengths</span>**:
> > > 	- Fast 
> > > - <span style="color:rgb(255, 0, 0)">**Weaknesses**</span>:
> > > 	- ? How do you share the key?
> > > 	- ? If you build a key together (Diffie-Hellman), how do you know you are doing it with the right other person?
> 
> > [!info] Asymmetric Encryption
> > - **Two keys** that are inverses of each other
> > 	- Keep one **<span style="color:rgb(0, 112, 192)">private</span>**, make the other <span style="color:rgb(0, 112, 192)">**public**</span>
> > 
> > ![[Pasted image 20240914171058.png]]
> > 
> > > [!question]- What Can We Do With Asymmetric Encryption?
> > > - Send a message only one person can read (**<span style="color:rgb(0, 112, 192)">encrypt</span>**)
> > > 
> > > 	  ![[Pasted image 20240914171215.png]]
> > > 
> > > - Prove that it was me that sent a message (**<span style="color:rgb(0, 112, 192)">sign</span>**) 
> > > 	
> > > 	![[Pasted image 20240914171405.png]]
> > 
> > > [!info]- Designing Asymmetric Cryptography
> > > - Need mathematical way to make two related keys
> > > - Hard as possible to figure out private key
> > > 	- Assume everyone knows public key
> > > - Idea: "trapdoor functions"
> > > 	- $b = f(a)$
> > > 	- Make it hard to find $a$ given $b$ (have to guess)
> > 
> > > [!info]- Trapdoor Functions
> > > - $n = p \times q$, where $p$ and $q$ are primes
> > > 	- Given $p$ and $q$, easy to compute $n$
> > > 	- Given $n$, very hard to find $p$ and $q$
> > > - Public, private keys require original primes to compute
> > > 	- Only product of primes is ever exposed
> > > 	- Computationally extremely challenging to recover original primes

> [!info] Public Key Infrastructure
> - Asymmetric cryptography depends on sharing public keys
> - ? How do you know that Amazon's public key actually comes from Amazon?
> 
> > [!example]- MITM Attack
> > ![[Pasted image 20240914171923.png]]
> 
> > [!info] Certificate Authorities
> > - There are companies called "Certificate Authorities"
> > 	- Verisign, Let's Encrypt 
> > 
> > ![[Pasted image 20240914172013.png]]
> > 
> > > [!info]- Trust in Certificate Authorities
> > > - Any CA can generate certificates for any website
> > > 	- 2015: rogue employees at Symantec generated fake certificates for google.com 
> > > - Certificate Transparency System
> > > 	- Public log of certificates that are created
> > > 	- Kind of like a blockchain for certificates
> 
> > [!info]- Chain of Trust in Your Computer
> > ![[Pasted image 20240914172202.png]]
> 
> > [!info]- HTTPS
> > ![[Pasted image 20240914172227.png]]
> > 
> > > [!info] HTTPS View 2
> > > ![[Pasted image 20240914172242.png]]

> [!info] Hash Functions
> 
> > [!info]- Hashing Passwords
> > 
> > ![[Pasted image 20240914172329.png]]
> > 
> > - Better idea: server hashes password using one-way hash function
> > - If someone gets the database, they don't get the passwords
> >   
> > > [!example] SHA-512 Hashing Example
> > > ![[Pasted image 20240914172413.png]]
> 
> > [!warning]- Rainbow Tables
> > - Compute a table of passwords and hashes
> > - Can use this against many different databases
> > 
> > > [!solution] Protecting Against Rainbow Tables
> > > - Make sure that different people in your database with the same password have different hashes
> > > 	- Add a random number to each password
> > > 
> > > ![[Pasted image 20240914172557.png]]
> > > 
> > > - The random number is called a salt 
> > > 	- Different one for evert user
> > > - You don't need to keep it a secret
> 
> > [!info] Salts
> > 
> > > [!info]- Storing Passwords
> > > ![[Pasted image 20240914172717.png]]
> > 
> > > [!info]- Verifying Passwords
> > > ![[Pasted image 20240914172746.png]]