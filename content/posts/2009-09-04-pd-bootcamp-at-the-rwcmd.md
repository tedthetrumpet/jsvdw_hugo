---
title: "Pd Bootcamp at the RWCMD"
date: "2009-09-04"
categories: 
  - "all"
  - "tech"
---

All week I've been on a PureData course at the [Royal Welsh College of Music and Drama](http://www.rwcmd.ac.uk/), with Simon Kilshaw. [PureData](https://puredata.info/), or Pd, is a free and open source graphical programming language for music and video; in plain language, a system allows one to plug together a series of graphical objects on a screen in order to create an original work of digital art.

Pd is closely allied with another very similar language, [Max/MSP](http://cycling74.com/products/max5), both having in fact been initiated by the same programmer, [Miller Puckette](http://crca.ucsd.edu/%7Emsp/). I've been working with and teaching a Max/MSP course for several years now; so why study Pd? Max/MSP is in many ways a much slicker and more fully developed environment, significantly easier to use, with clear documentation and tutorials, many higher level objects built in, and a large community of users. By contrast, coming to Pd from Max feels like a step back in time; the user interface seems clunky, many basic objects seem to be missing, the documentation is by comparison chaotic, and overall it feels like a poor relation.

Well, poor; yes exactly! You would be if you had to buy Max/MSP at the full commercial going rate of $699, and the 'price point' of Pd is undoubtably a serious attraction. More importantly, perhaps, the open source nature of Pd creates a different kind of community, one where it is perhaps easier for creative artists to own and share their digital works without being encumbered by licencing considerations.

The course here has been quite a full-on experience. Simon and his students at RWCMD seem to have a programming style which is extremely fast and hacky, driving straight at getting musical results from the software without much concern for neatness or elegance. It works; most of the week we've been following along behind Simon click-by-click as he more or less improvised patches before our eyes. Graphical languages are great for this kind of very rapid prototyping and developing of ideas, although I found that for my style of working I liked to go a little bit slower and think through what I was doing a little more.

Over the last two days we've also seen some of the work of one of the graduates here, Tristan Evans, including a very impressive piece for piano and Pd called '[Takeover](http://www.youtube.com/watch?v=QN06Ipq7ldk)'. Tomorrow, we're scheduled to put together a collaborative performance using a rather remarkable internet-based version of Pd, [netpd](http://netpd.org/); if all goes according to plan you should be able to watch and hear us all performing live using [this url](rtsp://194.82.127.93/mystream.sdp) at 1500 GMT+1 (that's three o'clock UK time).

I'll (maybe) be performing on the patch above. For those who are interested, this uses nothing which is not in Pd-extended (I hope!). The guts of the sound are four Karplus-Strong 'pluck' synths, with the delay lengths changing at random to produce glissando effects. These gestures are fed into an instance of freeverb, where the reverb tail can be frozen; while the tail is frozen, a pitch shifter patch is used to move this sound around in interesting ways. The klang gestures are either triggered manually, or by a randomised metronome, which can be set to the rather ridiculous value of 25 ms to produce an insane cascade of stringy sounds.
