---
layout: post
title: "Commandline Shenanigans"
date: 2016-01-07 14:57:53 -0800
comments: true
categories: [technical, commandline, shell, vim, tmux]
published: true
---

### Table of Contents

{% img /images/commandline_post/tmux_solarized_dark_profile.png 'tmux_solarized_dark_profile.png' %}

* [Art of the Command Line](#artofthecommandline)
* [Mastering Vim](#masteringvim)
* [Tmux](#tmux)
* [Profiles](#profiles)
* [One-liner for Killing Applications](#onelinerforkillingapplications)

<!-- more -->

<a name="artofthecommandline"></a>
### Art of the Command Line

I've always been interested in learning the Command Line better. So I was pretty excited to find this guide on [Hacker News](https://news.ycombinator.com/), or was it [r/programming](https://www.reddit.com/r/programming/)? [The Art of the CommandLine](https://github.com/jlevy/the-art-of-command-line) by [jlevy](https://github.com/jlevy) works as an overview of the most useful things, giving a short introduction so you know what's what. You can then look more into the things using 'man' or a quick google search.

It was a fantastic review of the stuff I knew and introduced me to lots of new tools. Here's a portion of my raw notes on things that were relatively new to me:

* Everyday Use:
  * xargs (example makes no sense)
  * HERE document (code block that io redirects list to a command)
  * mosh (ssh type thing using udp)
  * percol/fzf (interactive selection of values from output of another command)
* Processing Files and Data:
  * uniq (uniq reports or filters out repeated lines in a file, these would be perfect for lucky times)
  * cut/paste/join, pretty intuitive names but never used or seen these used before
  * awk/sed, awk is a pattern directed scanning and processing language, sed is a stream editor
  * repren, for complex renames
  * rysnc, versatile and fast file copying tools
  * shuf, shuffle or select random names
  * patch, works with diff to be the standard for patching source code
  * hd/hexdump/xxd/bvi/biew/strings+grep/xdelta3 for binary files...
  * iconv, convert text encodings
  * split/csplit to split by size or pattern
  * zless, zmore, zcat, zgrep to operate on compressed files
* Cool things:  
  * Press ctrl-r repeatedly to cycle through more matches,... or hit the right arrow to put the result in the current -line
  * ctrl-a, #, enter //enters command as comment so you can go back and edit it later
  * Brace expansion using {...}, cp somefile{,.bak} (which expands to cp somefile somefile.bak) 
  * The output of a command can be treated like a file via <(some command). ie, vim <(env)
  * man ascii
  * tmux/screen to multiplex the screen (byobu to enhance tmux, dtach for session persistence)
  * fpp (pathpicker) looks incredibly useful
  * Tab literal, ctrl-v [Tab] or write $'\t' (the latter is better as you can copy/paste it)
  * OSX: "Use Option as Meta key". To enable the Option key in Mac OS Terminal as an alt key (such as used in the commands above like alt-b, alt-f, etc.). Does wonders for emacs.

After going through this I decided to dive deeper into:

* xargs
* grep
* vim
* tmux/dtach (although I wasn't happy with dtach and use tmuxinator instead)
* zsh
* Profiles (terminal, bash, key remapping, etc)
* Cleaning up my environment (ex: had brew and macports fighting with eachother)

<a name="masteringvim"></a>
### Mastering Vim

Vim needs no introduction. I used vim a lot during university, but just got by rather than pushing the boundaries of what it can actually do. Yes I do love sublime text and neat things it can do like multiple cursors. But vim is incredible, and there is a reason people have been using it for decades.

Inspired by The Art of the CommandLine, I found this went searching for a Vim Guide and found [Mastering Vim by Daniel Miessler](https://danielmiessler.com/study/vim/).

Here's a portion of my notes:

* u and U interaction is unintuitive to me
* CTRL+G, line number+G
* CTRL-O, CTRL-I
* %
* :#,#s/old/new/g
* :%s/old/new/g
* :%s/old/new/gc
* :!
* :set ic hls is
* :set incsearch
* :set noic
* :nohlsearch
* /ignore\c
* :e (followed by CTRL+D)
* CTRL+L for redraw
* CTRL+[ for ESC
* CTRL+E for scroll up
* CTRL+Y for scroll down
* zz, zt, zb for scroll

To practice I went through vimtutor and played [vim adventures](http://vim-adventures.com/). Now I'm making a Javascript game with the Phaser framework that will make use of vim commands for controls

<a name="tmux"></a>
### Tmux

"[tmux](https://tmux.github.io/) is a "terminal multiplexer", it enables a number of terminals (or windows) to be accessed and controlled from a single terminal. tmux is intended to be a simple, modern, BSD-licensed alternative to programs such as GNU screen."

Tmux would have been an absolute lifesaver when I was back in school as I did a lot of my work by sshing into the school servers. It would have allowed me to login once and create multiple panes/windows instead of having to login multiple times. So many regrets. It has been instrumental for sshing in and working with my raspberry pi though.

First thing I did was change to prefix from ctrl+a to ctrl+b. The prefix is what you use before entering tmux commands. ctrl+a was originally saved for screen (since the creator of tmux used screen while developing tmux). However, ctrl+a is much easier on your fingers than ctrl+a.

The Art of the CommandLine recommended dtach for session persistence, but I found the redraw to be very buggy. So I looked around and found [Tmuxinator](https://github.com/tmuxinator/tmuxinator), which gas worked perfectly!

<a name="profiles"></a>
### Profiles

You can find most of my [Profiles](https://github.com/nmlau/profiles) here. This allows them to be cloned in and set up quickly and conveniently. It also allows me to keep track of them in one place. Since hitting 'ls -al' in ~/ is kind of messy.

I messed around with my profiles and environment:

* Setup [zsh](http://www.zsh.org/) and [Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)
* Installed [Solarized Dark theme](http://ethanschoonover.com/solarized) for terminal
* Changed to [iTerm2](https://www.iterm2.com/)
* Remapped keys: caps to control, remapping vims 'jk' to escape
* Fixed up [Homebrew](http://brew.sh/) by getting rid of macports, fixing permissions, etc (lots of running 'brew doctor')
* Changed host/terminal name
* etc

<a name="onelinerforkillingapplications"></a>
### One-liner for Killing Applications

Art of the Command Line brought up these:

``` bash
ps -ax | grep Finder
kill -9 390
```

And I had run into this command: kill `jobs -ps`, when messing around with background processes

At the same time, I've always been frustrated by how much time it takes to start up Activity Monitor, search for the offending process, and then clicking multiple times to force quit it. And I've always got a terminal open so why not just use that and get it done with no waiting, few key presses, and zero clicks. So I looked back at these commands which were pretty close already. I figured I'd learn some bash and try to combine them into a one liner that I could throw into an alias for my .zshrc.

I started with this, it read from jobs. And awk would pass the process id column to xargs which would call 'kill' on them

``` bash
zsh: jobs -p | awk '{print $3}' | xargs kill
```

But jobs obviously wasn't right, we wanted 'ps -ax' and to use grep to target the offending app. As well as 'kill -9' to forcequit.

``` bash
ps -ax | grep Finder | awk '{print $3}'
ps -ax | grep 'TextEdit' | awk '{print $1}' | xargs kill -9
```

Now there was the issue of passing in the app name as a variable, which requires a [bash function](http://stackoverflow.com/questions/941338/how-to-pass-command-line-arguments-to-a-shell-alias).

``` bash
alias killapp='function _killapp(){ps -ax | grep $1 | awk '{print $1}' | xargs kill -9};_killapp'
```

However, now the the grep $1 and awk $1 interfere with eachother. You can pass grep directly to xargs, '... grep $1 | xargs kill -9'... but that's not ideal. I tried a few things, like using a variable. As well as a variety of backslashes and [quotes around quotes](http://superuser.com/questions/114798/is-there-a-way-to-escape-single-quotes-in-the-shell)

``` bash
alias killapptest='function _killapp(){arg1="$1"; ps -ax | grep $arg1 | awk "{print $1}";_killapp' //using variable
```

Eventually I found the way that worked, by [escaping the $](http://stackoverflow.com/questions/7244534/using-awk-in-bash-alias-or-function):

``` bash
* alias killapp='function _killapp(){ps -ax | grep $1 | awk "{print \$1}" | xargs kill -9};_killapp'
```

But not perfect, since grep would find itself. To solve this I found this [stackoverflow thread](http://unix.stackexchange.com/questions/74185/how-can-i-prevent-grep-from-showing-up-in-ps-results) which recommended: 

``` bash
pgrep or 'ps aux | grep -v grep | grep "fnord"'
```

Looking more into pgrep, I remembered seeing it along with pkill in the Art of the Command Line under [Everyday Use](https://github.com/jlevy/the-art-of-command-line#everyday-use). And so with some frustration, to quote myself at that moment:

> WELL LOOKS LIKE I JUST REINVENTED PGREP/PKILL, THERE GOES AN HOUR AND SOME PRIDE. WELL I GUESS I LEARNED SOMETHING AT LEAST
