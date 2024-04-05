---
title: "Getting ready to be five (/four)"
date: "2017-03-08"
categories: 
  - "all"
  - "news"
  - "tech"
---

Next Friday I’m going to to be taking part in a 24 hour online algorave event [wearefive](https://algorave.com/wearefive/) to celebrate five years of the algorave movement. By accident or design I’m on back to back with [coï¿¥ï¾¡pt](https://co34pt.bandcamp.com/) (aka Sean Cotterill) who is one of only a couple of us livecoding in pure [SuperCollider](http://supercollider.github.io/), rather than the by-now overwelmingly popular [TidalCycles](https://tidalcycles.org/).

Sean has been putting together [an interesting set of pages](https://theseanco.github.io/howto_co34pt_liveCode/) on his approach to livecoding in SC, particularly on the things that need to be set up beforehand. I’ve evolved some similar ideas myself, perhaps little a less organised and more hacky. For interest, I’ve put my current [setup](http://sccode.org/1-56y) [files](http://sccode.org/1-56x) with comments on sccode.org and also a wee [example](http://sccode.org/1-56z) of the kind of code I use.

Admittedly, some of this won’t make sense without the particular arrangement of samples and loops that I use. I’ve recently hit upon the idea of using an array of 32 different drum samples organised roughly in the following pattern:

00 a bass drum sound 01 hi hat 02 a snare 03 a different hi hat (or other hit) 04 a different bass drum sound … etc

That way, I can make a basic un-ta-ka-ta beat just by stepping through all 32, or segments thereof:

`Pseq(~arrayOfHits, inf) Pseq(~arrayOfHits[4..7], inf)`

I’ve also discovered some really quite good longer patterns with this layout, using Pslide:

`Pslide(~arrayOfHits,inf,4,3)`

Guess we'll see how all of this sounds at the rather unravy time of 0800 GMT next Friday!
