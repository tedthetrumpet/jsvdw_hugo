---
title: "Routing text-to-speech on the mac"
date: "2011-08-02"
categories: 
  - "news"
  - "tech"
---

http://www.youtube.com/watch?v=3FG\_tsG7mI4

There are any number of ways of working with the built-in text-to-speech synthesis capabilities on the mac. All of the music programming languages I use - [Max](http://cycling74.com/ "http://cycling74.com/"), [Pd](http://puredata.info/ "http://puredata.info/") and [SuperCollider](http://supercollider.sourceforge.net/ "http://supercollider.sourceforge.net/") - offer ways of doing this, and I've also had great success with controlling the output using AppleScript. The problem is that in every case, the audio itself is actually synthesised by the mac os itself, which means it is not accessible within an audio environment for further processing.

I was inspired to have another think about this recently by a [thread](http://new-supercollider-mailing-lists-forums-use-these.2681727.n2.nabble.com/Jacked-Speech-td6604162.html "http://new-supercollider-mailing-lists-forums-use-these.2681727.n2.nabble.com/Jacked-Speech-td6604162.html") on the SuperCollider list where somebody was trying to do exactly this, by using [Jack](http://jackosx.com/ "http://jackosx.com/") to route the sound from the mac back into the application for further processing. What I've started to experiment with is routing the audio into a _different_ application: in the example above, controlling the speech synthesis in Max and passing the audio into Pd. Combined with the facility to pass midi from Max to Pd (easy), I think I can see how I can make a workable and potentially interesting system. But, for now, just proving to myself that it can be done :)
