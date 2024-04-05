---
title: "Quartz Composer video sampler for WSWEK"
date: "2013-01-27"
categories: 
  - "news"
  - "tech"
tags: 
  - "wswek"
---

Here's a screenshot of something I've been working on today for 'Why Scotland, Why East Kilbride':

[![wswek-samp01](http://tedthetrumpet.files.wordpress.com/2013/01/wswek-samp01.png?w=630)](http://tedthetrumpet.files.wordpress.com/2013/01/wswek-samp01.png)

Regular readers of this blog (ahem) will recall that this all started with a piece of music I heard in a dream, for a double rock band plus a big squad of french horns. Well, the double rock band is doable, but the french horns were going to be impractical for the gig.

So, I'm building a sort of video sampler. There will be video clips of each of the four chords the horns play, with four different variations of each chord. Midi notes will then be used to trigger a clip of the correct chord. This would have been easy to do using Jitter in Max… so I had to do it the hard way and try to build it in [Quartz Composer](http://en.wikipedia.org/wiki/Quartz_composer)!

I'm getting there, ish. The visual tools in QC are amazing, but the program structuring and logic is kind of Turing-machine basic. Like, to combine four numbers I had to use a combination of three OR gates, and to build a [toggle switch](http://quartzcomposer.wikispaces.com/SignalToggleStructure) it's a counter then take the count modulo 2. And it's crashy and buggy, and the documentation is rudimentary. And I'm going to have to edit the video super carefully, if the clips aren't exactly 2400ms long then my programming will break.

But… it might just work.
