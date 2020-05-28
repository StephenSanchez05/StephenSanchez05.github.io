---
layout: post
title:      "Finding Serenity in Rails"
date:       2020-05-15 14:50:42 -0400
permalink:  finding_serenity_in_rails
---

I play DnD.  I know, a programmer who is a nerd isn't exactly shocking.  There is a common problem I have when I play though.  I have to use pen and paper to keep track of the long list of spells that are available to my characters.  This can change every time my character rests so it makes for a messy piece of paper.  This is why I chose to create a website that will help keep my characters and what spells they have organized!  

Each user will sign up and have many characters and have many spells.  The characters can also have many spells, and the spells can belong to many characters.  If we were to accomplish this via has_many :spells then we would have to create a copy of each spell everytime I had a new character that owned the spell.  This is too messy.  So I created a class called Heros.  Now every Character can have a Spell through Heros, and every Spell can have many Characters through Heros.  

You'll noticed its called Heros and not Heroes.  Rails didn't seem to pick up on the plurality of Heroes so I pretend its a sandwich for simplicity sake.  This problem comes up again where I can't label a column "Class" even though it is a common word in DnD.  I had to name the column "Warrior".  However I found a neat trick where I can convert Warrior to display Class to the user.

If you go into config - locales - en.yml you can actually change the attributes of your without affecting how SQL views it.  Here is what I had to do to make "Warrior" appear as "Class" whenever I called on it.

  activerecord:
    models:
      character:
    attributes:
      character:
        warrior: "Class"
				
This means if there ever is a validation error (let's say uniqueness), when I display the errors to the user it will state that "Class has to be unique", not "Warrior has to be unique".  
