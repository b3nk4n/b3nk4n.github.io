---
title: Automatic Viewport Scaling in Windows 8 Apps Using MonoGame
author:
  name: Benjamin Sautermeister
categories: [Software Engineering, Games]
tags: [csharp, windows, monogame, game dev]
pin: false
toc: false
---

As [posted recently](/posts/porting-games-using-mono-game-windows8), I started to port a few of my games to Windwos 8 using [MonoGame](https://www.monogame.net/).
And I'm slowy getting there to submit my first game to the Window 8 Store. However, I had quite some troubles first regarding
the adjustment of the viewport when changing the screens resolution. And after reading through several forums, it looks like
others have been struggling as well. A few individuals offered alternative forks of MonoGame that have resolved this kind
of problem built-in. Others suggested to create a copy and do some manual changes in [OpenTK](https://opentk.net/), which is an
open source C# wrapper for OpenGL, OpenAL and OpenCL. However, I decided to not use any manually modified version of any of these
libraries, because otherwise it will be hard upgrade that dependency at some point.

Anyways, I managed to solve that problem at some point. The following snippet shows the most important bits.

```csharp
protected override void Initialize()
{
    graphics.IsFullScreen = true;
    graphics.PreferredBackBufferHeight = 480;
    graphics.PreferredBackBufferWidth = 800;
    // …
    graphics.ApplyChanges();
    ApplicationViewChanged += Game_ApplicationViewChanged;

    this.Window.ClientSizeChanged += Window_ClientSizeChanged;
    handleScreenViewState();
    base.Initialize();
}

void Window_ClientSizeChanged(object sender, EventArgs e)
{
    this.GraphicsDevice.Viewport = new Viewport(0, 0, 800, 480);
    graphics.PreferredBackBufferHeight = 480;
    graphics.PreferredBackBufferWidth = 800;
    graphics.ApplyChanges();
}

void Game_ApplicationViewChanged(object sender, ViewStateChangedEventArgs e)
{
    handleScreenViewState();
}
```

The most important part is the `ClientSizeChanged` callback of the `Window` class. In particular for Windows 8 Desktop games,
also the `ApplicationViewChanged` callback of the `Game` class plays an important role here, because this enabled to react
on chages of the `ViewState`, such as when the app entered _Snapped Mode_.
By explicitly setting the back buffer and applying the changes once again in the `ClientSizeChanged` helps to end up with
the same behavior you might be familiar with in [XNA](https://en.wikipedia.org/wiki/Microsoft_XNA). And the screen scales
automatically when the viewport or screens aspect ratio changed. For whatever reason, _MonoGame_ performs an unexpected change
of the back buffer and the viewport, thus causing the video output to be incorrect. Consquently, **manually resetting the
preferred back buffer and viewport** sizes resolves this problem.