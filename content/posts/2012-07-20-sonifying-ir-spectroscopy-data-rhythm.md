---
title: "Sonifying IR spectroscopy data – rhythm"
date: "2012-07-20"
categories: 
  - "news"
---

For today's exciting episode, I'm using the simplified spectrum data from glycine to generate a sound, and then looping round the same data to play the sound in a kind of 'rhythm':

```
[sourcecode]
(
~name = "glycine";
~path = Document.current.dir.asString++"/"++ ~name ++".csv";
f = CSVFileReader.readInterpret(~path);

f = ((f.flop[1] * -1) + 1).normalize;

f = (f*100).asInteger;
f = f.differentiate.removeEvery([0]).integrate;
f = f/100;

~peaksIndices = f.differentiate.sign.findAll([1,-1]);

g = Array.fill(f.size, 0);

~peaksIndices.do { |i| g[i] = f[i] }; // Daniel's line

~amps = g;

// [f,~amps].plot(~name, Rect(840,0,600,450));

~freqs = (36..128).resamp1(f.size).midicps;

SynthDef(\glycine, { | gate=1, amp |
	var env, sig;
	sig = Klank.ar(`[~freqs, ~amps, nil], PinkNoise.ar(amp/100));
	env = EnvGen.kr(Env.perc, gate, doneAction: 2);
	Out.ar(0, Pan2.ar(sig, 0, env))
}).add;

Pbind(	\instrument, \glycine,
		\amp, Pseq(~amps, 4).collect { |amp| if(amp &gt; 0) {amp} {Rest}},
		\dur, 0.02,
).play;
)

[/sourcecode]
```

\[audio src="https://tedthetrumpet.files.wordpress.com/2008/09/glycinerhythm.mp3"\]\[/audio\]

[glycinerhythm.mp3](http://tedthetrumpet.files.wordpress.com/2008/09/glycinerhythm.mp3)

In other news, my collaborator Steve has been having Ideas. Watch this space.
