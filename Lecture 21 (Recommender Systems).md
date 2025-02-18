> [!info] Making Recommendations
> 
> > [!info]- TikTok Algorithm
> > - Recommender systems are optimizing for something:
> > 	- Happiness of users
> > 	- Amount of money you spend
> > 	- Time you spend on the site
> > 
> > ![[Pasted image 20241211062937.png]]
> 
> > [!warning]- Challenges for recommendations
> > - Every person is unique
> > 	- Have to run the alg. many times
> > 	- Don't have much data about what you're recommending
> > 		- ? Does the YouTube alg. understand **why** people like a video, or even what it's about?
> > 	- Millions of different things that could be recommended
> 
> > [!example] Case Study: Twitter
> > ![[Pasted image 20241211063201.png]]
> 
> > [!goal] Problem we're solving
> > - ? Logged in user loads the home page. Which tweets do they see?
> > - Model:
> > 	- Posts called "tweets"
> > 	- Users can follow other users
> > 	- The feed can show tweets from both people you follow and others
> 
> > [!important] Twitter Recommendation Algorithm
> > 1. **Candidate Sourcing**: gather about 1500 tweets the user might want to see
> > 2. **Ranking**: sort those in order from most interesting to the user to least interesting
> > 3. **Filtering**: fix some issues that arise, like too many tweets from blocked accounts
> 
> > [!important] Algorithms
> > - **Ranking**: uses a neural net
> > - **Filtering**: custom rules for Twitter
> > - ^ **Candidate Sourcing**
> > 	- @ This is most relevant to other web systems
> > 	- We'll focus here
> > 1. **In-Network Sourcing** (tweets from people you follow)
> > 2. **Out-of-Network Sourcing** (tweets from people you don't follow)
> > 	- Social graph (what do your friends like?)
> > 	- Embedding spaces (what do people similar to you like?)

> [!info] In-Network Sourcing: RealGraph
> 
> > [!info]- Idea: User following graph
> > - P2 and P3: how we built the home page
> > 
> > ![[Pasted image 20241211063800.png]]
> > 
> > - ! Problem: not all followers are equal
> > 
> > ![[Pasted image 20241211063821.png]]
> 
> > [!info] RealGraph: add features to edges
> > 
> > ![[Pasted image 20241211063904.png]]
> > 
> > - Add features to each edge:
> > 	- For interactions: likes, comments, ... 
> > 		- How often it happens
> > 		- How long since it happened last
> > 		- How long since the first time it happened
> > 	- Number of common friends
> > 
> > > [!note]- RealGraph: predict whether users will interact this time
> > > ![[Pasted image 20241211064725.png]]
> > 
> > > [!info]- RealGraph: learning scores
> > > - Scoring is done by ML
> > > - Prediction problem: 
> > > 	- Input: features on edges for interactions in the past
> > > 	- Predict: -1 if no interaction, 1 if an interaction
> > > - Logistic regression
> > 

> [!info] Out-of-Network: Collaborative Filtering
> - Discover clusters of content that people enjoy
> 
> > [!info]- Collaborative filtering hypothesis
> > - We don't need to understand why people like certain things, we just need to make a statistical correlation
> > - Use information that other users have provided to fill in unknown information about you
> > - **Assumption**: people tend to have similar preferences to some other people
> 
> > [!example]- Movie Ratings Example
> > ![[Pasted image 20241211065038.png]]
> 
> > [!info]- Averaging
> > - Fill in the missing scores
> > 	- Average for each item over all users
> > - ! Problem: averaging ignores uniqueness of a user
> > 	- Terrible when there is a large variation in interest
> > 	- Movies, music a few examples
> > - $ Solution: nearest neighbor algorithm
> 
> > [!solution] Nearest Neighbor Algorithm
> > - Find another user with similar properties
> > - Use other user's rating to "fill in the blank"
> > - People who agreed in the past will agree in the future
> > 
> > ![[Pasted image 20241211065340.png]]
> 
> > [!important]- Exercise
> > - @ Recall: search similarity with vector space model
> > 
> > ![[Pasted image 20241211065453.png]]
> > 
> > - ^ If we did a similar technique with users and recommendations, what would the vectors be made up of?
> > 	- $ Vector of movie ratings
> 
> > [!example]- Nearest Neighbor Diagram - Movie Ratings
> > - We'll only use two movies to make it easier to draw
> > - Use the dimensions we do have information about
> >
> > ![[Pasted image 20241211081631.png]]
> 
> > [!question] How to determine distance?
> > - Geometric
> > 	- Euclidean distance
> > 	- Cosine similarity
> > - Pair comparisons
> > 	- Pearson correlation coefficient
> > 
> > > [!info]- Pearson correlation coefficient
> > > - Each movie rated by both users is a point
> > > - Value between $+1$ and $-1$
> > > 	-  = covariance / stddev
> > > 
> > > ![[Pasted image 20241211081902.png]]
> 
> > [!info]- K-nearest Neighbors (k-NN)
> > - Can we do better than selecting just one nearest neighbor
> > - Select several
> > <br>
> > 1. Find the *k* closest users
> > 2. Combine their scores to make a recommendation
> >  
> > > [!example]- YouTube Watch History
> > > ![[Pasted image 20241211082048.png]]
> > 
> > > [!info]- k-NN Improvements
> > > - cAn suffer from bias towards popular videos
> > > 	- 0 → not watched, 1 → watched
> > > 	- Then popular videos will have higher average
> > > - $ Solution 1: make nearer neighbors count for more
> > > - $ Solution 2: insight from tf-idf: make rarely watched movies count for more
> > > 	- Inverse user frequency

> [!info] Out-of-Network: Content-Based Filtering
> 
> > [!goal] Motivation
> > - Problems with user-based collaborative filtering
> > 	- Cold start, scalability, sparsity
> > - $ Solution: focus on content instead of users
> 
> > [!info] Content-based filtering
> > - *Content-based filtering*: recommend items similar to items the suer has liked in the past
> > - People will like the same things in the future that they liked in the past
> > - We need to understand the content to do this
> > 	- & Movie: decade, genre
> 
> > [!example]- Movie Rating Example 
> > ![[Pasted image 20241211082610.png]]
> 
> > [!question] How can we compute item similarity?
> > - Similar techniques to user-based collaborative filtering
> > - Euclidean distance, cosine similarity, correlation, tf-idf
> 
> > [!info] Hybrid Filtering
> > - *Hybrid filtering*: combine user-based content and content-based filtering