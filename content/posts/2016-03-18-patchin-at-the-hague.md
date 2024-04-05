---
title: "Patchin' at the Hague"
date: "2016-03-18"
categories: 
  - "news"
  - "tech"
---

I've been at the [Koninklijk Conservatorium](http://www.koncon.nl) in Den Haag for the last couple of days, working with a group of academics from all over Europe on the METRIC project – 'Modernizing European Higher Music Education through Improvisation'. (If anyone can tell me in which language that acronym works, I'd love to know!)

While I'm here, I've been amusing myself with some work on a simple SuperCollider patch to pitchshift live audio, that I intend to use as part of my own improvisational practice. Particularly tickled to be able to say in future that I 'worked on this patch at the Institute of Sonology in The Hague', which is strictly speaking… more or less true!

Also brings fond memories of another piece of software associated with this institution, [ACToolbox](http://www.actoolbox.net/), that I used quite extensively in the past, although not so much now.

Let's hear it for koncon!

Here's some test code, part of a larger project: `// Institute of Sonology, Den Haag, 18 Mar 2016 :) ( SynthDef(\pitchin, { | trans = 0, gate = 1 | var sig, env, ratio; sig = SoundIn.ar([0,1]); ratio = trans.midiratio; sig = PitchShift.ar(sig, pitchRatio: ratio, timeDispersion: 0.1); env = EnvGen.kr(Env.adsr, gate, doneAction: 2); Out.ar(0, sig * env); }).add; ) x = Synth(\pitchin); x.set(\trans, 12); // can sound a bit comby, try timeDispersion about half grainsize x.set(\trans, -12); x.set(\trans, 7); x.set(\trans, -7); x.free;`
