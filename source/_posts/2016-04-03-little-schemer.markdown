---
layout: post
title: "Little Schemer by Friedman and Felleisen"
date: 2016-04-03 12:51:55 -0800
comments: true
categories: [hobby, technical, reading, little schemer, daniel friedman, matthias felleisen]
---

With the exception of a quarter or two, University exclusively taught in the Object Oriented Procedural Paradigm. And while that will always feel like home... I don't spend that much time at home. It's nice to get out of your comfort zone, and go explore and learn new things. So I decided to pick up Little Schemer and gain some insight into Recursion and the Functional Programming paradigm.

While learning JavaScript I watched Douglas Crockford's lecture on JavaScript, [Act III: Function the Ultimate](https://goo.gl/hsLTwc). In this talk he recommended Little Schemer, promising that it would "Change the way you think, and there aren't a lot of books that will do that". It wasn't the first time that I had heard of the book, but this gave me to push to go out and pick it up.

I can happily say that it did not disappoint. I've always been fascinated by graphs and how easily that can model real world problems. And this book has pushed me towards some key insights there... which will probably get a full blog post in the future. But to put in a words I never thought I'd say: I now find it easier to think in recursion - since I know that if I can cover all the possible cases I'll eventually reach the solution.

Here are some of my favorite quotes and ideas from Little Schemer:

<!-- more -->

Note that Little Schemer isn't formatted like a normal book, it's based on lecture slides and works in a Q&A format. You can see a short excerpt below. It also assumes zero knowledge of Scheme so it starts with the basic building blocks of the language and builds up from there. It builds up very quickly and gets to some really cool stuff towards the end: Collectors, Applicative-Order Y-Combinator, Interpreter.

{% img /images/little_schemer_post/little_schemer_sample.png 'little_schemer_sample.png' %}

pg 23
>"What is the next question? else."

>"Why is else the next question? Because we do not need to ask any more questions."

>"Why do we not need to ask any more questions? Because a list can be empty, can have an atom in the first position, or can have a list in the first position"

>"Is else really a question? Yes, else is a question whose value is always true."

Fourth Commandment
>"Always change at least one argument while recurring. It must be changed to be closer to termination. The changing argument must be tested in the terminating condition: when using cdr, test termination with null?"

pg 83
> Because all *-functions work on lists that are either:
>
> > * empty
> > * an atom consed onto a list, or
> > * a list consed onto a list

Recursive way of looking at short-circuiting, pg 88
> Question: Do you remember what (or ...) does?

> Answer: (or ...) asks questions one at a time until it finds one that is true. Then (or...) stops, making its value true. If it cannot find a true argument, the value of (or ...) is false. And the opposite for (and ...)

Sixth Commandment
> "But then the  says: "Simplify only after the function is correct", so I shouldn't have skipped to the next iteration, and should have done the first version first because its easier to verify"

pg 98
> Why is (n + 3) a good representation?

> Because:
> > 1. (n + 3) is an S-expression. It can therefore serve as an argument for a function.
> > 2. It structurally resembles n + 3

Eight Commandment
> Use help functions to abstract from representations

pg 107
> "Numbers are representations? Yes. For example 4 stands for the concept four. We chose that symbol because we are accustomed to Arabic representations."

pg 127
> What kind of values can functions return? Lists and atoms (and functions)

> Note: Lambdas (currying) were discovered by Moses Schonfinkel and Haskell B Curry

pg 150
> Can you guess what sorn stands for? Symbol or Number

> Unnatural Recursion, does not recur on a part of lat (but on a result of a passed around function)

I didn't collect a lot of quotes from the last 3 chapters (collectors, Y-Comb, interpreter), but here are some of my notes:
> Really very mind expanding, chapter 9 and 10 are brutal. I thought 8 was hard with collectors but I got that in 2 reads. 9 I've already read twice and it still blows my mind.

> Using tables for stack frames and language (identifiers to primitives/values)

> Stack overflow on Applicative-Order Y-Combinator: Long story short, it allows you to implement recursion in a language that doesn't necessarily support it natively.

Y-combinator Proof steps in my words
> Length loses define, redefine length over and over with eternity as end point (use eternity because you lost length)

> Remove repetitions with create mk-length that creates length-like function

> Don't need eternity because you never reach it

> Pass mk-length to itself so it never runs out, but isn't infinite because of base case

> Make mk-length mk-length into a lambda that returns a function, so you can abstract it out and separate it from length

Learning more, recommends: 
> Polya, George. How to Solve it