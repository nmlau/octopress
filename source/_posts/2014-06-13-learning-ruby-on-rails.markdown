---
layout: post
title: "Learning Ruby on Rails"
date: 2014-06-13 16:16:28 -0800
comments: true
categories: [technical, project, ruby on rails, web, blog]
published: true
---

## Under Construction

### Table of Contents

* [Introduction](#introduction)
* [Learning Rails](#learningrails)
* [Apps](#apps)
* [Octopress](#octopress)
* [What I Learned](#whatilearned)
* [Conclusion](#conclusion)
* [Technologies behind this Blog](#technologies)
* [Source](#source)


<a name="introduction"></a>
### Introduction

I've always wanted a personal website, for such a long time that I can't even remember the original reason. But it always felt so difficult, like there would be hoop after hoop to jump through. And there were, but I found that each hoop was very easy to jump through, with fantastic resources and frameworks doing almost the entirety of the leg work.

This was one of my first truly independent projects. Prior to this I had always had a partner, professor, TA, etc to fall back on if I got stuck. So this project was stepping out of my comfort zone, which is always difficult. But as I've found, pushing those boundaries has great reward and brings a certain feeling of personal pride and independence.

<a name="learningrails"></a>
### Learning Rails

To learn Ruby on Rails I made use of [Codeacademy Ruby Guide](https://www.codecademy.com/learn/ruby), [Michael Hartl's Ruby on Rails Tutorial](http://ruby.railstutorial.org/), and [Railscast](http://railscasts.com/). Codeacademy was fairly basic and I think is catered towards complete beginners. But looking through there I found some good basic guides to brush up on things like git or commandline. Michael Hartl's tutorial was incredible and even after finishing it I would come back and use it as a reference guide. For things that Michael Hartl's guide couldn't cover I would look through Railscast.

<a name="apps"></a>
### Apps

I started off wanting to build a blog, so I modified Hartl's code for that purpose. Building a dynamic mysql blogged webapp. I wanted to try something a little bit different as well so I build a [Photo Uploading app](upload-app.nicklau.io/). It seemed like it would be difficult but by utilitizing Ruby on Rails gems it turned out to be easy. The Cloudinary gem was quick to setup and did all the heavy lifting, offering a way to upload and store images in the cloud.

I wasn't entirely happy with the blog though, as a one person blog I found the dynamic nature to be redundant. Then I got lucky browsing around the internet reading blogs. I found that this ['Octopress Blog: A Blogging Framework for Hackers'](http://octopress.org/docs/setup/) came up repeatedly, so I decided to check it out. Turns out it was exactly what I was looking for. I thought Ruby on Rails did a lot of the work for me, but Octopress utilizes Jekyll to do even more. It generates posts, provides tools like improved image tags. And above all it is static, so no need for a database, one less thing to worry about breaking. It also takes care of the UI, and lets you download template themes for a personal flare. Or quickly plugin fun additions like Disqus or Google Analytics.

<a name="whatilearned"></a>
### What I Learned

I learned far more than just Ruby and Ruby on Rails. The nature of an independent project is that every step you have to search for the proper tool to do this or that, and you end up finding a lot of new things. For example, I fell in love with the three window (commandline, editor, browser) workflow. I got more comfortable with using commandline debuggers, helping to reduce my dependence on the bloated IDEs I had been stuck with in college. The commandline is very romanticized and it was awesome to get to know it better.

I found out how easy things are, especially since Ruby on Rails has such a strong community. Heroku makes it effortless to deploy your app, gems like New Relic can monitor your app with less than 10 lines and 10 minutes of work. When I wanted to speed my app up, it took copying and pasting in two short blurbs and installing a gem. The hours I spent building a login system from scratch in Michael Hartl's tutorial was replaced instantaneously with the Devise gem (the understanding I got from the tutorial can not be replaced though). I remember setting the devise gem up and looking for the generated code (I thought it was a scaffold). But after checking git and seeing that there were actually no changes to the source... that the system actually worked! 

This is where I started to understand how much of programming is simply reading and interface and plugging to pieces together. How layers like ActiveRecord could be laid on top of your database so that it could handle anything from postgresql, mysql, etc. How REST could be laid on top off resources and interact with them through universal verbs/actions. 

I learned to write user stories and plan out my code better before I started typing (school projects would generally provide structure). I learned to use git better, to branch on features and merge them back only once completed. And that they were only completed once that had an automated test suite. And to use Test Driven Development to make sure they that new features were fulfilling their test cases. I had theoretically known what MVC and REST were, but here I got some first hand experience with them. Things I take for granted like how to write in Markdown.

University didn't expose me to the most interesting language, there were a few weeks of ocaml and python, but asides from that mostly Java and C++. I found Ruby to be very refreshing, being able to do things like 
[inject](http://blog.jayfields.com/2008/03/ruby-inject.html). Or easy list comprehension and array splicing like python. Or how as a dynamic language, it would have really cool methods like 'method_missing()', lazy evaluation, or would put '?' or '!' if it returned a boolean or modified data, respectively. How it had an REPL to play around with an idea, or first class functions (procs, lambdas, closures) intead of the mess that Java callbacks are. It also enforced the idea that despite all the differences, at their root all the languages were very similar. Sure there would be some different syntax, typing, or libraries but in the end it all came down to the idea of structured programming: that everything could be done with a combination of sequence, selection, iteration.

I bought a domain and learned how to use its DNS, which was actually one of the biggest hassles. There isn't a wealth of helpful information online about hosting, and it's very unhelpful that providers work differently so the guides you find aren't entirely applicable. However, the longer it takes you to find something out, the better you understand it, so no harm there.

I learned random invaluable things like Lorem Ipsum and the origins of foobar.

<a name="conclusion"></a>
### Conclusion

Overall I found it very analagous to backpacking around Asia. When you first set out its terrifying, you have no one to rely on. But you learn and quickly find everything to be very easy. You meet incredible people who want to help you. You discover new things about yourself and come out of it a stronger and more independent individual.

<a name="technologies"></a>
### Technologies behind this Blog

This blog webapp utilizes the technologies/services:

* Ruby on Rails obviously!
* Octopress, powered by Jekyll. A blogging framework for hackers.
* gandi.net for hosting and dns services.
* Rack::Cache for faster loading
* Heroku for hosting online as well as the New Relic addon to stop the dyno from idling.
* Devise for user, session, and password management.
* Bootstrap to make things look pretty since I’m no css wizard.
* Rspec and Capybara for quick automated testing.

<a name="source"></a>
### Source

* Source on [github](https://github.com/nmlau/octopress)
* Hosted at [nicklau.io](http://www.nicklau.io/)
