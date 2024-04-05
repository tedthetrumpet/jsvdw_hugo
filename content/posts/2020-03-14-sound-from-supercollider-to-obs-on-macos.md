---
title: "Sound from SuperCollider to OBS on macOS"
date: "2020-03-14"
categories: 
  - "tech"
---

The principle here is that sound is sent from SuperCollider to the virtual audio driver BlackHole, and from BlackHole to OBS. You then listen to the sound through OBS.

Install [https://github.com/ExistentialAudio/BlackHole](https://github.com/ExistentialAudio/BlackHole)

[![](images/screen-shot-2020-03-14-at-09.42.56.png)](https://tedthetrumpet.files.wordpress.com/2020/03/screen-shot-2020-03-14-at-09.42.56.png)

Set the mac sound output to 'BlackHole 16ch' using the widget in the menu bar:

[![](images/screen-shot-2020-03-14-at-09.43.20.png)](https://tedthetrumpet.files.wordpress.com/2020/03/screen-shot-2020-03-14-at-09.43.20.png)

**Boot or reboot the server in SuperCollider** – this is a key step, the SC server will **not** pick up a change of audio device without a fresh boot or a reboot:

[![](https://tedthetrumpet.files.wordpress.com/2020/03/screen_shot_2020-03-14_at_09_44_52.png?w=246)](https://tedthetrumpet.files.wordpress.com/2020/03/screen_shot_2020-03-14_at_09_44_52.png)

After boot, check that the SC post window says '"BlackHole 16ch" Output Device':

[![](https://tedthetrumpet.files.wordpress.com/2020/03/screen_shot_2020-03-14_at_09_45_19.png?w=300)](https://tedthetrumpet.files.wordpress.com/2020/03/screen_shot_2020-03-14_at_09_45_19.png)

(If you're using Tidal you'll need to run SuperDirt.start here again.)

In OBS, click on 'Settings' and go to the 'Audio' pane. Set 'Mic/Auxillary Audio' to 'BlackHole 16ch' and 'Monitoring Device' to 'Built-in Output':

![Screen_Shot_2020-03-15_at_19_56_47.png](images/screen_shot_2020-03-15_at_19_56_47.png)

In OBS, look for a gear icon for settings in the Audio Mixer panel select 'Advanced Audio Properties':

![Screen_Shot_2020-03-14_at_09_47_41.png](images/screen_shot_2020-03-14_at_09_47_41.png)

Under Audio Monitoring select 'Monitor and Output':

![Screen_Shot_2020-03-15_at_20_06_42.png](images/screen_shot_2020-03-15_at_20_06_42-1.png)

Play a sound in SuperCollider. In OBS, turn up the slider in the Audio Mixer Panel, and you should see the Mic/Aux slider picking up sound:

[![](https://tedthetrumpet.files.wordpress.com/2020/03/screen-shot-2020-03-14-at-09.48.36.png?w=630)](https://tedthetrumpet.files.wordpress.com/2020/03/screen-shot-2020-03-14-at-09.48.36.png)

[![](images/screen-shot-2020-03-14-at-09.48.15.png)](https://tedthetrumpet.files.wordpress.com/2020/03/screen-shot-2020-03-14-at-09.48.15.png)

Sound should now be playing from SC into OBS and through into your speakers/headphones. Adjust volume as usual from the widget in the menu bar.

**Update:** it seems that on macOS 10.15 you may need to go back to the volume widget in the menu bar and select the output you want to hear there. (I can't test this directly, I'm still on 10.13).
