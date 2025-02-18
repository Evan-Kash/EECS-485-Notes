> [!info] Linked-Based Ranking
> 
> > [!info]- Document Importance
> > - Search for "Python threads"
> > - ? Which document is more likely to be what I am looking for?
> > - ? How can we measure importance?
> 
> > [!example] Link Graph
> > ![[Pasted image 20241120025549.png]]
> 
> > [!info]- Using the link graph importance
> > - Ideas:
> > 	- If lots of pages link to a page, it is important
> > 		- ![[Pasted image 20241120025710.png]]
> > 	- If an important page links to a page, that page is also important
> > 		- ![[Pasted image 20241120025720.png]]

> [!info] PageRank
> - Humans know better than computers which pages are important
> - Humans indicate importance through links
> 	- Like citations on an academic paper
> 
> > [!info] PageRank Model
> > - Assume someone starts on a random web page
> > - They click a random link on that page
> > - They do this over and over
> > - For each page on the Internet, how often do they visit a page?
> 
> > [!info] Random Walk
> > ![[Pasted image 20241120030440.png]]
> > 
> > > [!info] Effects
> > > - If many pages link to you, random person will be at your site more often
> > > - If you're popular, you will make the pages you link to more popular
> > 
> > > [!warning]- Problem to solve 1: Sink nodes
> > > - Some nodes do not have an outgoing path
> > > -  **Solution**: add paths from sink node to every other node
> > > 
> > > ![[Pasted image 20241120030719.png]]
> > > 
> > > - @ Idea: path chosen by sink node is random (selects on of any path)
> > 
> > > [!warning]- Problem to solve 2: sink components
> > > - Paths make a region we can can never get out of (can't break cycle)
> > > 
> > > ![[Pasted image 20241120030954.png]]
> > > 
> > > - $ Solution: add low probability paths to each node
> > > - @ Can be thought of leaving a website and searching for a new one (not through links)
> 
> > [!important]- PageRank Formula
> > ![[Pasted image 20241120031328.png]]

> [!info] PageRank Algorithm
> 
> > [!example] Example Link Graph
> > ![[Pasted image 20241120031508.png]]
> 
> > [!info] Initial Page Rank
> > - Initialize to $\frac{1}{N}$
> > - Add edges for sink nodes
> > 
> > ![[Pasted image 20241120032039.png]]
> 
> > [!info] Process
> > - Visit every node:
> > 	 - Compute node's PageRank
> >  - Loop over this many times until the PageRanks stabilize
> >    
> >  ![[Pasted image 20241120031917.png]]
> 
> > [!example]- Exercise
> > 
> > > [!note] Exercise 1
> > > - Predict then compute:
> > > 	- Highest <span style="color:rgb(255, 0, 0)">PR → 0</span>
> > > 	- Lowest <span style="color:rgb(255, 0, 0)">PR → 3</span> 
> > > 	- ? Which nodes will have the same PR? <span style="color:rgb(255, 0, 0)">→ 1, 2</span> 
> > > 	- \# of iterations to converge, <span style="color:rgb(255, 0, 0)">→ small \#</span> 
> > > 
> > > ![[Pasted image 20241120032751.png]]
> >  
> > > [!info] Exercise 2
> > > - Highest <span style="color:rgb(255, 0, 0)">PR → 0</span>
> > > - Lowest <span style="color:rgb(255, 0, 0)">PR → 2, 3</span> 
> > > - ? Which nodes will have the same PR? <span style="color:rgb(255, 0, 0)">→ 2, 3</span> 
> > > - \# of iterations to converge, <span style="color:rgb(255, 0, 0)">→ lots </span> 
> > > 
> > > ![[Pasted image 20241120032759.png]]
> 
> 
> > [!important] Combing PageRank and Text-Based Ranking (P5)
> > - Define a weight for PageRank as % of total 
> > 	- Use tf-idf for rest
> > 	- You will do this in P5
> > 
> > ![[Pasted image 20241120032940.png]]

> [!info] HITS Algorithm
> 
> > [!info]- HITS Concept
> > - Account for both links in and out of a node
> > 	- Authority score: value of content
> > 	- Hub score: value of links
> > 
> > ![[Pasted image 20241120033236.png]]
> 
> > [!info]- HITS Formula
> > - <span style="color:rgb(255, 0, 0)">Authority score</span> = sum of <span style="color:rgb(0, 112, 192)">hub</span> scores of pages that link to me
> > - <span style="color:rgb(0, 112, 192)">Hub score</span> = sum of <span style="color:rgb(255, 0, 0)">authority</span> scores of links I link to
> > 
> > ![[Pasted image 20241120033352.png]]
> 
> > [!info]- HITS Algorithm
> > - Start with a **root set** (tf-idf good matches)
> > - Build a **base set** (link to root set)
> > - Ignore all nodes and edges not in vase set
> > - Repeat until converged:
> > 	- Compute all authority scores
> > 	- Compute all hub scores
> > 	- Normalize
> > - Authority scores for root set used for ranking
> > 
> > ![[Pasted image 20241120033638.png]]
> 
> > [!info]- HITS Outcomes
> > ![[Pasted image 20241120033729.png]]
> 
> > [!info]- Combining HITS with Text-Based Ranking
> > - Put the best text-based results as root set
> > - Combine HITS authority with weight (like for PageRank)