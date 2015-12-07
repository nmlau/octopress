---
layout: post
title: "Raspberry Pi Alarm"
date: 2015-12-01 16:16:28 -0800
comments: true
categories: [Raspberry Pi, DIY, Alarm]
published: true
---

## Under Construction

### Introduction

Put a pic here

I've always had trouble waking up. Sometimes I wake up, sometimes I don't, sometimes I just end up lying in bed... it's been a lifetime point of stress. But in the last few months I've found a solution that works for me. I use the [Sleep Cycle Phone App](http://www.sleepcycle.com/) to gently wake me up so I'm ready for my out of bed alarm that goes off at 630 (weekdays) or 830 (weekends). This forces me to get out of bed to walk across the room and turn it off.

But with the larger problem solved, there's always more you can do to make it more perfect. Right now I'm using an iPad as my out of bed alarm. There's a lot of problems here: it's a really pricey device being used for a very simple task, it can be inefficient to turn off or adjust alarm times (I don't enjoy the gui), the battery will eventually run out, and if I wake up early there's no kill button to stop my normal alarm from going off without remembering to turn them back on.

There's a lot of pros though, the battery lasts for several weeks, it doesn't need to be plugged in (I'm a little OCD and don't want extra wires).

On top of this, I've been hearing about Raspberry Pi's for years and have always wanted to mess around with one. This seemed like the perfect project to get started on the DIY journey.

Note: this isn't so much of a guide as my reflections on my journey to solidify the things I learned.

<!-- more -->

### Components

How I chose my components, used these two guides: [Getting Started Guide](http://www.howtogeek.com/138281/the-htg-guide-to-getting-started-with-raspberry-pi/all/) and [Component Guide](http://www.htpcbeginner.com/raspberry-pi-accessories-for-xbmc-media-center/2/)

Here's what I bought:

- [Raspberry Pi 2](http://www.alliedelec.com/raspberry-pi-raspberry-pi-2-model-b/70465426/)
- [MicroSD Card - Transcend Class 10](http://www.amazon.com/gp/product/B004TA0AUW/) (preferably preloaded with NOOBS, but it's easy to set it up yourself)
- [WiFi Adapter - Edimax](http://www.amazon.com/dp/B003MTTJOY) I got the Edimax rather than the [Panda 300Mbps](http://www.amazon.com/dp/B00EQT0YK2/), because it has a nano adapter and the Panda is overkill at 300Mbps. Or just use ethernet.
- [Power Adapter - Northpada](http://www.amazon.com/gp/product/B00OY7HR1U) Northpada because better reviews, higher mAH, one piece charger. In hindsight, I should have just used one of the many micro USB cables I have sitting around and plugged them into a usb outlet.
- [Case](http://www.amazon.com/gp/product/B00MQLB1N6), although at first I accidentally bought the a [Model 1 Case](http://www.amazon.com/gp/product/B008TCUXLW)

Already owned:

- [Monitor](http://www.amazon.com/Dell-UltraSharp-27-Inch-LED-Lit-Monitor/dp/B00P0EQD1Q), any monitor will do. HDMI is more convenient though
- [Keyboard](http://shop.daskeyboard.com/products/das-keyboard-ultimate-model-s), you can use any usb keyboard, I had a few lying around. Wireless is always convenient too
- [Mouse](http://www.amazon.com/gp/product/B003TG75EG), and any usb mouse. Wireless always good
- [HDMI Display Cable](http://www.amazon.com/gp/product/B0002L5R78), Raspberry Pi has a HDMI display port, I'm sure you've got one lying around. Or if your monitor can't do HDMI, use one of the many adapters out there. All modern display cables are digital and can be converted from one to another.
- [Ethernet](http://www.amazon.com/gp/product/B00316263Y), Got hundreds of these too
- [Speaker](http://www.amazon.com/dp/B00YARCGOC), Choose the favorite one you've got lying around. All you need is a 3.5mm Audio cable to plug it in

[Messing with Infrared](http://ozzmaker.com/2013/10/24/how-to-control-the-gpio-on-a-raspberry-pi-with-an-ir-remote/):

- [Mini Remote Control (IR)](http://www.adafruit.com/products/389)
- [IR Receiver Sensor](http://www.adafruit.com/products/157)
- Ribbon Cable
- Breadboard
- 3 LEDs
- Wires (3 for LED Positives, 3 for LED Negatives, 3v3 power to IR Out, Ground to IR GND, GPIO 18 - PCM_CLK to IR Vs)
- [R1 270n, whatever the yellow boxes are](http://ozzmaker.com/wp-content/uploads/2013/10/IRwiring2.png?csspreview=true)
- Note: Might be able to attach IR sensor straight to GPIO. ALso, LEDs and most wires are just for testing

Optional:

- Heatsink, don't think you need this unless I'm running HD video constantly. A lot of people, like my dad, use their Pi's as DVRs

I ended up doing a headless setup where I ssh'd in from my laptop (more on this later). This eliminated the need for: Monitor, Keyboard, Mouse, Display Cable. And switching to ethernet meant no need for a wifi adapter

### Setup

- Download Noobs (make sure not copy files in, not the folder)
- Download and use formatter, make sure to have lock switch off
- Plug everything in
- Turn on, Install Raspian
- Initial Settings screen: Turn on SSH, expand filesystem

[Setting up headless](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=74176):
I'm a little bit of a neat freak. And I don't have enough space at the moment for a dedicated work bench. So shortly after I went through all the trouble of acquiring and plugging in all the components plugged in I realized I could do better. A headless setup means all the pi needs is an internet connection (wifi adapter or ethernet) and I can use it over ssh.

I got to learn a lot about networking, having to mess around with commands like 'arp -a', 'nmap', modifying /etc/ssh/ssh_config, [learn about MAC and ARP addresses](http://whatismyipaddress.com/mac-address)

Even once I was connected, the workflow was mediocre until I was able to setup:
File Transfer using [afp (appletalk protocol) to pi](http://raspberrypi.stackexchange.com/questions/8950/copy-files-from-osx-to-from-pi)
-Install netatalk on pi, afp in from mac
-This let me use finder and all my os x apps to access my pi's files. Much better than the trouble I was having with Filezilla. Incredibly convenient although it did leave hidden .AppleDouble folders in every directory
Another huge thing was using tmux combined with dtach. Tmux meant I only had to ssh in one time, then I could split that session into several windows. dtach allowed me to shut the pi off, ssh back in jump right back to my desired tmux session.

Random note: sshing in forced me to use command line a lot. Which inspired me to read a few [guides on CLI](), [vim](), that got me play with my profiles (my vim is beautiful now - [image of Solarized profile]()) to setup my profiles like [this](https://github.com/nmlau/profiles)

### Programming

Source available on [github](https://github.com/nmlau/RPiAlarm)

I got my inspiration from: [Speaking Alarm Clock](https://www.youtube.com/watch?v=julETnOLkaU), [github available here](https://github.com/skiwithpete/alarmpi). And some better [Alternative Alarm Clock Projects](https://www.raspberrypi.org/forums/viewtopic.php?f=41&t=95500), most notably the [Simple Google Alarm Clock](https://github.com/bubbl/SimpleGoogleAlarmClock)

One set the alarm with chronjobs, another by hardcoding, but I really liked the Google Calendar integration. And plan to add some pyfeed stuff, particularily to get weather. I also stole how they used datetime module, config parser, os and mpg123 to play sound files. However, all these projects were deprecated because of changes to the Google Calendar Service API.

One of them suggested setting up a socket to listen for real world events, so I'm setting one up to work with an Infrared Remote (IR).

### Brickwalls

Here are some problems that took longer to solve than they should have. In other words, things I learned:
-Setup was actually the longest part, I had to follow a lot of tutorials that didn't work without going in and understanding the commands better
-Changes in Google Calendar API also slowed me down more than they should have. I accidentally setup the deprecated API at first... wish they had thrown a note on the article that it had been deprcated two years ago!
-Just learning python so had some trouble here, easily fixed though. Just read some guides, learned syntax better, got the normal tools like pdb for debugger
-Learned how to use a GPIO, got my EE friends to show me how to use a breadboard, ribbon cable, wiring, etc. Closest I had gotten to this stuff before was an FPGA in my embedded systems course or using VHDL to design a CPU although no actual hardware was involved in that.
-Time was a huge hassle, I learned a lot about how the time modules worked together, and about formatting. I'll probably swap that all out at some point and just use the arrow module