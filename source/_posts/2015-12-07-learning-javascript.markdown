---
layout: post
title: "Learning Javascript"
date: 2015-12-07 15:22:29 -0800
comments: true
categories: [technical, project, javascript, videogame, phaser, douglas crockford]
---

## Under Construction

### Table of Contents

* [Introduction](#introduction)
* [MDN Reintroduction](#mdnreintroduction)
* [Crockford on JavaScript](#crockfordonjavascript)
* [MDN Game Development Workflows](#mdngamedevelopment)
* [Building a Game](#buildingagame)

<a name="introduction"></a>
### Introduction

I've always been interested in learning Javascript, but have been too overwhelmed by the abundance of resources out there. I finally took the time to do some thorough looking around with lead me to this Stack Overflow [link](http://goo.gl/iPMGV) on resources for learning Javascript. This lead me to the MDN Javascript Reintroduction and Crockfords Lectures.

<!-- more -->

<a name="mdnreintroduction"></a>
### MDN Reintroduction

* [Mozilla Developer Network (MDN) Reintroduction to JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
* [Beej Guide: JavaScript Prototypes and Inheritance](http://beej.us/blog/data/javascript-prototypes-inheritance/)

Learning javascript made me realize how little I knew about the languages I was comfortable with. Programming in my comfort languages (Java/C++) had become almost like being fluent in English, I forgot a many of the little details and rules here and there.

It was a good dose of reality to get me out of my comfort zone and push me to learn the deeper details of languages.

<a name="crockfordonjavascript"></a>
### Crockford on JavaScript

* [Volume 1: The Early Years](https://www.youtube.com/watch?v=JxAXlJEmNMg)
* [Chapter 2: And Then There Was JavaScript](https://www.youtube.com/watch?v=RO1Wnu-xKoY)
* [Act III: Function the Ultimate](https://www.youtube.com/watch?v=ya4UHuXNygM)
  * This talk also convinced me to pick up Little Schemer, promising that it would "change the way you think, and there aren't a lot of books that will do that"
* [Episode IV: The Matamorphasis of Ajax](https://www.youtube.com/watch?v=Fv9qT9joc0M)
* [Part 5: The End of All Things](https://www.youtube.com/watch?v=47Ceot8yqeI)
* [Scene 6: Loopage](https://www.youtube.com/watch?v=QgwSUtYSUqA)
* [Level 7: ECMAScript 5: The new Parts](https://www.youtube.com/watch?v=UTEqr0IlFKY)
* [Section 8: Programming Style & Your Brain](https://www.youtube.com/watch?v=taaEzHI9xyY)

The first two talks are a history lesson, very informative. A lot of the languages and software architects have come up in random reading around the internet, such as some of my favorite (research) papers:

* Ken Thompson's Turing Award Lecture, "Reflections on Trusting Trust"
* Lamport's "The Future of Computing: Logic or Biology"
* CAR Hoare, "The Emperor's Old Clothes"
* Fred Brooks (1986), "No Silver Bullet"
* Parnas, David L. “Designing Software for Ease of Extension and Contraction.”

I really enjoyed the foundations of JavaScript. How Netscape had Brendan Eich create a web language. He wanted to base it on Scheme, but Netscape put its foot down and said they wanted it to be more approachable. So Eich used the syntax of JavaScript, the first-class functions of Scheme, and the Prototype Chain of Self to make one of the most popular languages of all time. And in 4 weeks! Although this short time frame is responsible for a lot of JavaScript's blunders which are slowly being repaired (ES6 Strict was a big jump).

Some benefits of Prototyped OOP:

* Trivial to make new "classes", avoids lots of boilerplate
* More "functional" style
* Change behavior at runtime
* Easy multiple inheritance, don't need crazy and hard to maintain type hierarchy
* Property modifiers

Wouldn't be complete without cons list:

* Lose static typing
* Performance overhead, still have to check inheritance hierarchy and compiler can't help you out
* New is scary, can easily accidentally clobber global object

Now that I knew a lot of the theory behind Javascript, it was time to practice applying it. I decided to make a game.

<a name="mdngamedevelopment"></a>
### MDN Game Development Workflows

* [2D Breakout in pure JS](https://developer.mozilla.org/en-US/docs/Games/Workflows/2D_Breakout_game_pure_JavaScript)
  * [Try it!]({{ root_url }}/resources/games/breakout/)
* [2D Breakout game using Phaser](https://developer.mozilla.org/en-US/docs/Games/Workflows/2D_Breakout_game_Phaser)
  * [Try it!]({{ root_url }}/resources/games/breakoutPhaser/)
* [2D Maze game with Device Orientation using Phaser](https://developer.mozilla.org/en-US/docs/Games/Workflows/HTML5_Gamedev_Phaser_Device_Orientation)
  * [Try it!]({{ root_url }}/resources/games/phaserMaze/)

<a name="buildingagame"></a>
### Building a Game

You can try it out, it is still a work in progress though. It was really fun to not just program this, but design it, create the maps... to have complete control. I did have several issues developing it though, mostly with JavaScript.

* [My Game](https://github.com/nmlau/vim-maze)
  * [Try it!]({{ root_url }}/resources/games/vimMaze/)

List of issues and what I learned:

* Hosting issues: browser was caching objects so when I updated and went to test my changes... everything would be the same. Octopress had some issues with actually changing letter capitalization in the repo that prevented a few scripts from loading properly.
* Maps: used Tile Map Editor to generate json maps.
* Pass in method, not method call as callback. If you pass the method call then it will only get called once AND have the wrong context.
* Make sure to pass the context. 'this' isn't passed around implicitly like in java, context is generally one part of a long list of arguments.
* Using an unfamiliar framework in a new language was difficult. While Java does have varargs, the way Javascript parameters work was still weird, like how you could leave them out and wouldn't even get a warning. Even with the docs open, a lot of the high level functions had huge lists of parameters and I would often misread, misunderstand, or forget something.
* Modularizing. Awkward in Phaser, it doesn't provide a built in way to do it. This is because sites like to have games in a single minified js file. Being used to OOPs highly structured and separated classes this was kind of weird. But hey, this is what you learn new technologies and languages for.
* Debugging. The console has awesome debugger tools built in. Just throw the 'debugger' statement into your Javascript code. I make sure to use the '.js' library rather than 'min.js' so I can use the debugger to source code dive.
