---
title: "Rave the Space"
date: "2016-10-06"
categories: 
  - "news"
  - "tech"
---

Last night I gave a performance called 'Rave the Space' at Stereo in Glasgow, part of a series of events called [INTER](http://www.stereocafebar.com/listings/events/5-oct-16-inter--7-sonic-spaces-in-between-stereo/) run by Iain Findlay-Walsh 'creating a focused, public listening context for deep experiments in / with sound'.

My proposal was to 'perform the soundscape of the venue through the medium of livecoding'. What I did was to visit the venue the day before, at a quiet time, and make some recordings – a fairly typical basement club/rock venue, so I was able to wander onstage, through dressing rooms, behind the bar, into the toilets etc, all the while recording both the ambience and, in some cases, tapping or hitting objects of particular interest – there was a group of CO2 cylinders that were particularly nice.

On the morning of the event, I roughly levelled these recordings, discarded uninteresting ones, cut out handling noise, mobile phone interference, and initial and terminal clicks from the recorder. This left me with nine recordings, each about a minute long.

I decided to challenge myself by doing as little rehearsal for the performance as possible. I had one synth precoded, a slicing sampler. All this does is to take an audio file and play back one of n slices: in the case of these roughly 60 second long files, I used n=64. On previous occasions when I've done livecoding/algorave with found sounds, I've gone through the source audio files carefully in Audacity, looking for particular short sounds that I can then isolate and shape into something resembling a drum hit, then performed with those sounds in place of drum sounds.

The slicing approach used here is deliberately less controlled: it's a matter of luck what sound falls where as the point at which the file is sliced is quite arbitrary, perhaps falling just on ambience, or half-way through a percussive noise.

The performance was only to be ten minutes: which is not a lot on my timescale of livecoding in SuperCollider! I decided to start with a blank screen: in retrospect, I could have got to better musical gestures faster if I'd had maybe ten or a dozen lines precoded. Nevertheless, in this sit-down and concentrate atmosphere, the blank-page start was quite intruiging for the audience, I think.

The performance mostly went well, although there was one of those moments where I had what looked like a correctly typed line that evaluated correctly, that did not seem to be doing anything! I still can't figure out what I was doing wrong.

I'm pleased with this idea and intend to repeat it, particuarly the site-specific approach to gathering sounds.

Here's the code, not much to see here:

`(//setup s.waitForBoot{}; SynthDef(\sl, { |out, gate=1, buf, sig, slices=16, slice=0, freq = 261.6255653006, amp=0.1| var myenv, env, start, len, basefreq = 60.midicps, rate; rate = freq / basefreq; len = BufFrames.kr(buf); start = (len / slices * slice); myenv = Env.asr(attackTime: 0.01, sustainLevel: 1, releaseTime: 0.1); sig = PlayBuf.ar(2, buf, BufRateScale.kr(buf) * rate, startPos: start); env = EnvGen.kr(myenv, gate, doneAction: 2); Out.ar(out, sig * env * amp) }).add; t = TempoClock(140/60).permanent_(true); u = TempoClock(140/60 * 2/3).permanent_(true); Pbindef.defaultQuant_(4); Pdefn.defaultQuant_(4); ) ( ~paths = [ "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/bar.aiff", // 0 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/c02ambience.aiff", // 1 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/cafe.aiff", // 2 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/co2.aiff", // 3 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/corner.aiff", // 4 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/lane.aiff", // 5 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/seatingbank.aiff", // 5 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/space.aiff", // 6 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/stage.aiff", // 7 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/stairs1.aiff", // 8 "/Users/jsimon/Music/SuperCollider Recordings/stereoglasgow/stairs2.aiff" // 9 ] ) ~thebuf = Buffer.read(s, ~paths[7]); ~thebuf.play // Pbindef(\x, \instrument, \sl, \buf, ~thebuf, \slices, 64) Pbindef(\x).play(t) Pbindef(\x, \slice, 0) Pbindef(\x, \slice, 64.rand) Pbindef(\x, \slice, Pwhite(0,63,inf)) Pbindef(\x, \legato, 1/4) Pbindef(\x, \dur, 1/4) Pbindef(\x, \note, Pwhite(0,12,inf)) // Pbindef(\y, \instrument, \sl, \buf, ~thebuf, \slices, 64) Pbindef(\y).play(u) Pbindef(\y, \slice, 0) Pbindef(\y, \slice, 64.rand) Pbindef(\y, \legato, 4) Pbindef(\y, \dur, 1/2) Pbindef(\y, \note, Pwhite(-12,12,inf)) t.sched(t.timeToNextBeat(4), {u.sync(120/60, 10)});`
