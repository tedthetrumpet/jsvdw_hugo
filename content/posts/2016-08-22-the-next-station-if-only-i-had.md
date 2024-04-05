---
title: "The Next Station – ‘if only I had’"
date: "2016-08-22"
---

Tomorrow sees the launch of [The Next Station](http://www.citiesandmemory.com/thenextstation), a project by Cities and Memory to reimagine the sounds of the London Underground. My contribution to this project is an audio work called [_if only I had_](https://audioboom.com/boos/4896960-if-only-i-had-pimlico-station), constructed entirely from a 3'42 recording of a train arriving and departing from Pimlico station.

The title is taken from Spike Milligan’s ‘Adolf Hitler: My Part in his Downfall’:

‘Edgington and I promenaded the decks. Harry stopped: “If only I had a tube.” “Why?” “It’s quicker by tube.”

… an inconsequential pun that has, for some reason, always stuck in mind!

I made this piece as a personal study into the possibility of using [livecoding](http://toplap.org/) techniques in [SuperCollider](http://supercollider.github.io/) to develop a fixed piece. In recent months I have been very active in exploring coding in this way, particularly in the context of [algorave](http://algorave.com/): _if only I had_ leverages these techinques. Here’s some of the code I used, with explanation:

`( s.waitForBoot{ Pdef.all.clear; Pbindef.defaultQuant = 4; t = TempoClock.new.tempo_(120/60).permanent_(true); ~path = "/Users/jsimon/Music/SuperCollider Recordings/pimlicoloops/";`

This is a remnant of what turned out to be a bit of a false start to the project. My initial idea was to look through the file for shortish sections, in the region of 2-3 seconds long that, when looped, had some sort of rhythmic interest. This was done offline, using [Audacity](http://www.audacityteam.org/). I thought it might be interesting to develop the piece by using these fragments almost in the manner of drum loops, and wrote some code to juxatpose them in various ways at different tempi. This didn't really produce anything very effective however: the material is rather dense and noisy, and when looped together the rhythmic interested was lost in broadband mush of sound.

Instead, I revisited a synth from an earlier project that slices a buffer into 16 pieces for playback:

`~bufs = (~path ++ "*.aiff").pathMatch.collect({ |i|  Buffer.read(s, i)}); SynthDef(\slbuf, { |out, buf, slices=16, slice=16, freq=440, sustain=0.8| var myenv, env, start, len, basefreq = 440, rate, sig, sus; rate = freq / basefreq; len = BufFrames.kr(buf); start = (len / slices * slice); sus = BufDur.kr(buf)/16 * sustain * 1.1; myenv = Env.linen(attackTime: 0.01, sustainTime: sus, releaseTime: 0.1); sig = PlayBuf.ar(2, buf, BufRateScale.kr(buf) * rate, startPos: start, loop: 1); env = EnvGen.kr(myenv, 1, doneAction: 2); Out.ar(out, sig * env) }).add;`

As well as experimenting with reverb, I also had a delay effect in here at one point. Again, the nature of the already fairly resonant material meant that this was not that useful. In the end, I only used the reverb at the very end of the piece as a closing gesture.

`~rbus = Bus.audio(s, 2); SynthDef(\verb, {|out = 0, room = 1, mix = 1| var sig = FreeVerb.ar(In.ar(~rbus, 2), room:room, mix:mix); Out.ar(out, sig) }).add; s.sync; Synth(\verb);`

At some point in developing the project, it occured to me to try playing together the sliced material with the orignal file. This seemed to effective, and gave me a clear trajectory for the work: I decided that the finished piece would be the same pop-song length as the original recording. In experimenting with this approach – playing sliced loops in SC at the same time as playing back the whole file in Audacity – I found myself gently fading the original in and out. This is modelled in the synth below: I used an explicit random seed together with interpolated low frequency noise to produce a replicable gesture:

`~file = "/Users/jsimon/Documents/ Simon's music/pimlico the next station/Pimlico 140516.wav"; ~pimbuf = Buffer.read(s, ~file); s.sync; SynthDef(\pim, { |out=0, start=0, amp = 1| var sig, startframe, env; startframe = start * 44100; RandSeed.ir(1,0); env = EnvGen.kr(Env.linen(sustainTime: ~pimbuf.duration - 9, releaseTime:9)); sig = PlayBuf.ar(2, ~pimbuf, startPos:startframe, doneAction:2) * LFNoise1.kr(1/5).range(0.05, 1.0); Out.ar(out, sig * amp * env); }).add;`

There was a nice moment in the original where the accelerating electronic motors of the departing train created a seried of overlapping upward glissandi, sounding very like Shepard tones, or rather, the sliding Risset variation. Looking to enhance this gesture, I tried a couple of my own hacks before giving up and turning to a nice class from Alberto de Campo’s [adclib](https://github.com/supercollider-quarks/adclib):

`~shep = { var slope = Line.kr(0.1, 0.2, 60); var shift = Line.kr(-1,2,60); var b = ~bufs[8]; var intvs, amps; var env = EnvGen.kr(Env.linen(sustainTime:53, releaseTime:7),1,doneAction:2); #intvs, amps = Shepard.kr(5, slope, 12, shift); (PlayBuf.ar(b.numChannels, b, intvs.midiratio, loop: 1, startPos:3*44100) * amps).sum * 0.2 }; s.sync;`

All of the above is essentially setup material. The gist of the composition was in iterative experimentation with Pbindefs, as can be seen below: trying out different slicing patterns and durations, working with the various segments I'd prepared beforehand in Audacity.

`Pbindef(\a, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/2, \buf, ~bufs[1], \note, 0); Pbindef(\b, \instrument, \slbuf, \slice, Pser((8..15).pyramid(1), 32), \dur, 1/4, \buf, ~bufs[1], \note, 0); Pbindef(\c, \instrument, \slbuf, \slice, Pser((2..5).pyramid(1), 32), \dur, 1/4, \buf, ~bufs[0], \note, 0); Pbindef(\d, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/4, \buf, ~bufs[3], \note, 0); Pbindef(\e, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/4, \buf, ~bufs[3], \note, 12); Pbindef(\f, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/4, \buf, ~bufs[3], \note, [-12,12,24,36]); Pbindef(\g, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/4.5, \buf, ~bufs[3], \note, [12,24,36]); Pbindef(\h, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/5, \buf, ~bufs[3], \note, [-12,12,24,36]); Pbindef(\i, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(12), 1), \dur, 1/6, \buf, ~bufs[3], \note, [-24,-12,12,24,36]); Pbindef(\j, \instrument, \slbuf, \slice, Pseq((1..8).pyramid(1), 1), \dur, 1/7, \buf, ~bufs[3], \note, [-24,-12,12,24,36], \amp, 0.3); Pdef(\k, (instrument: \slbuf, buf: ~bufs[3], slice: 2, note: [-24,-12,12,24,36], amp: 0.5, out:~rbus));`

s.sync; };

The final composition was produced by running and recording the code below, which uses the handy Psym as a way to sequence the gestures developed above. The code by this point is entirely deterministic, and would produce the same piece on every run. No further editing was done, apart from normalising in Audacity.

`// start from beginning fork{ Synth(\pim); 2.wait; Psym(Pseq("aabaccddeeffghiijk",1).trace).play(t); (60+14+20).wait; "shep".postln; ~shep.play; 10.wait; "off again".postln; Psym(Pseq("aabaccddeeffghiijk",1).trace).play(t); }; ) s.prepareForRecord s.record s.stopRecording`

Overall, I'm happy with the piece, and glad to have been able to contribute to this very interesting project.
