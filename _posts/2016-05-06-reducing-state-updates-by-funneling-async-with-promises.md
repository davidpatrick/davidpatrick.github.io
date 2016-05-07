---
layout: post
title:  "React State Management & Promise.all Async Funneling"
date:   2016-05-06 12:00:00
categories: reactjs javascript promises
image: 'http://i.imgur.com/wT0L1yb.png'
---

[flashingScreen]: http://i.imgur.com/EkO9Z4o.gif "Flashing Screen During Loading"
[loadingScreen]: http://i.imgur.com/VpyU55n.gif "Optimized Loading Screen"
[beforePerformance]: http://i.imgur.com/5ZnS8Oo.png "Performance Before Changes"
[afterPerformance]: http://i.imgur.com/aRaYzvI.png "Performance After Changes"

### Multiple Async Calls Updating State

In our app, we have multiple asynchronous calls firing off when it first loads up.  Each call is updating the state with the information it retrieves, in turn components are receiving new props and triggering their setup process more than once.  The first problem we have is the main container component rendering children before it is done gathering the data the children needs.  

![Unintended Loading User Experience][flashingScreen]

To fix this we need to manage when the children are rendered.

{% highlight javascript %}
if ( this.state.setupComplete )
  return <div className='container'>
    { React.cloneElement(this.props.children}) }
  </div>
else
  return <div className='loader'>
    Loading...
  </div>
{% endhighlight %}

 Don't render the children until all of the async calls have finished. But how do we know when all of the calls are finished if they all finish at different times?  We could try and manage this by contionously updating our state each time an async call finishes checking to see if it should also set state.setupComplete, but I want to avoid component life cycles and only update state when the setup process is completed, not when part of it is completed.  For this scenario, I think Promises are a perfect use case, and the handy Promise.all can resolve all of our calls, and it makes handling failures a breeze too.  
 
 We start by creating a Promise for each Async call and passing the Promise's resolve/reject into our async calls.  We then resolve all of the promises at the same time using Promise.all.  That returns an array of promises, which we will loop through and assign the data to our newState object.  We can use setTimeout and have a 2sec delay to avoid our loading screen from flashing in and out.
 
{% highlight javascript %}
// Create a Promise for Each Async Call
// For brevity I will include only 2 calls
const userDataPromise = new Promise( (resolve, reject) => { 
  $.get('/user')
    .done( data => { resolve(data) })
    .fail( error => { reject(error) })
})
const layoutDataPromise = new Promise( (resolve, reject) => { 
  $.get('/layout')
    .done( data => { resolve(data) })
    .fail( error => { reject(error) })
})

// Resolve all Promises after a 2s delay
setTimeout( () => {
  Promise.all([
    userDataPromise,
    layoutDataPromise
  ]).then( promises => {
      const newState = { setupComplete: true }

    // Assign promise data to our newState 
      for (let promise of promises) {
        Object.assign(newState, promise)
      }

      this.setState(newState)
    }).catch( failure => {
      // Easily Handle Failures
      const newState = { setupFailed: true }
      this.setState(newState)
    })
}, 2000)
{% endhighlight %}

Now let's take a look at the result of Promise.all managing the Loading State.

![YES! Success.][loadingScreen]

That is the user experience that we were going for!  Okay so we have avoided the flashing screen, and have created an extensible setup process, but what kind of performance gains did we get with these changes?  

### React Performance Tools
To get started measuring Reactjs performance we will use the [Performance Tools](https://facebook.github.io/react/docs/perf.html) supplied to us by the Reactjs Team.  To install them run `npm install react-addons-perf -D` and before your ReactDOM.render put the following

{% highlight javascript %}
window.perf = require('react-addons-perf') //Mount the tools to the Window so we can run in console
window.perf.start()
{% endhighlight %}

Now when you run your page and your components have finished rendering, open up the web console and run the following

{% highlight javascript %}
perf.stop()
perf.printInclusive() // Prints the overall time taken.
perf.printExclusive() // Time excluding mounting
perf.printWasted()    // Time spent on components that didn't render anything
{% endhighlight %}

Here are the results BEFORE we did any refactoring
![Whoa! Look at all of that wasted time!][beforePerformance]

Here are the results AFTER we implented Promise.all and Loading State
![Where did the wasted time go!][afterPerformance]

The biggest gains we can see is in the difference in the amount of [instances](https://github.com/facebook/react/issues/4911) and the amount of time spent on every component. One other thing you will notice that is missing in the second screenshot is the [wasted measurements](https://facebook.github.io/react/docs/perf.html#perf.printwastedmeasurements).  That is because we are no longer wasting anytime in the components!  Thanks to no longer rendering our components until the container is ready.  We have created a highly performant and easily mangeable loading state using Promise.all and not rendering our children until they are ready.