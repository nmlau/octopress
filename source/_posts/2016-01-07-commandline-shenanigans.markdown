---
layout: post
title: "Commandline Shenanigans"
date: 2016-01-07 14:57:53 -0800
comments: true
categories: [commandline, shell, vim, tmux]
published: true

---

# Under Construction

#### **Important Note: Nothing I did worked the first time, so I was constantly forced to solve new problems and learn new things**

### Table of Contents

* Art of the CommandLine
* Mastering Vim
* Tmux
* Profiles
* One-liner for Killing Applications

### Art of the CommandLine

I've always been interested in learning the CommandLine better. So I was pretty excited to find this guide on Hackernews, or was it r/programming? [The Art of the CommandLine](https://github.com/jlevy/the-art-of-command-line) works as an overview of the most useful things, giving a short introduction so you know what's what. You can then look more into the things using 'man' or a quick google search.

Here's a portion of my raw notes (things that were relatively new to me):

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
  * tab literal, ctrl-v [Tab] or write $'\t' (the latter is better as you can copy/paste it)

After going through this I decided to dive deeper into:

* xargs
* grep
* vim
* tmux/dtach (although I wasn't happy with dtach and use tmuxinator instead)
* zsh
* profiles (terminal, bash, key remapping, etc)
* cleaning up my environment (ex: had brew and macports fighting with eachother)

Notes:
OS X Only:
-"To enable the Option key in Mac OS Terminal as an alt key (such as used in the commands above like alt-b, alt-f, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key"."
-How to change option to meta key properly: http://goo.gl/jrJDW
-Holy shit now emacs is usable, and it was easy to fix

### Mastering Vim

I used vim a lot of school, but just got by rather than pushing the boundaries of what it can actually do. Yes I do love sublime text and neat things it can do like multiple cursors. But vim is incredible, and there is a reason people have been using it for decades.

Inspired by The Art of the CommandLine, I found this, [Mastering Vim](https://danielmiessler.com/study/vim/).

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

### Tmux

Tmux would have been an absolute lifesaver when I was back in school. Since I did a lot of my work by sshing into the school servers. So many regrets.

First thing I did was change to prefix from Ctrl+a to Ctrl+b.

The Art of the CommandLine recommended dtach for session persistence, but I found it didn't work very smoothly. Setting up Tmuxinator solved the problem though.

### Profiles

You can find most of my [Profiles](https://github.com/nmlau/profiles) here. This allows them to be cloned in and set up easily. Also allows me to keep track of them in one place. Since hitting 'ls -al' in ~/ is kind of messing.

I did a lot of messing around with my profiles and environment:

* setup zsh and oh my zsh
* installed solarized dark theme for terminal
* changed to iTerm2
* remapped keys: caps to control, remapping vims 'jk' to escape
* got rid of macports and fixed brews permissions (lots of running 'brew doctor')
* changed host/terminal name

### One-liner for Killing Applications

[2] Figure out how to combine kill processes:

* Ask on Stackoverflow?
* kill `jobs -ps` # Kill jobs running in background
* ps -ax | grep Finder
* kill -9 390
* zsh: jobs -p | awk '{print $3}' | xargs kill
* ps -ax | grep Finder | awk '{print $3}'
* ps -ax | grep 'TextEdit' | awk '{print $1}' | xargs kill -9
* Bash functions for replacement text, http://goo.gl/zqlude
* Single in double quotes or vice versa to escape, http://goo.gl/ccL5mp
* alias blah='function _blah(){ echo "First: $1"; echo "Second: $2"; };_blah'
* alias killapp='function _killapp(){ps -ax | grep Finder};_killapp'
* alias killapp='function _killapp(){ps -ax | grep $1 | awk '{print $1}' | xargs kill -9};_killapp'
* alias killapptest='function _killapp(){arg1="$1"; ps -ax | grep $arg1};_killapp' //using variable
* alias killapptest='function _killapp(){arg1="$1"; ps -ax | grep $arg1 | awk "{print $1}";_killapp' //using variable
* FINAL:
alias killapp='function _killapp(){ps -ax | grep $1 | awk "{print \$1}" | xargs kill -9};_killapp'
* Not perfect, grep seems to find itself
* pgrep or 'ps aux | grep -v grep | grep "fnord"' would fix finding itself, http://goo.gl/H9XhRL
* Running simplehttp server on different port, but don't run below 1024, http://goo.gl/tvTJmx
* Fixing my 'awk {print $1}' conflicting $1 issue, http://goo.gl/Sct0Ji

WELL LOOKS LIKE I JUST REINVENTED PGREP/PKILL, THERE GOES AN HOUR AND SOME PRIDE. WELL I GUESS I LEARNED SOMETHING AT LEAST