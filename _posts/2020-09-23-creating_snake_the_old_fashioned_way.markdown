---
layout: post
title:      "Creating Snake The Old Fashioned Way"
date:       2020-09-23 14:17:09 +0000
permalink:  creating_snake_the_old_fashioned_way
---

### The Dream

A few weeks ago, I completed the Redux/React portion of the Flatiron curriculum. It was here. The final project, and scarier even, the *final assessment*. I was considering, once again, making some sort of to-do or social media clone application to show off my stuff. Looking back now, the thought had always been there. But never had I felt the confidence needed to follow through on my fantasy. *To create a game.* I piddled around the ground with my feet, nervously considering the mountain of work and logic of which I knew was needed for such an endeavor. For reasons beyond our understanding regarding memory recall, my mind flashed back to a time in my childhood garage. I was sitting on a stool, click frantically on the buttons of my mom's Nokia 3310, playing yet another round of Snake. 

### npx create-react-app liquid_snake

There, I did it. No backing out now. I had created the project, which occupied physical space on my solid state drive. It was *real* now. Most everything, dismissing the general process of game development, was for me entirely a black box. I knew I needed a snake. Okay, that's good, we'll need some food as well. A game board? What about distance? I'd have to define a standard unit of distance the snake will travel in a certain standard unit of time. While I felt overwhelmed at the thought of this work, it was paired with exhilaration. Alright, I know. It's 2D snake. But still, all of these factors still had to be implemented, as rudimentary as they would be.

### Let's start with the not-so-fun part

Unfortunate as it may be, we are all constrained by borders. And I mean this not at all in the political sense. I cannot travel to Alpha Centauri for a myriad of physical and biological reasons. But really, these are just borders. So just as I can, at most, fly to a different country, my snake could only slither about within the boundaries of a box. I chose to create this with CSS. The box itself would be a regular old `div`, with `position: fixed` relative to the master root `div`. Now, when you nest an element with `position: absolute` within a `position: fixed` element, the absolute element's dimensions are relative to the element that is fixed. This would allow me to situate the snake within the box, and theoretically keep track of its location. The same would go for any other elements that I would need to track, such as the snake's food.

### 'Moving' on to the snake

I could not imagine a more trecherous disposition than being trapped in a box, always staring at a juicy morsel of food, and not being able to move to it and chow down. So clearly, I would not subject my snake to such a scenario. But before thinking about the snake's movement, I would need to think about how to represent the snake in the first place. I chose to do this in a similar fashion to the box, with CSS. The snake itself would be represented by a series of coordinates organized in an array. These coordinates, passed into the snake component via its container's props, would then be used to set the `top` and `left` style values of the snake component. So, by passing in an AoA, containing 3 sets of coordinates, the snake component would render 3 `divs`, with the class name `snake-piece`, and its left and top style values set by the first and last set of coordinates passed to it, respectively. 

Moving the snake was a bit more complex than the simple rendering of it. Amuse me, while I get into some basic classical mechanics. The snake needs velocity. Simply put, velocity is movement with direction, over time. Let’s start with the direction part.

### The snake's direction

To handle direction, I wanted to use the arrow keys, as I wanted to allow only movement perpendicular to the box's borders. I created a event listener on the window, which listened for the `onKeyDown` event. This listener function would fire each time a key was pressed. If the pressed key was an arrow key, the function would determine which arrow key was pressed, and set a value named `direction` in the redux store, equal to the value of the key. In other words, if the right arrow key was pressed, the value of `direction` in the store was set to 'RIGHT'. One additional feature I needed was that the snake could not turn around and munch on its own body. To do this, I first check the orientation of the snake. If the key pressed was the opposite direction, I would not set the new direction from the pressed key.

### Direction, check. On to time

For the second part of our velocity, well need some sort of way to implement 'time'. This is a little wonky to wrap the head around, but it is necessary to consider when designing any game. In game development, a single unit of time is usually called a 'tick'. In JavaScript, it seemed best to use the `setInterval` method, which calls any provided function as a callback every time for a given timeframe. The timeframe is given in milliseconds. So by using this, we would be able to call the `moveSnake` method, which would be responsible for re-rendering the snake given its direction.

### Finally, movement

Alas, we have reached the moment of truth. Where our simple snake comes to life and gain motor control right before our very eyes. Well, that's a bit of an overstatement. Our movement is more of an illusory magic trick, rather than traditional movement. Basically, I wanted to, at every interval update, to remove a piece(the tail) and add a piece(a new head). The head is the part that matters, as removing the tail is easy as `shift`ing the array of snake pieces in the store. Depending on the orientation of the snake, defined two paragraphs ago, we would add a new head accordingly by creating a new set of coordinates, and `push`ing that new set onto the snake pieces AoA. Once the new AoA was set, we would dispatch these new coordinates to the store, the props would change for the snake and cause a re-render. Once again, this would be happening at a given interval. All set! Our snake moves and shakes with the best of em'.

### To wrap things up

There were several other features implemented in this project, such as a live score tracker, an ability to submit your name as 3 letters (old school style). And view a list of global scores sorted by hi-score. Oh, and also a random cat picture generator, because, you know, it's the internet. However, I'll keep things short enough in this one to just give you a sense of how I was able to overcome my fear of game development, and create something of which I am truly proud and excited.


