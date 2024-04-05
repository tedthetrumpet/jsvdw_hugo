---
title: "First public livecode"
date: "2016-04-26"
categories: 
  - "news"
  - "tech"
---

Last night I stumbled into my first public outing of some livecoding I've been working on in [SuperCollider](http://supercollider.github.io/). The context was an improvisation night called [In Tandem](https://www.facebook.com/events/1081102458615158/) run by [Bruce Wallace](http://cargocollective.com/whatitisis/about-what-it-is-is) at the [Academy of Music and Sound](http://academyofmusic.ac.uk/) in Glasgow. I hadn't intended to play, as I really don't feel I'm ready yet, but I had my laptop and cables with me, they had a projector, so…!

I was jamming along with three other people, on bass, guitar and analog synth. It all went by in a blur, but everyone there seemed to think what I was doing was ok – mostly making grooves out of a random collection of drum samples, but running some algorithmically chosen chords as well.

The code is below: this is my screen exactly as I left it at the end of the night, mistakes and all. Although [Toplap](http://toplap.org/wiki/Main_Page) say 'show us your screens', they don't say 'show us your code', but… it seems the right thing to do.

`// the end! // they still going // if you're curious, this is SuperCollider // musci programming language // writing code live is called, er, livecoding // i'm just starting out "/Users/jsimon/Music/SuperCollider Recordings/hitzamples/".openOS;`

`( s.waitForBoot{ Pdef.all.clear; // clear things out ~hitzpath="/Users/jsimon/Music/SuperCollider Recordings/hitzamples/"; // a folder of samples ~hbufs = (~hitzpath ++ "*.aiff").pathMatch.collect({ |i| Buffer.read(s, i)}); // samples into an array of buffers t = TempoClock(140/60).permanent_(true); // tempo 140 bpm u = TempoClock(140/60 * 2/3).permanent_(true); // tempo 140 bpm * 2/3 SynthDef(\bf, {|out=0 buf=0 amp=0.1 freq=261.6255653006| var sig = PlayBuf.ar(2, buf, BufRateScale.kr(buf) * freq/60.midicps, doneAction:2); Out.ar(out, sig * amp) }).add; // this whole chunk defines a synth patch that plays samples };  // Pdef.all.clear; //"/Users/jsimon/Music/SuperCollider Recordings/".openOS; // t.sync(140/60, 16); )  (instrument: \bf, \buf: ~hbufs.choose).play; // play an event using the synth called \bf // pick a randoms sample from the array (instrument: \bf, \buf: ~z).play; ~z = ~hbufs.choose;  t.sync(140/60, 32); // gradual tempo changes possible u.sync(140/60 * 2/3, 16); v.sync(140/60 * 5/3, 16);  Pbindef(\x, \instrument, \bf, \buf, ~hbufs.choose).play(t).quant_(4); Pbindef(\y, \instrument, \bf, \buf, ~hbufs.choose).play(u).quant_(4); Pbindef(\z, \instrument, \bf, \buf, ~hbufs.choose).play(v).quant_(4); Pbindef(\z, \instrument, \bf, \buf, ~hbufs.choose).play(v).quant_(4); ~g1 = {~hbufs.choose}!16; // choose sixteen samples at random = one bar full ~g2 = {~hbufs.choose}!16; Pbindef(\x, \buf, Pseq(~g1, inf)); // play those sixteen samples chosen Pbindef(\x, \buf, Pseq(~g2, inf)); // different sixteen, so, a variation. Pbindef(\x, \dur, 0.5); ~d1 = {2.rand/10}!16; ~d2 = {2.0.rand/10}!16; Pbindef(\x, \amp, Pseq(~d1, inf)); Pbindef(\x, \amp, 0.2); Pbindef(\x, \note, Prand((-36..0), inf)); Pbindef(\x, \note, Pseq({(-24..0).choose}!16, inf)); // pitch each sample down by random amount Pbindef(\x, \note, nil); Pbindef(\x).resume; Pbindef(\x).pause; Pbindef(\z).pause; Pbindef(\y).resume;  // hmm. blx diminished, that's just C major! // was using \degree instead of \note, better sounds a bit more like messiaen now :) ~c = {var x = Scale.diminished2.degrees.scramble.keep(4).sort; x.insert(1,(x.removeAt(1)-12))}; // hexMajor thing also works beautifully now! ~c = {var x = Scale.hexMajor6.degrees.scramble.keep(4).sort; x.insert(1,(x.removeAt(1)-12))};  ``// next question might be changing \note, \dur and \root in a coordinated way ( Pbindef(\k, \note, Pstutter(Prand([5,7,9,11,13]*2, inf), Pfunc(~c)), \dur, 0.5, \root, 3, // best option for feeling of key change \amp, Prand((2..5)/70,inf) ).play(t); ) Pbindef(\k).pause; Pbindef(\k).pause;`