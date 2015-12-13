---
layout: post
title: "Research Papers: System and Language Design"
date: 2015-12-10 13:46:43 -0800
comments: true
categories: 
published: false

---


[1] Pick CS papers to read, https://goo.gl/D2JkNn
-Ken Thompson's Turing Award Lecture: Reflections on Trusting Trust, https://goo.gl/orXksh
-Lamport's "The Future of Computing: Logic or Biology", https://goo.gl/f7Dgly
-C A R Hoare, The Emperor's Old Clothes, https://goo.gl/c4BZyg
-No Silver Bullet — Essence and Accidents of Software Engineering (Fred Brooks, 1986), https://goo.gl/4fK9RK

Amazon Dynamo, Google Mapreduce

Focuses on:
-Lamport's "The Future of Computing: Logic or Biology", https://goo.gl/f7Dgly
-C A R Hoare, The Emperor's Old Clothes, https://goo.gl/c4BZyg
-No Silver Bullet — Essence and Accidents of Software Engineering (Fred Brooks, 1986), https://goo.gl/4fK9RK


(reread)
[1] Read Lamport's "The Future of Computing: Logic or Biology", https://goo.gl/f7Dgly
-Biology is so complex that being right 80% is enough, but for things like logic and physical science you have to be abel to explain the other 20%
-We want programming to be like Logic, not to become like biology where that 20% is often misinterpreted in the classic "coincidence vs causality" which leads to things lik homeopathy and faith healing. However programs are getting more and more complex. And there are two approaches for dealing with this complexity:
1. Base on biological system, let them evolve. But take the human body, a marvel of biological engineering... it took nature millions of years, its still so far from perfect ("just good enough to survive"), and its slow to adapt (many species go extinct). It's a fundamentally wrong approach, since it means giving up on understanding how the systems actually work
2. Through logic. Proving correctness of small programs, using mathematical methods at earliest stage of system design
-At the same time, programming isn't like automobiles. It doesn't run so much as it's a mathematical object. You can never prove that an autombile will run, but you can for a program, though it's very difficult and unrealistic for large programs
-"Computers interact with users through metaphors. Metaphors are not based on logic, but they are not illogical.
Metaphor and logic are not opposites. They are complementary. A good program must use good metaphors, and it must behave logically. The metaphors must be applied consistently—and that means logically."
-Have to resist this shift towards incomprehensibly complex systems that a lot of incompetent architects are developing. Or else we'll end up with more biological systems than logical

(meta: underestimated how long this would take to read... Logic and Biology was pretty short)
[1] Read CAR Hoare, The Emperor's Old Clothes, https://goo.gl/c4BZyg
-A story of his career: Inventing Quicksort, ALGOL implementation, working on ALGOL team, failure of 503 MARK II operating system
-Key to Mark II failure was that he had programmers implementing things that he himself didn't understand. And very ambitious things at that
-Found that operating systems were much more difficult to program than languages... leading to his work on monitors and communicating processes
-Used assertions throughout the program, they worked as a checklist... if all the assertions were true then it would mean the program was correct. Similar to how if you check all modules work correctly you can see that the system works. And every module is a program whose correctness is shown by assertions
-When ALGOL working group didn't select his languages draft:
"I conclude that there are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies and the other way is to make it so complicated that there are no obvious deficiencies."
-"You include only those features which you know to be needed for every single application of the language and which you know to be appropriate for every single hardware configuration on which the language is imple- mented. Then extensions can be specially designed where necessary for particular hardware devices and for partic- ular applications. That is the great strength of PASCAL..."
-However, the successes of Pascal were not learned from and replicated as they should have been
-I'm disappointed that this guy didn't go on to create some awesome language... after going through all the "failed" languages he's been involved in
-Ahhahahah the story at the end is hilarious... 
-Discovered the concept of Program Correctness as mentioned in the last paper I read, Logic or Biology. It's awesome, Logic and Biology is clearly influenced by this... this paper talks about Physical science being able to comprehensively explain complex phenomena of nature (Biology). Furthermore, this paper makes me want to rewatch Crockfords History JS lecture and compare his opinion of ALGOLs development (1965ish, ALGOL 60 to 68). Or PL/I or ADA.

[3] Read No Silver Bullet (Fred Brooks, 1986), https://goo.gl/4fK9RK, pdf: http://goo.gl/tpDiRQ
-Things were so different in 1986... they're so excited about ADA, OOP, the next 30 years of moores law...
-Keywords are essence, the design. And accidental difficulties, the programming/implementation
-Parnas comes up a couple times, once involving AI. I definitely recognize this name... but a grep of knowledge doesn't find anything. Google search shows he was huge in developing modular design and information hiding. That's probably where I've heard of him. Yes! Know him for 'Decomposing Systems'
-"In short, automatic programming always has been a euphemism for programming with a higher-level language than was presently available to the programmer", this reflects my thoughts that frameworks are a step towards automatic programming. But I hadn't thought that the step before that was High level languages like Java generating loads of ARM code
-Program verification can only ensure a program meets its specification. The hardest part of building software is arriving at a complete and consistent specification, much of the essence of building a program is in fact the debugging of the specification
-Spot on prediction of giving computer-naive intellectual workers personal computers and good programs, then let them loose
-On Prototypes:
"A prototype software system is one that simulates the important interfaces and performs the main functions of the intnded system, while not being necessarily bound by the same hardware speed, size, or cost constraints. prototypes typically perform the mainline tasks of the applciation but make no attempt to handle the exceptions, responding coreectly to invalid inputs, abort cleanly, etc. The purpose of the prottype is to make real the conceptual structure specified, so that the client can test it for consistency and usability"
-His metaphor for creating software has gone from writing to building. But he says it's complexity has moved beyond that to growing. That we should imitate the human brain, an biological marvel that was grown by evolution. This is so funny because the last two papers I've read, Turing award by Tony Hoare, and Logic vs Biology both said the exact opposite: that biology was an 80% sure thing that gave up on understanding, and logic was the future
-Or maybe he's not saying it should be like biology, but that it should be "grown by incremental development" (his quote from Harlan Mill's topdown design paper). Which is akin to agile programming
-He compares well designed languages/systems like: Unix, APL, Pascal, Modula, Smalltalk Interface, Fortran against the bad: Cobol, PL/I, Algol, etc... So funny since Hoare was ragging on PL/I and Algol in the last paper I read (Turing Speech)