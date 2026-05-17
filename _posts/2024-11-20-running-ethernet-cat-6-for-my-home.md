---
title: "Running Ethernet (CAT 6) for My Home Network"
date: 2024-11-20 03:28:00 +0000
tags:
  - "Home Network"
  - "Networking"
---

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/01.jpeg)
Running Ethernet (CAT 6) in my house is a project I had wanted to do since moving in. Several years later, I finally got it done. Why did I choose to do it in July in Florida? Wireless, even with multiple APs and Ubiquiti gear, wasn't getting near the gigabit speed I expected from our ISP and I had had enough of it. And there really isn't anything that compares to a hardwired connection.

I hadn't planned on turning this endeavor into a blog post at the time, so I don't have pictures every step of the way. But ultimately, I wanted to share this in case anyone is thinking of doing something similar in their house.

## Supplies

On the face of it, you wouldn't think there would be much needed to run some CAT 6 through a house. Maybe the cable and a ladder to get into the attic (or crawlspace if you have one). Breaking down each step of it though, the number of supplies start to add up:

- CAT 6 cabling (I got a 500ft pull box).

- Make sure to READ what you are buying. At the very least, ensure that the cable is pure copper and is UL certified. Do not buy copper clad aluminum for this type of work despite it being cheaper.

- Respirator / masks
- Keystone jacks for the walls
- Wall plates
- Low voltage mounting brackets to hold the wall plates in place
- Either a drywall saw or box cutter to cut into the drywall (I prefer the latter for more precise cuts, though it takes longer)
- Punch-down tool for use on the keystone jacks
- Cable stripper
- Snips or very sharp scissors for cutting the CAT 6 cable.
- Ethernet jacks (depending on how you are terminating)

- I had an immense amount of difficulty using traditional Ethernet jacks when terminating my cables. I chose not to use a traditional patch-panel, and instead use RJ45 couplers which allow connecting two terminated ends to connect to each other.
- I had no idea that PASS THROUGH RJ45 connectors existed -- once I got these they made terminating so much easier. Note though that a special crimper is also needed when using these.

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/02.png)
## Preparations

Before starting any drilling, pulling, or cutting, my first step was to inspect the attic. If you aren't familiar with Florida style attics, they look like this:

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/03.jpeg)
I made sure I could access every part of the attic I would need in order to run CAT 6 to the desired rooms. This is no small task at 6'2" walking on ceiling joists and through trusses. I'm sure for people that do this every day it's no problem -- for me, I just didn't want to fall through the ceiling.

Once I established I could get everywhere, back on the ground I ran the length of cable I would need from my telecom box to the desired rooms. This gives a decent estimation of how much cable you'll need to pull through the attic. Just make sure to include some cable to account for the walls that the cable will be going down (and of course you want to have a little extra just in case).

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/04.jpeg)
![](/assets/img/posts/running-ethernet-cat-6-for-my-home/05.jpeg)
While in the attic, it may be a good time to establish where you plan drill and where you want the Ethernet jacks in the desired rooms. I used a stud finder and painter's tape to mark where each stud was located. Then, as I was in the attic, my wife and I yelled to one another (she would be in the room) to establish which space between the studs I was closest to in the attic. Once that was established, I'd know where to drill in the attic.

If it's not clear -- the goal here is to avoid drilling first, running cable down the wall, and then cutting into the wall, just to discover that the cable is not in that section of wall. Then you have to patch the wall and cut a hole in the correct area of the wall.

There was no exact science to this method, and there's probably a better way. This worked well for us though and all my prior experience was in commercial settings with drop-ceilings where this really wasn't a problem.

Doing this also enabled me to realize that the places I originally wanted to run Ethernet were not going to be possible. There were obstructions in the attic that just weren't going to allow me to get where I needed to be for those spots in the drywall. Ultimately, I needed to move several feet from where I first planned.

## Execution

First I ran the pre-measured and pre-cut CAT 6 cable up through the attic to the predetermined spots I was going to drill.

After that, there wasn't much to do but start drilling. How big of a hole to drill depends mostly on the number of cables you plan to run and of course the size of the ceiling joist. In my case, I only ran two cables per drop. I used a 3/4" spade similar to the one below, but I think I would have needed to go larger if dropping any additional cables.

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/06.png)
Once the cables were dropped through the hole, it was finally time to get down from the attic.

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/07.jpeg)
I crossed my fingers that we had determined the correct area between studs in the wall and cut out a hole for the low voltage mounting bracket. These come with guides on how to most easily cut the proper dimensions for installation and are overall very easy to work with. This was probably the easiest step of the project.

With much relief, the cables were there and were pulled through. On to punching down the CAT 6 to the keystone jacks.

This was also something that I hadn't done in years and threw me for a loop at first. Some of the instructions that keystone jacks provide are better than others, and the ones I purchased did not clearly label the punch-down order. If you're not sure what I'm referring to, this is an example:

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/08.jpg)
While this is not the same keystone I used, the diagram is similar enough. It took me some Googling and trial-and-error to determine what the diagram was saying for the correct layout of the [T568B standard](https://www.flukenetworks.com/knowledge-base/application-or-standards-articles-copper/differences-between-wiring-codes-t568a-vs). Don't mix A and B standards or the communications simply won't work across the wire.

After getting everything punched down, the cover plates went on and the keystones were inserted. At least one end of the terminations was complete! Below is what it looks like installed and with Ethernet cables connected to the new ports. Just as if the ports and wall plate were always there.

![](/assets/img/posts/running-ethernet-cat-6-for-my-home/09.jpeg)
The other end of the termination came at the telecom box I mentioned earlier. If you're planning to terminate to a traditional Ethernet connector, I will reiterate my support for pass-through RJ45 connectors. The pass-through connectors still weren't easy, but in my eyes, they allowed the project to continue where the traditional RJ45 connectors simply were not allowing for successful termination. This very well may have been due to the RJ45 connectors I had on hand.

## Summary

While it was frustrating at times, this is definitely a project that was well worth the effort. I wish I had done it sooner. Wireless has come a long way and can be excellent, but nothing beats a hardwired connection. This project noticeably improved latency on video calls and games, made downloads and uploads multiple times faster than before, and overall improved my work and personal network experience.

Next time though, I'll wait for winter. 🙂