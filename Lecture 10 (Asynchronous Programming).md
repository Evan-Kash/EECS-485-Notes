> [!info] More About Promises
> 
> > [!info] Promises
> > - Promise represents value that is not available right away 
> > - Creating a Promise sets up a pipeline for what happen when the value is available
> > - & Real-life example
> > 	- Your friend promises to give you $1 in the future
> > 	- You can start to plan what to do with it
> > 	- But you can't actually do it yet
> 
> > [!info] Promise Picture - `fetch`
> > <br>
> > 
> >```js
> > fetch("/api/v1/u/jklooste")
> > 	.then(handleResponse)
> > 	.then(handleData);
> >```
> > 
> > ![[Pasted image 20241001033207.png]]
> 
> > [!info] Promises (cont.)
> > 
> >  - A promise is in one of these states:
> > 	 - ***pending***: initial state, neither fulfilled nor rejected
> > 	 - ***fulfilled***: meaning that the operation completed successfully
> > 	 - ***rejected***: meaning that the operation failed
> > 
> > <br>
> > 
> >  - If the executor function success, the the method provided by `{js}.then()` runs
> >  - If the executor function fails, then the method provided by the `{js}.catch()` runs
> 
> > [!info] Creating Promises
> > <br>
> > 
> > ```js
> > let p = new Promise((resolve, reject) => {
> > 	//do some asynchronous work
> > 	//in "pending state"
> > 
> > 	//call reject if there's an error
> > 	if(error happens){
> > 		//enter "rejected state"
> > 		reject("Error");
> > 	}
> > 
> > 	/call resolve when promise complete
> > 	//enter "fulfilled state"
> > 	resolve("All finished");
> > });
> > ```
> > 