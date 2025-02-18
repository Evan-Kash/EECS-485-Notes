> [!info] Text Analysis: Boolean Retrieval
> ![[Pasted image 20241118181954.png]]
> 
> > [!warning]- Key problem: ranking results
> > - 33% of clicks on top result
> > - Different ranking methods
> > 	- Words on page
> > 	- Importance of page using links
> 
> > [!goal] Goal of ranking algorithms
> > - ? Which web pages (documents) does the person searching want to find?
> 
> > [!info]- Simplest ranking algorithm: Boolean retrieval
> > ![[Pasted image 20241118182227.png]]
> 
> > [!info]- Index for Boolean retrieval
> > - **Inverted index**: words to documents
> > 
> > ![[Pasted image 20241118182317.png]]
> 
> > [!info]- Boolean search using inverted index
> > ![[Pasted image 20241118182347.png]]

> [!info] Vector Space Model
> 
> > [!info]- Boolean index to vectors
> > ![[Pasted image 20241118182507.png]]
> 
> > [!question] Why vectors?
> > - A document is a vector
> > - Each dimension represents a word
> > - \# of dimensions: \# of unique words in *all* documents
> 
> > [!info]- Vector Similarity
> > - Euclidean distance
> > 	- ![[Pasted image 20241118182644.png]]
> > - Cosine similarity
> > 	- ![[Pasted image 20241118182651.png]]
> 
> > [!info]- How to search in a vector space model
> > - Construct a vector for each document
> > - Construct a vector for the search query
> > - Find closest documents
> > 
> > ![[Pasted image 20241118182826.png]]

> [!note] TF-IDF: Term Frequency - Inverse Document Frequency
> 
> > [!abstract] Adding more information
> > - Right now, vectors contain only 0 or 1 depending on whether they contain a word
> > 	- `doc1 = [1, 1, 1, 0, 0]`
> > - @ Idea: use entire range `[0, 1]` to give more information
> > 	- `doc1 = [0.2, 0.1, 0.5, 0, 0]`
> 
> > [!info]- Term Frequency
> > - Word count
> > 
> > ![[Pasted image 20241118183055.png]]
> 
> > [!info]- Document Frequency
> > - Number of documents containing the word
> > 
> > ![[Pasted image 20241118183137.png]]
> 
> > [!info]- tf-idf Formula
> > ![[Pasted image 20241118183208.png]]
> > ![[Pasted image 20241118183238.png]]
> 
> > [!info] TF x IDF
> > - *Term-Frequency x Inverse-Document-Frequency*
> > 	- $W_{ik} = tf_{ik} \times \log{(N / n_k)}$
> > 		- $T_k$ = term $k$ in document $D_i$
> > 		- $Tf_{ik}$ = frequency of term $T_k$ in doc $D_i$
> > 		- $N$ = total \# docs in collection $C$
> > 		- $n_k$ = \# of docs in $C$ that contain $T_k$
> 
> > [!info]- TF-IDF Normalization
> > - The cosine similarity formula normalizes vectors (converts to length 1)
> > - Doing this when you store the vectors saves time when searching
> > 	- Cosine similarity becomes dot product


