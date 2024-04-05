---
title: "Bare Wires – text to screech"
date: "2008-11-29"
categories: 
  - "all"
  - "tech"
tags: 
  - "bare"
---

Hers is a very early and approximate proof-of-concept video of a possible text-to-screech interface for 'Bare Wires';

\[youtube=http://www.youtube.com/watch?v=Npii4-3awcQ&hl=en&fs=1&rel=0\]

The idea is to have a laptop and screen onstage, visible to the audience. The setup is used by various performers during the piece, in various ways; to address the audience, or to direct an improvisation, ask questions, tell a story… anything, really.

'text-to-screech' is my coining for taking familiar text-to-speak technology built into many modern computers, and mangle it, creatively misuse it. The most extensive project I have done along these lines was a commission in 2005 for an online piece for Paragon, which is unfortunately not up any more. A similar strategy was used in '[The Other Other Hand](http://workingtitle08.blogspot.com/)', where creatively edited machine speech was used to represent the voice of the Edwardian composer C. Hubert H. Parry.

The interface shown above is done in [Max/MSP](http://www.cycling74.com/products/max5), using the built-in voices on a mac. The first aim was to program it so that it would speak each word immediately after it was typed, which was relatively simple to achieve. In addtition, when an 'x' is typed in a word, the partcular voice used changes, typing 'u' or 'v' subtly affects the rate and pitch of the voice. For the next iteration, I want to try the effect of having it speak the word then display it; also to munge the spoken text more drastically, perhaps mutliple voices speaking, perhaps a more clearly pitched approach, perhaps looping a word, so that the result is more 'musical'.

The demo video above fakes up very roughly what it might be like if one performer types up instructions to the others, and then addresses the audience. Another idea I have been playing with is a game whereby the performers are instructed, for instance, to make some sort of distinctive gesture every time an 'a' is typed, and no to obey any other instructions given. So, for instance, the audience sees the performers being told 'play a note'. The performers actually respond to the two 'a's in the sentence by throwing a book to the floor, which is a the prearranged (invisible) instruction. Then the gag is blown by by one of the performers explaining onscreen what is going on. Then another performer changes the rules… etc etc.

(Another, umm, visual/performative reference here is to [livecoding](http://www.toplap.org/index.php/ManifestoDraft), where an artist improvises live onscreen with a computer programming language to produce music and/or visuals, some nice examples [here](http://impromptu.moso.com.au/gallery.html). I've been doing some experimenting in that direction myself using [SuperCollider](http://supercollider.sourceforge.net/), which can also, as it happens, do text-to-speech. Watch this space…)
