---
title: Porting Windows 8 Games Using MonoGame
author:
  name: Benjamin Sautermeister
categories: [Software Engineering, Games]
tags: [c#, windows, monogame, game dev]
image:
  src: /assets/img/posts/2013/vaderpixx-banner.jpeg
  width: 1000   # in pixels
  height: 400   # in pixels
  alt: VaderpiXX for Windows PC
pin: false
toc: false
---

You might have heard already of [Mono](https://www.mono-project.com/). It's more or less an open source implementation of
the _.NET Framework_ and allows to bring your apps developed in C# to other platforms. And beside that, there is also
a free implementation of XNA game, called [MonoGame](https://www.monogame.net/), which is a framework for creating powerful
cross-platform games. All my Windows Phone 8 games are based on XNA. And with the power of MonoGame, I believe it might be
worth a try to bring these games to Windows 8 PC.

I honestly just started a few days ago. But so far, I can say that things are working better than expected. It just took me
about 2 hours to have a running version of [VaderpiXX](http://windowsphone.com/s?appId=ee290c98-b70f-4e81-95b8-f8cc4c7947d0)
running on my Windows 8 laptop.

![VaderpiXX with MonoGame](/assets/img/posts/2013/vaderpixx-monogame.jpeg){: .shadow }
_VaderpiXX running with MonoGame on my X220 Windows 8 laptop_

Of course, the devil is in the details. That game was both a touch and accelerometer controlled game. And the latter is
typically not available on most Windows 8 devices. So there are various adjustments of the game required before its ready
to be tested and published.

I also had a quick look into how to port the game to Android or iOS. However, this requires an _Indie_ license of
[Xamarin](https://en.wikipedia.org/wiki/Xamarin) that is unfortunately **not** free.

I'm pretty excited to bring my games to Windows 8. Many of my friends have no Windows Phone, but a Windows 8 PC or laptop.
So this might be the easiest way to enable them to play them, too.