> [!abstract]- Review: JS Functions and `setTimeout()`
> ![[Pasted image 20240930045741.png]]
> ![[Pasted image 20240930045817.png]]

> [!info] Accessing REST APIs in JavaScript
> 
> > [!info]- Client-side applications picture
> > ![[Pasted image 20240930045907.png]]
> 
> > [!info]- JavaScript `fetch` API
> > ![[Pasted image 20240930045947.png]]
> > 
> > > [!info]- Timeline
> > > ![[Pasted image 20240930050132.png]]
> > 
> > > [!question]- What will print?
> > > ![[Pasted image 20240930050200.png]]

> [!info] JavaScript Promises
> 
> > [!info] `fetch()` returns a Promise
> > - Network requests take a long time, unpredictable
> > - We want to do useful work while we wait
> > - $ Solution:
> > 	- `fetch()` returns a Promise
> > 	- ^ Promises build a plan that executes in the future
> > 	- The currently running function keeps executing after the promise is set up
> 
> > [!warning]- `.then()` vs. Linear Code
> > ![[Pasted image 20240930050504.png]]
> 
> > [!info] Promise Diagram
> > ![[Pasted image 20240930050604.png]]

> [!info] React and Fetch API
> 
> > [!info]- Side effects and React Components
> > - React functional components (what we use in 485) need to be "pure"
> > 	- Pure function: output only depends on inputs to the function
> > 	- React: same props lead to same return value
> >
> > ![[Pasted image 20240930052156.png]]
> 
> > [!info]- Network Requests are Side Effects
> > 
> > ![[Pasted image 20240930054042.png]]
> > 
> > - **Rule**: Anything that synchronizes with something outside React must be in `useEffect()`
> > - ? **Why?** Lets React know there's something outside its control, affects caching
> 
> > [!info]- React `useEffect()` hook
> > ![[Pasted image 20240930054228.png]]
> 
> > [!tip] Race Condition with `fetch` in `useEffect`
> > - It's possible for responses to arrive in a different order than requests were made
> > - In the P3 React tutorial, there's a ignoreStaleRequest flag that helps resolve this race condition

> [!tip] Bonus: Closures
> ![[Pasted image 20240930054424.png]]