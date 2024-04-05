---
title: "Max 5 to SuperCollider using OSC"
date: "2010-06-18"
categories: 
  - "tech"
---

http://www.youtube.com/watch?v=1QhG4cpS9ik

### Updated

I guess it's just possible some people might not get what's going on here :) [SuperCollider](http://supercollider.sourceforge.net/) is a very powerful text-based programming language for sound. If you know what you're doing, then with just a couple of lines of code you can create really fascinating sounds and textures, even entire compositions; see for instance [sc140](http://supercollider.sourceforge.net/sc140/), an album where each piece is created using just a twitter-long 140 characters of code.

Unfortunately, I _don't_ know what I'm doing; my mind doesn't seem to work logically enough to really do computer programming properly! Enter the other half of the equation, [Max 5](http://cycling74.com/products/maxmspjitter/) (or Max/MSP as it used to be known). This is a _graphical_ programming language, which allows you to make stuff happen just by plugging things together on the screen.

I've got quite good at Max, and sometimes managed to make quite interesting sounds in SuperCollider.  I found the missing link between these two on [a great blog posting by Fredrik Olofsson](http://www.fredrikolofsson.com/f0blog/?q=node/401). It's a way of using a so-called 'quark', a type of extension to SuperCollider, to send OSC (Open Sound Control) messages from Max to SC. So, what I'm happy to have found here is an easy way to attach knobs to these hard-to-get-at text based sounds. The next step from here will be controlling SC using external midi/bluetooth/whatever hardware, again via Max.
