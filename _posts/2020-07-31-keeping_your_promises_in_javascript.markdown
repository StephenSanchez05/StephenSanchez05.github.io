---
layout: post
title:      "Keeping your Promises in Javascript"
date:       2020-07-31 16:11:43 +0000
permalink:  keeping_your_promises_in_javascript
---


A promise in Javascript is one of those neat objects that act in a way the way you would expect it to.  Just like making a promise to your friend, a Javascript promise is an object that may be produced in the future.  The thing to remember though is that this is a promise, not a guarantee.  This means that there is a possibility that the promise is not kept, or rejected.  Lets break it down.

There are three states of the promise object:

- Fulfilled 
- Rejected
- Pending

All promises start in the pending state.  This is to say that there will be a value here in the future, but we won't get it until you call onto the Promise.  If the promise is fulfilled/resolved then you then define a .then() method which will execute on a successful promise.  The .then() method can be chained.  An example of this would be:

const myPromise =
  (new Promise(myExecutorFunc))
  .then(handleFulfilledA)
  .then(handleFulfilledB)
  .then(handleFulfilledC)
  .catch(handleRejectedAny);
	
In plain speak the const above is saying wait until the promise is executed, once thats executed perform (handleFulfilledA), once thats done perform (handleFulfilledB), etc.  At the bottom you'll see a .catch() method.  This is to handle the third state of a promise object, Rejected.
	
The Rejected, or reject(), state is essentially a broken promise.  Whatever action you wanted the promise to execute was not possible.  Instead of letting the code just fall to pieces, .catch() will catch the broken pieces and perform its method.  Most of the time an error object is passed to display what went wrong with the promise.  This is optional but it certainly a good practice to include .catch() methods in all your promises.
