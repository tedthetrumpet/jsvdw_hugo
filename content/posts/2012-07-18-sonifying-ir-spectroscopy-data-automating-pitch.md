---
title: "Sonifying IR spectroscopy data - automating pitch"
date: "2012-07-18"
categories: 
  - "news"
---

Going off in a bit of a different direction here, using the data as automation to drive the pitch of a synth:

`( f = CSVFileReader.readInterpret(Document.current.dir.asString++"/water.csv");`

f = ((f.flop\[1\] \* -1) + 1).normalize(48,84); //midinotes

`Pmono( \default, \midinote, Pseq(f, inf), \dur, 0.005).play )`

In this recording, looping up the three chemicals one by one. Kind of cute - early days for this approach.

\[audio src="https://tedthetrumpet.files.wordpress.com/2008/09/pmono01.mp3"\]\[/audio\]

[pmono01.mp3](http://tedthetrumpet.files.wordpress.com/2008/09/pmono01.mp3)
