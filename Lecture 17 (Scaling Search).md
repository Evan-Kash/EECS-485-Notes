> [!info] Web Crawling
> - Review: last two lectures
> 	- IR1: find matching documents
> 	- IR2: Using link graph
> - To search Internet, need to build index and link graphs
> - Download the entire Internet
> - ! Problem: no list of all pages
> 	- $ Solution: do a traversal of the link graph
> 
> ![[Pasted image 20241120124822.png]]
> 
> > [!info] Web crawling: graph traversal
> > - Have a list of "seed pages", follow all links like a BFS/DFS
> > 	- Most of the Internet is a connected component
> 
> > [!warning]- Problem 1: Client-side dynamic pages
> > - Can't pull data out
> > 
> > ![[Pasted image 20241120125056.png]]
> 
> > [!warning]- Problem 2: Not nice to websites
> > - Crawlers generate a **lot** of traffic
> > 	- CPU and bandwidth costs money
> > - Website owners don't like if you crawl too fast and will block you
> > - $ Solution: limit \# of requests per sire per second
> 
> > [!warning]- Problem 3: Not all sites want to be indexed
> > - Websites generally like being on search engines
> > - Reasons not to:
> > 	- Personal creations
> > 	- Parts of dynamic websites
> > - $ Solution: robots.txt
> 
> > [!info]- robots.txt
> > - Defines what crawlers can do
> >   
> > ![[Pasted image 20241120125331.png]]
> 
> > [!problem] Problem 4: Deduplication
> > - Many web pages are exact copies of other web pages
> > 	- Only create index once
> > - We'll learn how to solve this in the next segments

> [!info] Deduplication
> 
> > [!warning] Problem to solve
> > - Many web pages are duplicates or near-duplicates
> > 	- News websites: many have exactly the same articles
> > - Indexing takes CPU time, so want to run index algorithm once for all duplicates
> > - ? How to detect duplicate pages in an efficient way?
> 
> > [!info] Straightforward algorithm
> > - Define a hash of a document
> > 	- Hash("It grows in dry places...") = 8d2fgo8
> > - When crawling a document:
> > 	- Compute its hash
> > 	- Look that up in a hash table
> > 	- If present, it's a duplicate
> > 	- If not, put in the hash table
> > 
> > > [!question] Why not do this?
> > > - Documents can be *almost* similar but not exactly similar
> 
> > [!info]- Quantifying Similarity
> > - Property of pairs of documents A and B
> > - Treat documents as sets of words
> >   
> > ![[Pasted image 20241120125925.png]]
> > - Jaccard Similarity 
> > 
> > ![[Pasted image 20241120130009.png]]
> 
> > [!info]- Shingles: give context
> > - Instead of words, use "shingles": sequences of $k$ words
> > - ? Why?
> > 	- $ Context reduces noise in similarity
> > 
> > ![[Pasted image 20241120130125.png]]
> 
> > [!info]- Combining Jaccard Similarity and Shingles
> > - Crawl document
> > - Compute 3-shingles
> > - Compute Jaccard similarity with all previous documents using sets of shingles
> > - If similar enough, it's a duplicate

> [!info] MinHash
> 
> > [!info]- Improving efficiency
> > - Jaccard similarity requires computing the size of set intersection and union
> > - Repeat this work for every pair of pages
> > - ^ Goal: pre-compute some information about every page which makes computing Jaccard similarity faster
> 
> > [!info]- Trick: compute hashes
> > - Given a hash function
> > - Compute hash of each shingle for documents A and B
> > 
> > ![[Pasted image 20241120130436.png]]
> 
> > [!info]- Trick: find minimum hash
> > ![[Pasted image 20241120130459.png]]
> > 
> > - If the minimum hash is equal, signs of similarity
> > - ? What is the probability that minimums will be equal?
> > 	- Equal to Jaccard similarity
> 
> > [!info]- Why this works
> > ![[Pasted image 20241120130640.png]]
> 
> > [!info]- Many hash functions
> > ![[Pasted image 20241120130712.png]]
> > - Each is run 1 or 0 (for T/F)
> > - To converge on a value, repeat it with different hash functions for different random orderings
> 
> > [!info]- MinHash signatures
> > - Ahead of time, we can compute *signatures* for documents
> > - Given hash functions h1, h2, h3, ...
> > 
> > ![[Pasted image 20241120130838.png]]
> 
> > [!info]- Comparing using signatures
> > ![[Pasted image 20241120130915.png]]
> 
> > [!note]- Similar Idea: SimHash
> > - Combine partial hashes into a large hash
> > 
> > ![[Pasted image 20241120130955.png]]
> > 
> > > [!info]- Properties of SimHashes
> > > - Can measure Hamming distance between SimHashes
> > > 	- Hamming distance: \# of different bits
> > > 	- Lower distance = more similar

> [!info] Distributing Search
> - ! Problem: inverted index is too big for one machine
> 	- Billions of docs
> - ! Problem: query load is too big for one machine
> 	- Billions of queries
> - ! Problem: a machine could fail
> - $ Solution: parallel query processing
> 	- Segment by term
> 	- Segment by document
> 
> > [!info]- Segment by term
> > ![[Pasted image 20241120131306.png]]
> 
> > [!info]- Segment by document
> > ![[Pasted image 20241120131402.png]]

