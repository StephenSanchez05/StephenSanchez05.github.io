---
layout: post
title:      "Programming at the speed of code"
date:       2020-09-11 20:13:47 +0000
permalink:  programming_at_the_speed_of_code
---


Computers are fast.  Like really really fast.  This is normally a good thing, but sometimes it can create interesting problems.  I want to create an app that will return a gif based on the users search term.  A simple fetch request that will set the state of the class' url to the appropriate one to reflect the search.  Here is a look at the code:

    constructor() {
        super();
        this.fetchGifs = this.fetchGifs.bind(this);
    }
    state = {
        query: "",
        blog_id: "",
        gifs: []
    }

    handleChange = event => {
        this.setState({
            query: event.target.value
        });
    }

    fetchGifs = () => {
        
        fetch(`https://api.giphy.com/v1/gifs/search?q=${this.state.query}&api_key=dc6zaTOxFJmzC&rating=g&limit=1`)
          .then(res => res.json())
          .then(({data}) => {
            this.setState({ gifs: data.map( gif => ( gif.images.original.url ) ) })
            console.log(this.state);
          })
      }


        handleSubmit = event => {
            event.preventDefault();
            this.fetchGifs();
            this.props.postGif({url: this.state.gifs[0], blog_id: this.props.blogid})
            this.setState({
                query: '',
                blog_id: ''
            });
        }
				
				
				
				It all looks correct on face value.  However the gif state was not being updated.  How could this be?
				
				After a lot of console logging I found that the fetchGif function was not only correctly searching the query, it was also setting the state appropriately.  handleSubmit was calling on the fetchGif function correctly and was pulling the correct state.  However here's the weird thing, the first time it pulled the gif state, it was blank.  However if I searched the same word again it would return correctly.
				
				
			It came down to timing.  handleSubmit was not asynchrous.  It would call fetchGifs(), but it wouldn't wait for the function to finish its job before it pulled the gif state.  That why we would use useEffect.  useEffect is essentially componentdidmount, but after the component actually mounted.  Attaching it to the fetchGifs function solved the problem!
