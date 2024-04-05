---
title: "That syncing feeling"
date: "2019-12-31"
categories: 
  - "news"
  - "tech"
---

In order to be able to work up sketches for ‘Perang Gagal’ at [ICLC in Limerick](http://iclc.livecodenetwork.org/2020/), I wanted to use Logic to compose demos of the material for the live players that I could then improvise with in SuperCollider. This poses the problem of how to sync the pulse and tempo between the two programmes, which proved annoyingly difficult to accomplish!

Ideally, I would have liked to set the tempo in SuperCollider for Logic to follow. A straightforward way to do this would have been for SC to send MIDI clock and have Logic follow but, annoyingly, Logic does not support slaving to MIDI clock.

[According to the Logic help](https://help.apple.com/logicpro/mac/10.4.7/#/lgcpfffd9371), it should be possible to sync to an audio click from Logic. I couldn’t get this to work, and nobody on the [Logic Users Group](https://logic-users-group.com/threads/sync-to-exernal-audio-click.11048/) seemed to be able to help either.

The eventual solution was less than perfect. I used Logic to send MIDI clock, and had SuperCollider slave to that. This involved using the MIDISyncClock extension from [H. James Harkins](http://www.dewdrop-world.net/display.php?src=sc.md) ddwMIDI quark. Not perfect, but got the job done.

What did work very well indeed was the recently released [Blackhole](https://github.com/ExistentialAudio/BlackHole) tool for passing audio between mac applications. I’d definitely recommend this as a replacement for Soundflower!
