---
title: "Building a RetroPie (2025)"
date: 2025-04-18 01:24:00 +0000
tags:
  - "Linux"
  - "Raspberry Pi"
---

![](/assets/img/posts/building-retropie-2025/01.jpeg)
Several years ago I had heard about the concept of a "RetroPie." A Raspberry Pi loaded with hundreds of classic games that can be connected to custom home builds, arcade systems, or just a normal TV. The idea always interested me as I'm a fan of '80s style arcades, but primarily from the perspective of getting this to work on a computer about the size of a credit card. I recently decided it was time to give it a try.

![](/assets/img/posts/building-retropie-2025/02.jpeg)
I had seen plenty of Raspberry Pi's before -- I knew what they were and generally what they were capable of, but never actually used one. My [Raspberry Pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) actually had better [specs](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/) than I was expecting. Next I needed a case and other supplies to get this ready to be a RetroPie. A list of requirements is supplied on [the RetroPie website](https://retropie.org.uk/docs/First-Installation/).

## Ordering Supplies

![](/assets/img/posts/building-retropie-2025/03.jpeg)
I already had a USB keyboard, a USB flash drive, a USB controller, and an HDMI cable. I needed to order:

- [a case](https://www.amazon.com/dp/B089LHSRLB?ref=ppx_yo2ov_dt_b_fed_asin_title) (I chose one that looks like a NES)
- [a micro SD card](https://www.amazon.com/dp/B09WB3D5GQ?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1) (I went with 256GB)
- [a micro-HDMI to HDMI adapter](https://www.amazon.com/dp/B09LYPXPH6?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1)
- [a micro SD card reader](https://www.amazon.com/dp/B08P517NW5?ref=ppx_yo2ov_dt_b_fed_asin_title)

These have all worked very well for me and are not Amazon affiliate links. That being said, there are a lot of alternatives out there that will also work.

## Installing RetroPie

The first step was to download the latest image available for RetroPie. RetroPie publishes pre-made images on their website - <https://retropie.org.uk/download/>

Next I needed software to flash the SD card. Software I've used before and that was recommended by [a great tutorial video](https://youtu.be/E1sbnPZ_A8w?si=TcPAeFQbKz3s3fHa) is [balenaEtcher](https://etcher.balena.io/).

![](/assets/img/posts/building-retropie-2025/04.png)
They make the process as simple as possible. Insert the SD card into the card reader, select the RetroPie file you downloaded, choose the SD card as your target, and hit Flash!

Once this is done I put the SD card into the RetroPie, connected power, connected the display and my controller, just to find that I had no display on my TV. At this point I was determined to continue, but got a feeling this was going to be harder than I hoped.

Thankfully, I was wrong. The next evening I connected all the peripherals (including display) before connecting the power cord to the RetroPie. I immediately had a working display and the RetroPie OS booted without issue.

At this point I am going to be borrowing screenshots from [that tutorial video](https://youtu.be/E1sbnPZ_A8w?si=V9iWZizQmDt8k58-) I mentioned earlier. Whoever "Herb Fargus" is on YouTube, I very much appreciate them creating that video as it helped a lot in getting this working.

![](/assets/img/posts/building-retropie-2025/05.png)
## Working in RetroPie

Once RetroPie booted, I was presented with a screenshot very similar to this. It successfully detected my controller (a third-party, wired Xbox 360 controller) and prompted me to configure it.

![](/assets/img/posts/building-retropie-2025/06.png)
The configuration process was very simple, though on the latest version of the RetroPie OS looked slightly different than what was shown in that video. It's certainly close enough that you know what to do though.

![](/assets/img/posts/building-retropie-2025/07.png)
Once complete you're brought to the RetroPie main menu for further configuration.

![](/assets/img/posts/building-retropie-2025/08.png)
## Loading Games

The RetroPie does not come loaded with any games. These must be acquired. If you'd like more information, I suggest [/r/Roms](https://www.reddit.com/r/Roms/?rdt=33281) on Reddit.

Once you have some ROMs, the process of loading them is extremely easy.

1. Put a USB flash drive in the RetroPie once it is booted up. A file system will automatically be copied to your flash drive.
2. Remove the flash drive from the RetroPie after several minutes (if your flash drive has an activity light this will help greatly in knowing when the process is done)
3. Insert the flash drive into the computer that has the ROMs.
4. Copy and paste the ROMs (usually in compressed/zipped format) into the appropriately named location on the flash drive. For example, the /retropie/roms/nes folder for NES games.
5. Remove the flash drive and put it back in the RetroPie. The games will automatically be copied to the RetroPie.
6. Restart Emulation Station from within the RetroPie OS or restart the Raspberry Pi.

Your games should now be visible. If not, try uncompressing the files in the process above. I had mixed results -- some games worked fine without, others only appeared after I uncompressed them.

![](/assets/img/posts/building-retropie-2025/09.png)
Notice I said that the games should be visible, not playable. Here too, I've had mixed results. Many of the ROMs I've loaded play just fine. However many simply fail to play despite appearing in the menu. I suspect this could be for a variety of reasons depending on the ROM, emulated system, and more.

Ironically, the type of game I'm having the hardest time playing are the classic arcade games that interested me in the first place. Instead, I'm able to load and play without much issue many Nintendo 64 and other games I didn't even know could be played on a RetroPie when I started this project!

That being said, this will be a growing project and I intend to get as many different systems properly emulated and as many of the classic games working as possible. Some systems require special BIOS to be loaded before they can be emulated properly, some ROMs detect they are being emulated and not on a hardware system and therefore don't play, etc. There is work to be done that will keep me busy for a while to come.

Thankfully, there is a great community of RetroPie enthusiasts across the Internet and I can't be the first to run into some of these problems...right?

But overall, I've had a great experience getting this built and it's running very well with several working games. Even just as a learning project, I definitely recommend it.

## References

Again, I owe a lot of credit to Herb Fargus on YouTube as well as several authors of articles on the RetroPie website and elsewhere. The members of the RetroPie community are greatly appreciated.

- RetroPie - First Installation:  
  <https://retropie.org.uk/docs/First-Installation/>
- A Beginner's Guide to Setting Up RetroPie on a Raspberry Pi:  
  <https://youtu.be/E1sbnPZ_A8w?si=8rl_MbYCl7Ki31Kf>
- RetroPie OS download:  
  <https://retropie.org.uk/download/>
- BalenaEtcher:  
  <https://etcher.balena.io/>
- Reddit - /r/Roms:  
  <https://www.reddit.com/r/Roms/>
- Also see hardware and other links throughout this post.