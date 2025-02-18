> [!question] What is MapReduce Useful For?
> - Web systems require computations that are too large for one computer to do
> - & Examples:
> 	- Building a search index for the entire Internet
> 	- Analyzing log files
> 	- Precomputing recommendations for followers or videos
> - ^ In general, MapReduce is a tool for:
> 	- **Big** tasks
> 	-  **Batch** tasks (as opposed to interactive)

> [!info] MapReduce Insight
> - Splitting work between multiple computers is hard 
> 	- ? How do they communicate?
> 	- ? What happens if one of them crashes?

> [!example] Simple Example
> - ^ Goal: find word count
> - <u>**Input**</u>
> 	- hello
> 	- world
> 	- hello
> - <u>**Output**</u>
> 	- hello: 2
> 	- world: 1
> 
> > [!i]- Map
> > - Transform one line of input to o+ (key, value) pairs
> > 	- Separate key and value with a tab
> > 
> > ![[Pasted image 20241017004920.png]]
> 
> > [!ii]- Group
> > - Put all the entries with same key together
> > 
> > ![[Pasted image 20241017005032.png]]
> 
> > [!iii]- Reduce
> > - Combine each group into an output value
> > 
> > ![[Pasted image 20241017005343.png]]
> 
> > [!question] Why This is a Good Structure?
> > - Map and Reduce don't have dependencies between rows/groups
> > - Group stage is possible to distribute too
> > 
> > ![[Pasted image 20241017021836.png]]

^715559

> [!info] Designing MapReduce Algorithms
> 
> > [!goal]- Goal
> > - Algorithms need to be rewritten from scratch to fit in MapReduce
> > - A MapReduce program has two functions:
> > 	- `map(input)`
> > 		- returns a `{key, value}` pair
> > 	- `reduce(group of {key,value} pairs)`
> > 		- returns output
> 
> > [!info]- Problem
> > - Determine average rating of books
> > 
> > ![[Pasted image 20241017022342.png]]
> 
> > [!info]- My Method
> > - I work backwards
> > 	- output → reduce → map
> > - Reason: 
> > 	- Reduce always combines rows
> > 	- Easier to think about what will be combined, which dictates what map needs to do
> 
> > [!example]- Output → Reduce
> > ![[Pasted image 20241017022536.png]]
> 
> > [!example]- Reduce → Map
> > ![[Pasted image 20241017022609.png]]
> 
> > [!info]- Pseudocode
> > <br>
> > 
> > ```{psuedocode}
> > # Input: "John Cookbook 4"# Output: "Cookbook 4" 
> >  function map(row):
> > 	name, book, rating = split(row)
> > 	return "{book} {rating}"
> > 
> ># Input: ["Cookbook 4", "Cookbook 2"]
> > # Output: "Cookbook 3"
> > function reduce(rows):=
> > 	vals = []
> > 	for row in rows:
> > 		name, rating = split(row)
> > 		vals.append(rating)
> > 	return "{name} {average(vals)}"
> > ```
> 
> > [!Output]-
> >  ![[Pasted image 20241017023256.png]]
> 
> > [!example]- Short Design Example
> > ![[11 - MapReduce - Annotated (dragged).pdf]]

> [!info] Parallel MapReduce
> 
> > [!info]- MapReduce Frameworks
> > - We supply `map()` and `reduce()`
> > - Framework
> > 	- Moves data to right place
> > 	- Runs `map()` and `reduce()` on the right input
> > 	- Handles the grouping
> > 
> > ![[Pasted image 20241017023605.png]]
> 
> > [!info]- Distributing Map and Reduce
> > ![[Pasted image 20241017023646.png]]
> 
> > [!info] How Grouping Works
> > - ^ Rule: same reducer needs everything with the same key
> > 
> > ![[Pasted image 20241017023731.png]]
> > 
> > - Simple to do with 1 centralized group stage: merge sort
> 
> > [!important]- Distributed Grouping (P4)
> > ![[Pasted image 20241017023829.png]]

> [!info] MapReduce Fault Tolerance
> 
> > [!info] MapReduce as Distributed System
> > - Our Python system so far runs as a single program 
> > - ? How to split into multiple?
> > 
> > ![[Pasted image 20241017023942.png]]
> 
> > [!important] P4 MapReduce Jobs
> > - Manager is coordinator
> > - Workers execute shell commands
> > 	- Can be Bash scripts, Python programs
> > 	- Data is shared using the file system
> > - Map and Reduce can be done on same pool of workers
> > 	- Both are just shell commands operating on files
> 
> > [!note] Fault Tolerance
> > - ? How do we know if machine goes down?
> > - Workers send periodic heartbeat messages to manager
> > - Manager keeps track of which workers are up
> >   
> > > [!example]- Example
> > > ![[Pasted image 20241017025007.png]]
> > 
> > - ? What happens when a machine dies?
> > - Without MapReduce
> > 	- Program (or query) is restarted
> > 	- Not so hot if your job is in hour 23
> > - With MapReduce
> > 	- If map worker dies
> > 		- Just restart that task on a different box
> > 		- You lose the map work, but no big deal
> > 	- If reduce worker dies
> > 		- Restart the reducer, using output from source mappers