---
layout: post
title:      "Using CSS to Make Your Website Standout"
date:       2020-11-26 19:14:11 -0500
permalink:  using_css_to_make_your_website_standout
---

It's amazing how much design is an important part of creating a website.  Simply stylizing your code can make or break your website.  An incredibly effective way to do this is to add animations with CSS.  Animation is simply making your text move around the screen.  This can be done using @keyframes.  Here is what something like that would look like:

@keyframes moveit {
from {top: 0px;}
to { top: 200px;}
}

Let's break down what is happening here.  First we are calling on @keyframes.  This tells CSS we are going to be doing animation.  Then we name the animation, which in this case is called "moveit", so we can call on it later.  Next we determine the starting point and the ending point in the brackets.  Now how do we call it?

In the CSS declaration you must declare what animation you would like played, and how long you would like to play it for.  This is how it would look:

div {
animation: moveit 5s;
}

This tells the div that we want animation, we want specifically the moveit animation, and we want it to go from the start to end keyframes over 5 seconds.  Its as simple as that!  Now when the website loads in, anything with the div designation will move downward 200 pixels over 5 seconds.
