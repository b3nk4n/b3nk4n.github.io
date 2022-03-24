---
title: WPI IMGD3000 Technical Game Development Course Inspired by My UnitTest Manager
author:
  name: Benjamin Sautermeister
categories: [University, Abroad]
tags: [university, cpp, project, game dev]
pin: false
---

Today, I received the following email from my Technical Game Development professor at Worcester Polytechnic Institute (WPI)
in the US out of a sudden:

> Hi, Benjamin.  Just a quick note to tell you I've created a Unit Test
> Manager based on the one you started for the IMGD 3000 class last
> year.  I'm looking to encourage students to do basic unit testing as
> they do developments, and the framework you started is nice in its
> simplicity.  I've put up a sample at
> http://dragonfly.wpi.edu/games/index.html and credited you with the
> early version.  Nice work.  Anyway, thought I'd let you know.
> By the activity on your Web page (http://bsautermeister.de/) your
> personal code development projects are coming along nicely!  I've
> just switched to a Windows phone (a Nokia 1020) so tried out
> a few of your apps.  Fun!  Keep up the good work.
> 
> Hope you are doing well.
> 
> sincerely,
> Mark

Background of this email is the following. In a course I visited at WPI, we learned about the fundamentals of developing
a game engine from scratch. I a larger project in scope of 3 months, each student developed a full blown ASCII based
game engine in C++. And with this engine, each smaller team of two then had to develop and present a game.
You can check out videos and results of that course on the official [IMGD 3000](https://dragonfly.wpi.edu/games/index.html)
website. Our game called [Planetary Defense](https://github.com/b3nk4n/wpi.imgd.planetary-defense) is also available
as a [video on YouTube](https://youtu.be/sDJTdeRDa0A).

Developing using C++ is known to be not the easiest language, as many students struggle with the concept of points.
To make my life a little bit easier, I implemented a small lightweight unit-testing framework in C++ next to it, so that
I could easily test the more complex things, such as the scene graph or other data structures we had to implement from scratch.
We have not been allowed to use any third party library beside [ncurses](https://en.wikipedia.org/wiki/Ncurses)
for the ASCII rendering, so I had to get creative. But in the end, using a close to TDD style of development helped me to
find tiny bugs quick and resolve them efficiently. And all this payed out a lot. In the end, I was the only student who
could finish the entire engine without any of the extra features left out.
Any my professor [Mark Claypool](https://web.cs.wpi.edu/~claypool/) was more than impressed.

Now, he seems to have liked the idea so much that he made it part of this book and course. Based on my `UnitTestManager`,
he now provids a small [UTM framework](http://dragonfly.wpi.edu/games/utm/utm.zip) to his students to use.
And generally encourages to do unit testing right from the beginning.

I'm happy, that my ideas contribute to make this really great and fun course even better.
