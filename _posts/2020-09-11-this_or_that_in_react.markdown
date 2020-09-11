---
layout: post
title:      "This or That in React"
date:       2020-09-11 19:41:22 +0000
permalink:  this_or_that_in_react
---

Here is an app with a simple idea.  I want the user to type in a word into an input field and when they hit submit it should return the first gif that returns matching that word from a website.  Here are my states.  The web address attached to gifs is one that returns a gif of "Error".  This is to let me know that the gif state was not replaced properly with the fetch request:

    state = {
        query: "",
        blog_id: "",
        gifs: ["https://media.giphy.com/media/TqiwHbFBaZ4ti/giphy.gif"]
    }
		
		Here is my fetch request.  You'll see in the middle of the website address I am including this.state.query.  The query comes from the form that the user will submit.  Essentially the search word.  Then the fetch request sets the gif state to the returned url that conatins the new gif:
		
		   fetchGifs = () => {
        
        fetch(`https://api.giphy.com/v1/gifs/search?q=${this.state.query}&api_key=dc6zaTOxFJmzC&rating=g&limit=1`)
          .then(res => res.json())
          .then(({data}) => {
            this.setState({ gifs: data.map( gif => ( gif.images.original.url ) ) })
            console.log(this.state);
          })
      }
			
			
			And here is my handleSubmit funciton.  As you can see once the user hits submit the handleSubmit function will call on the fetchGifs function, it will wait 300 ms (to allow the fetch request to occur) and then upload the gif state to the database using a function called this.props.postGif from my actions folder:
			
handleSubmit = event => {
            event.preventDefault();
            this.fetchGifs();
            console.log(this.state)
            setTimeout(() => {
            this.props.postGif({url: this.state.gifs[0]})
            }, 300);
            this.setState({
                query: '',
            });
        }
				
	Seems simple enough right?  But the handleSubmit function isn't working!  All I get are the error gifs which let me know that the fetch function did not get the proper information.  After some troubleshooting and many many console.logs later I found the issue was actually with the handleSubmit function.

handleSubmit did not recognize this.fetchGifs().  How could this be?  The function is literally one line above it!  Its in the same component.  The trick was what "this." refers to.

this. does not actually recall to the top layer of the component.  It depends on what it is being used on.  In this case, using this.fetchGifs tells handleSubmit to look for a function within itself, not within its component, and call on it.  I can handle this two ways.

1.  build the fetchGifs function inside the handlesubmit function.  That works, but can be ugly and make the handlesubmit button function long and complex.

2. In the constructor I tell the class that I don't care where I use this.fetchGifs, I am referring to the class level of functions.

I went with option two which looks like this:

    constructor() {
        super();
        this.fetchGifs = this.fetchGifs.bind(this);
    }
		
		And now you can react to any post on my app with the perfect gif!
