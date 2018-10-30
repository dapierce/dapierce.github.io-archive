---
layout: post
title: "Quick Nostalgia Trips with Retropie"
date: 2018-03-15 12:06:06 -0700
description: Setting up a Raspberry Pi with Retropie and making a fast and easy emulation box.
published: false
---

My newfound fatherhood has been making me appreciate the few and fleeting moments I have to myself. It has also made me very impatient with my favorite pastime, video games.

I have found myself firing up the PS4, waiting for updates to install, waiting for the disc to spin up the intro movie, waiting for my save to load, etc, etc was leading to me playing a moment of a new game, and then immediately shelving it because my child is up again.

Perhaps becoming a father, I have become more nostalgic for some of the things I loved as a kid, noteably Nintendo and SNES games. You can turn those games on and get started within seconds. Although Nintendo has their NES and SNES Classics, there are a lot of games that I care about that do not show up on their "best of" (and mostly first party) selections.

I needed [RetroPie](https://retropie.org.uk/), a Linux image that combines a few programs and scripts devoted to making emulation on the TV simple. After reading about it, I poured through Amazon and picked up about $65 worth of components:
* **Raspberry Pi 3B**
* A **case** with **heat sinks** and a **2.5 amp power supply**
* **32GB SD micro card**

Since I already have too many HDMI cables, and several unused PS3 controllers ([most current and recent gen console controllers are compatible](https://retropie.org.uk/docs/Controller-Configuration/)), I didn't need to buy anything else.

### Building the box

With my tiny Raspberry Pi and accessories arriving in the mail, it was time to put it together! Which is pretty simple, actually--the Raspberry Pi computer is just one piece, and if you have heat sinks that came with it, you just place them on the two chips of matching size. From there, you can put it inside a case of your choosing. I picked a see-through plastic case with some amount of venting at the top to try and keep it cool.

The micro SD card requires setting up on another computer, basically you format it as FAT32 and use a [program to copy the RetroPie image onto it](https://retropie.org.uk/docs/First-Installation/#installation).

The rest of the setup is easy to follow on the [RetroPie Docs](https://retropie.org.uk/docs), but there are some particular things that were not immediately clear that have made my retro game experience fit perfectly into my now extremely busy life.

### Making RetroPie play better

So now I have a little box devoted to old games, how about making playing them as smooth as possible?

#### Wireless vs wired controls

When I started, I was running my Wii U Pro controller using Bluetooth built into the Pi. But I found my inputs were very laggy. Playing Super Mario World was like molasses and jumping had a very noticeable delay for me. So I switched to a USB connection for my PS3 controller and turning off the Pi's Bluetooth pairing. This has been working fantastically, and with my wired PS3 controller, I don't percieve any extra lag.

Reading about people's experiences with wireless, it seems that although the built-in Bluetooth input is a bit spotty on the Pi, connecting a $10-$20 USB Bluetooth adapter seems to solve input lag issues, so I may try that one day.

#### Set Auto save states for starting and ending a game

This is the crux of accomplishing my goal of quick nostalgia trips. I can hop into a game, play a couple minutes, and leave with my progress intact. Playing RPGs minutes at a time is now as simple as choosing the game on the menu, and save points are no longer the bane of my existence.

This can be done using either 
By editing lines 32 and 34 of `/opt/retropie/configs/all/retroarch.cfg`:

```
savestate_auto_save = true
savestate_auto_load = true
```

you will automatically stop and resume your games simply by exiting a game (Select+Start using the default control configuration). This makes the RetroPie the definition of pick up and play, and real life can happen without losing my progress.

### Making RetroPie look better

With the RetroPie playing great, there are a few cosmetic things you can do to make the whole experience come together and pop!

#### Themes

RetroPie has some [great themes](https://retropie.org.uk/docs/Themes/) submitted by users with a variety of styles. There are minimalistic interfaces for a clean HD menu look as well as noisy, colorful themes that are lots of fun.

They can be accessed by first going to the RetroPie configuration screen and selecting "esthemes". This program will allow you to download the themes from the internet, and after they are downloaded, reset the Pi. When Emulation Station loads back up, access the themes in the Main Menu under "UI Settings" and "Theme Set".

My own favorites are:
* **tronkyfran** - has great close-up splash photos for each system.
* **art-book** - minimalistic with a professional design sensibility, on a very large HDTV this one looks understated and classy.
* **Chicuelo** - friendly iOS-esque design, with lovely game/character spash images for each system.
* **snes-mini** - 16 bit pixel asthetic perfected--this is my favorite, but I will admit it might be too colorful and noisy for some people's tastes. It hits me right in the pixel art bone though and is perfect for my mostly SNES-based library!