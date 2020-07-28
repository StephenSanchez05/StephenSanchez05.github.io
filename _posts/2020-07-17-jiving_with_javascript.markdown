---
layout: post
title:      "Jiving with Javascript"
date:       2020-07-17 13:04:44 -0400
permalink:  jiving_with_javascript
---


Lets make a game!  The game will show you a random assortment of words.  Your job is to guess the right word.  To pull the words that are going to be shown is simple enough.  Create an array of words and create a function that will iterate over the array randomly and push a few of those into a brand new array.

function createWordLibrary(data) {
        data = data.replace(/["[\],]+/g, "");
        let diff = data.split(' ');
        let arr = [];
        for(var i = 0; i < 15; i++) {
            randNumber = Math.floor(Math.random() * 10);
            let y = diff.splice(randNumber, 1);
            arr.push(y);
        }
        answer = String(arr[randNumber]);
        arr.forEach(x => {
            addHackWords();
            addWordsToDom(x);
            addHackWords();
        })
        console.log(answer);
}

Then randomness comes from Math.floor(Math.random() * 10).  You'll notice I have the function run this over each iteration.  This is to increase the randomness of the words that are pulled.  If you set randNumber before the iteration then the words will always be shown in the same order, just a random starting point.

answer = String(arr[randNumber]) is how we choose the correct answer.  We tell the variable answer to select a word from the new array we created at a random index.  This ensures that the answer will be shown to the player of the game.

Now how do we check if the word the player has selected matches the answer?  Not only that, if they guess wrong we want to let the player know how many letters are in the right place. (i.e. they select "bring" and the correct word is "sting" then 3/5 letters are correct).

This can be done with another iteration.  We want to split the word selected and the correct answer so that each letter is pushed into an array.  Then one by one we will compare the arrays at the same indexes.  If they are === then we += 1 to the "how many letters are correct" total.  

function wrongAnswer(x) {
    correctLetters = 0;
    scoreAttempts++;
    let wrongAnswer = x.split('');
    let rightAnswer = answer.split('');
    for(var i = 0; i < wrongAnswer.length; i++) {
        if ( wrongAnswer[i] === rightAnswer[i]) {
            correctLetters += 1;
        }
    }
		
		Viola!  Iteration is extremely powerful and can be used to make fun comparing games like so.
