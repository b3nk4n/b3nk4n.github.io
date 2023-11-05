---
title: Retrospective on 6 Years of Windows App Development
author:
  name: Benjamin Kan
categories: [Projects, Analytics]
tags: [windows, windows phone, downloads, review, history]
pin: true
---

This article is a follow-up on previous posts about reaching individual milestones on my journey
as an _Indie Window App Developer_:

- [100k Downloads in Windows Phone Store](/posts/100k-downloads-windows-store/) --- 05/2013
- [250k Downloads in Windows Phone Store](/posts/250k-downloads-windows-store/) --- 10/2013
- [500k Downloads in Windows Phone Store](/posts/500k-downloads-windows-store/) --- 09/2014
- [1 Million Downloads in Windows App Store](/posts/one-million-downloads-windows-store/) --- 05/2015

## Intro

About 5 years have passed in the meantime after I submitted my last update to any of my Windows 10 (Mobile) apps.
This is more or less right after I finished my Masters degree. My focus simply shifted towards other things,
such as work, other side projects such as games for Android using [LibGDX](https://libgdx.com/).
Or even non-professional things such as hiking, reading criminal novels --- _I really ♥ books from [Jo Nesbø](https://en.wikipedia.org/wiki/Jo_Nesb%C3%B8)_ ---
or last but not least spending quality time with my wife and friends.

Anyways, a lot happened in the meantime. And I'm not talking about the pandemic or the war in Ukraine. I'm referring to much less
important things such as the fact that [Microsoft ended support for Windows 10 Mobile](https://support.microsoft.com/en-us/windows/windows-10-mobile-end-of-support-faq-8c2dd1cf-a571-00f0-0881-bb83926d05c5)
end of 2019. And that was my main target platform as a developer back then. With the exception of [Action Note](https://www.microsoft.com/de-de/p/action-note/9nblggh6c03h?ocid=badge&rtc=1#activetab=pivot:overviewtab),
Windows 8 and later Windows 10 was just secondary.

![Action Note](/assets/img/posts/2022/action-note-teaser.png){: .shadow }
_Action Note with innovative Action Center integration --- launched in late 2015_

To be very honest, after not supporting or updating my apps and game for such a long time, the main reason that triggered
having a closer at them once again is kind of embarrassing: Microsoft started to unpublish one app after the other due to
my inactivity. The following is from Microsoft's report:

> **App Policies:** 10.1.4 App Quality - Active Presence
> 
> **Notes To Developer**
> 
> Apps must have an active presence in the Store. When determining this Microsoft looks for several factors including
> acquisitions rate and update frequency.

Because I'm neither owning a Windows powered smartphone nor laptop anymore, I think it's time to unpublish the majority
of the apps that might not fully work anymore for various reasons, such as changes in 3rd party APIs, changes in the
Windows APIs or policies like the Action Center, etc. I'm sure the most recent app reviews will serve as a very good
heuristic for that.

### Why did I start to develop for Windows Phone?

How did I actually end up developing apps and games for Windows Phone 7, Windows 8 any beyond you might ask? Wasn't it
already said to be without any real chances against Apple's _App Store_ or Google's _Play Store_ dominance?
Well, that's absolutely right. And it was more or less by accident in the end.

Everything kind of started with a mini job as a _Junior .Net Developer_ that I started in 2009. There, I created a first
prototype for the mobile client of a task tracking application called _QuickTask_. Windows Phone 7 was not even publicly
available yet, so the development and debugging of it was purely based on an early version of a Window Phone simulator.
With a little bit of luck and good connections, we have been invited by [Sascha Corti](https://www.linkedin.com/in/saschacorti/?originalSubdomain=ch)
to Microsoft Zurich one day to run our app on an early LG prototype of a Windows Phone 7 device. I still remember how
thick that device was. Very close to a [Nokia 3310](https://en.wikipedia.org/wiki/Nokia_3310). All that clearly influenced me
quite a bit as somebody who did not even yet start his first semester at university.

But I was short on money. And any smartphone has still too expensive for me to even think about buying one.
And it took even more luck before I finally start with my indie dev career. If you can even call that a career? More a hobby?
Anyways, I think somewhen in late 2010 or early 2011, I participated at a conference called
[Microsoft Shape](https://www.netzwoche.ch/news/2014-01-31/shape-konferenz-ganz-im-zeichen-der-apps) in Zürich. And within
each bigger break, there have been quizzes with the audience. Actual exactly three in total. The moderator just dropped
a question into the about 400+ people large audience. And the first one shouting out the right answer got a prize. And guess
what the prizes has been? Exactly, an [LG Optimus 7](https://en.wikipedia.org/wiki/LG_Optimus_7), one of the first
Windows Phone 7 device on the market. And if I remember correctly, such devices have been launched just a few weeks before
that conference. And who was lucky (or smart) enough to walk home with **two** of these WP7 devices? **Me!** ㋡

### The very start of my 2D game dev journey

The rest was then just my pure ambition to put my ideas and things I learned at university, by reading articles or books
into practice. I liked playing video games. And many of the projects in the first semester have been rather boring for me,
because I already had many years of programming experience compared to most of the others. And I felt a little but unchallenged.
Consequently, I started to put most of my time outside of my lectures into my own projects instead. I started to read a book
about [XNA](https://en.wikipedia.org/wiki/Microsoft_XNA), which taught the basics of game development using the example of
a very primitive space shooter. Guided with the book, I implemented it. Then extended it a little bit. And was hooked.
Out of nowhere, I had so many ideas how to extend that game. Different types of weapons and enemies. Particle effects. Creating
my own pixel art. Online leaderboards. Accelerometer controls. I had such a rush of adrenalin, that worked on my project till 8am
in the morning, then went to my lectures and finally took a power nap during the lunch break to recharge. Just a few weeks later,
my first game [SpacepiXX](http://windowsphone.com/s?appId=cbe0dfa7-2879-4c2c-b7c6-3798781fba16) was born.

![SpacepiXX](/assets/img/posts/2022/spacepixx-v1.png){: .shadow }
_First version of SpacepiXX --- launched in April 2011_

The next games [AstropiXX](http://windowsphone.com/s?appId=8ed6a448-5864-4579-ad73-a5efc209760a) and
[VaderpiXX](http://windowsphone.com/s?appId=ee290c98-b70f-4e81-95b8-f8cc4c7947d0) have been reusing 90% of the underlying
code base. Followed by [SpaceScribble](http://windowsphone.com/s?appId=71fc4a5b-de12-4b28-88ec-8ac573ce9708) in which I
experimented with an all-hand-drawn game experience. And it was a huge success. Just a few days after its release, watching
the DevCenter stats like an addict, I was absolutely amazed and could almost not believe it when I've seen a huge spike in the
number of downloads. Far more than 10,000 downloads in just a single day. Without putting a single cent into advertisement.
I knew something must have happened. And a quick Google search could answer that. WPCentral, the most renowned Windows Phone
related website I'm aware of, wrote an extensive and positive article about my game called
[SpaceScribble, Windows Phone space combat the doodle way](https://www.windowscentral.com/spacescribble-windows-phone-space-combat-doodle-way).

![SpaceScribble Review](https://www.windowscentral.com/sites/wpcentral.com/files/styles/xlarge/public/postimages/2014/03/SpaceScribble.jpg){: .shadow }
_SpaceScribble review by WPCentral in March 2014_

### Transition to app development

After diving deep into game development for almost two years, I realized that there was a lot of overhead necessarily with developing
games, such as taking care of all the required graphics, game design and sound effects. The background music always has been
the only thing where I borrowed the help from friends, such as this blasting theme remix used in VaderpiXX by
[QBIG](https://www.youtube.com/watch?v=eNtcPCyutag) who I know since preschool. To have some variety, I decided to develop a
regular app next. Nothing too fancy, but practical. And because the canteen of my university had an Android but no Windows Phone
client yet, I implemented [seeMENSA](http://windowsphone.com/s?appId=8bf87c6a-bf51-4145-b684-8df5c8419ba2) to provide the menu
for any university around Lake Constance.

Next, and during my exchange semester at [WPI](https://www.wpi.edu/) in the US, I wanted to work on a tool to make my own
power napping more convenient. The default clock app in Windows Phone 7.5 was not really convenient, and it took many taps
in order to setup a short 30-minute alarm. When I felt like I could fall into sleep right now for a nap, navigating to the clock
app and setting the timer ripped me out of my napping mood, and it took me too long to get back into it. So, I decided to implement
an app to make setting the napping timer as quick as possible. The idea for
[powernAPP](http://www.windowsphone.com/s?appid=92740dff-b2e1-4813-b08b-c6429df03356) was born. And with the introduction of
[Cortana](https://en.wikipedia.org/wiki/Cortana_(virtual_assistant)) and the hype around voice-controlled apps, I found a way to
set a napping timer without even a single tap: just by using natural language such as _"Power nap for 20 minutes"_ instead.
And was another [hit](https://www.phonearena.com/news/Voice-controlled-powernAPP-for-Windows-Phone-wakes-you-up-when-you-tell-it_id52431).
The feedback by users was overwhelming. At some point, I received about 10 email per week from users that asked for feature
requests or just wanted to share how much they enjoyed my free apps. And on top of that, there have also been hundreds of reviews
in the Windows Store.

Complex apps with lots of functionalities have never been a thing for me. I liked it a lot when an app had a small scope,
but did that thing just right. And tried to apply the same thing to my own apps by focusing on creating small tools for
a specific purpose that made the life of a user at least a tiny bit simpler. One good example for that is
[Photo Marker](http://www.windowsphone.com/s?appid=e3c2905b-f01f-4b3e-a7eb-0f7bcd89cad9), which was later also reviewed
by [Windows Central](https://www.windowscentral.com/photo-marker-windows-phone-app-review). It integrated into the Windows Phone
operating system to easily add annotations to a picture right before sharing it with another app. This was even way **before** _WhatsApp_
added the annotation feature to their app.

![Photo Marker Review](https://www.windowscentral.com/sites/wpcentral.com/files/styles/larger_wm_blw/public/postimages/2014/12/Photo_Marker_Lead.jpg){: .shadow }
_Photo Marker review by Windows Central in December 2014_

### Entering the era of Universal Windows Platform

The last app I want to talk about is [Action Note](https://www.microsoft.com/store/apps/9NBLGGH6C03H?ocid=badge),
which was -- guess what -- also reviewed by Windows Central in a review called
[Note-taking made easy with Action Note for Windows 10 PC and Mobile](https://www.windowscentral.com/action-note-windows-10-app-review).
I found many of the popular note-taking apps to complex and cluttered with features I did not need. And ever since the
Action Center was introduced in Windows 10 Mobile and PC, I was looking for an app which integrates well with it.
After I realized nothing like that exists, I decided to develop it myself. Including cross-device synchronization as a premium
feature. This external [video review](https://www.youtube.com/watch?v=jINEg4EBt8Y) demonstrates is quite well.
And even though it's by far not my most downloaded app, it was in the end the major cash cow with an extraordinary conversion rate.
About **2%** of the users decided to upgrade to the **Pro version** of the app to unlock the cross-device syncing. That's extremely high!
Especially because it was not just a _0.99$_ IAP, but my only every premium feature where I set a high price tag of _3.99$_.

![Action Note Review](https://www.windowscentral.com/sites/wpcentral.com/files/styles/larger_wm_blw/public/field/image/2015/12/ActionNotes_Lead.jpg){: .shadow }
_Action Note review by Windows Central in December 2015_

But users loved it. Not just Action Note. The positive feedback from users and their constructive support was overwhelming.
They asked for **internationalization**, but I did not want to spend money on a translator. So, users started to volunteer to help
me with _i18n_. And ended up with apps that have been available in 19 languages:

- Arabic
- Chinese (Simplified)
- Chinese (Traditional)
- Czech
- Dutch
- English
- French
- German
- Hebrew
- Hungarian
- Italian
- Korean
- Polish
- Portuguese
- Portuguese (Brazil)
- Spanish
- Swedish
- Turkish
- Ukrainian

And because not many apps are available in some of these languages, even popular ones, this gave me just another big boost
thanks to that great community. And with that help, I even managed to have multiple of my apps being listed in the top 20
for multiple weeks. Or took over the pole position from Runtastic as the [best Health & Fitness app](/posts/powernapp-best-rated-health-app/)
in the Windows Phone Store for quite some time, which was more than hilarious.

![App Highlights in Windows Store](/assets/img/posts/2015/wp-app-highlights.png){: .shadow }
_3 of my apps listed in the top 20 highlights of the Windows Phone Store_

## Retrospective

Now, about 5 years after I wrote my last line of C# code, I would like to do a tiny look back into what worked pretty well,
and what I could have done differently.

### The good

- Even though Windows Phone never had a market share bigger than 5% globally, probably not even close, it was still a good
decision to develop for Windows Phone at that time. And I'm very sure I would have never reached such a big audience on iOS
or Android. Simply because on both platforms, it is very hard to get visibility without investing money first.
In contrast, at least in the first years of Windows Phone, every single new app was listed at the very top in the Windows Store
in a special _New Releases_ section. Which immediately generated downloads and visibility from day one.
- The focus on small and simply apps helped me not just to create many of them, but also made it easier to guarantee good
quality, make them easy to use and iterate on feedback quickly.
- Providing apps in various languages had a very good effect to get better visibility in respective markets and finally increase
the number of downloads. 
- Especially as a beginner in the early days, starting with an example such as a tutorial from a book, and then extending it
step by step with your own ideas to an entire tiny product worked very well.
- The [freemium model](https://en.wikipedia.org/wiki/Freemium) is the perfect model for your apps as an indie developer.
Don't bother about even thinking about setting a price tag for your app. Instead, if you have features users might want to
spend money on, use in-app products. Otherwise, users will very likely simply not even download your app. And all your time
and effort was for nothing.
- Keep a close eye on user reviews. Engaging with users via contact form or app store reviews helped to spot bugs,
deliver features or improvements users really cared about. And helped me to keep my motivation on a high level over
many years.
- I can recommend every programming beginner to start with game development. Also for programming lectures at university.
It makes topic much more exciting. In my Bachelors, about 50% of the students didn't make it till the 3rd semester. While
this was on one side due to quite challenging math exams, it was on the other side because many of them gave up with learning to
code. Many of them could not really relate to boring terminal applications which ask for your age, or writing data strucutres such as
lists or sets. I'm pretty sure most of them would not have given up in case we would have started to write simple 2D games
within the first two semesters. And from the topic we learned, they should have been able to do so.
- At least in my point of view, one important skill I learned on this journey is to look at a product from both a technical but still
relatively neutral or unbiased user perspective. I was in direct conversation with customers over many years, and basically acted in
all roles such as Product Manager, Customer Success, Software Engineer and Tester. This skill is something I found very useful in my
professional career. At least I have the feeling that I have a much better sense of good UX, product consistency and spotting bugs
compared to the average Software Engineer.

### The bad

- Localization of your app has positive effects, **but** please wait until you have a stable version with all the major features implemented.
Trust me, if you rely on volunteers to translate your app, then you don't want to end up in a situation where you cannot add new features just
because you are not able anymore to translate it into all the supported languages. This can **slow you down** quite a lot.
- At some point a started to add ads to some of my apps or games. But I regret doing this. At least regular ad banners really destroy the
user experience of your app. But I might be a bit biased here.
- If I could travel back in time, I would have spent more time reading into topics around cross-platform development.
- It is a bit unfortunate that only a minority of my friends could actually use any of my apps, because most of them have been obviously
Android or iOS users. However, I'm still pretty sure that I would not have had such a success on these platforms.


## Analytics

Let's have some fun with numbers together.

### Downloads and ratings

To have a final summary of my downloads, app ratings and reviews, I collected the data from Microsoft Partner Center
and composed the following table.

|  # | App / Game         | Total downloads | ★ Rating [1 -- 5] | User reviews |
|---:|:-------------------|----------------:|------------------:|-------------:|
| 1  | Photo Marker       | 832,556         | 4.4 ★             | 5,575        |
| 2  | powernAPP          | 643,637         | 4.5 ★             | 6,778        |
| 3  | SpaceScribble      | 248,480         | 4.6 ★             | 2,080        |
| 4  | Action Note        | 159,500         | 4.4 ★             | 1,548        |
| 5  | Whip               | 121,263         | 3.9 ★             | 2,116        |
| 6  | AstropiXX          | 104,570         | 3.4 ★             | 382          |
| 7  | SpacepiXX          | 89,299          | 3.8 ★             | 625          |
| 8  | Photo Info         | 79,816          | 4.5 ★             | 1,472        |
| 9  | pocketBRAIN        | 68,201          | 4.5 ★             | 1,808        |
| 10 | Daily Focus        | 27,835          | 3.6 ★             | 134          |
| 11 | ScribbleHunter     | 20,801          | 4.4 ★             | 161          |
| 12 | Pin to Start       | 14,986          | 4.5 ★             | 147          |
| 13 | URI Launcher       | 13,203          | 3.9 ★             | 40           |
| 14 | Frequenzer         | 12,110          | 4.6 ★             | 271          |
| 15 | VaderpiXX          | 8,244           | 3.5 ★             | 33           |
| 16 | Voice Timer        | 4,194           | 4.6 ★             | 114          |
| 17 | Bash0r             | 2,995           | 3.3 ★             | 15           |
| 18 | ScribbleHunter Pro | 2,351           | 4.0 ★             | 17           |
| 19 | seeMENSA           | 2,155           | 4.6 ★             | 73           |
| 20 | iBash0r            | 611             | 4.4 ★             | 23           |
| 21 | German Bash0r      | 609             | 4.7 ★             | 6            |
| 22 | Developer's Diary  | 402             | 4.6 ★             | 9            |
| 23 | PriceChecker       | 244             | 3.7 ★             | 6            |
| 24 | UWPCore            | 5               | -                 | -            |
|    |                    | **2,458,067**   | **4.4** ★         | **23,433**   |

I have to admit, I'm more than surprised that the average rating is still far above 3 ★ even 5 years after I stopped supporting
my apps and games. That being said, there are many 1 ★ reviews within the last years for quite a few apps, because some of them
are not fully functional anymore. As an example, the Action Center API and usage regulations changed, and therefore
Action Note's key feature does not work anymore. But still, its average rating is 4.4 ★, and was previously even very close to
4.8 ★, which is absolutely amazing.

Furthermore, when I started with my first game in 2011, I would have never dreamed of ever getting close to
**about 2.5 million downloads**. And receiving such good reviews by more than 23,000 users.

### Activity since I stopped supporting my apps

After I published my very last app update in early 2017, Microsoft
[announced end of support](https://docs.microsoft.com/en-us/lifecycle/announcements/windows-10-mobile-end-of-support)
for Windows 10 Mobile in December 2018. And finally
[ended its support](https://docs.microsoft.com/en-us/lifecycle/announcements/office-apps-windows-phones-end-of-support)
one year later. I thought it would be interesting to see how this influenced things such as downloads or activity
in the Windows Phone store. This is shown in the following images.

As a first example, I exported the data since around 2016 from Microsoft Partner Center. Unfortunately, no data before
that could be exported.

![Photo Marker Downloads](/assets/img/posts/2022/photo-marker-downloads.png){: .shadow }
_Photo Marker cumulative downloads since 2016_

![Photo Marker Store Activity](/assets/img/posts/2022/photo-marker-store-activity.png){: .shadow }
_Photo Marker store activity since 2016_

Taking Photo Marker as an example, my most popular app regarding total app downloads, you can clearly see that app downloads
started to stagnate in mid 2018. Starting with the announcement for end of support for Windows 10 Mobile, also the store traffic
dropped down to an insignificant amount.

![powernAPP Downloads](/assets/img/posts/2022/powernapp-downloads.png){: .shadow }
_powernAPP cumulative downloads since 2016_

![powernAPP Store Activity](/assets/img/posts/2022/powernapp-store-activity.png){: .shadow }
_powernAPP store activity since 2016_

Secondly, the same picture repeats for powernAPP. With the only difference that the store traffic already converged to zero
about a year earlier. This app was first published in December 2013 and already more than 4 years old at that time.
So no big surprises.

![Action Note Downloads](/assets/img/posts/2022/action-note-downloads.png){: .shadow }
_Action Note cumulative downloads since 2016_

![Action Note Store Activity](/assets/img/posts/2022/action-note-store-activity.png){: .shadow }
_Action Note store activity since 2016_

Finally, let's use Action Note as a second example. This app is availalbe in both Windows 10 Mobile and PC, and therefore
a bit different compared to both apps above. Here we can see that app downloads are still happening. Even though
there does not seem to be any significant store traffic anymore since mid of 2020.

### In-app purchases and premiums

Finally, also a few stats about monetization, listed in the following table.

| App / Game         | IAPs      | Purchase of Pro version |
|:-------------------|----------:|------------------------:|
| Action Note        | 3,111     | -                       |
| Photo Marker       | 2,540     | -                       |
| powernAPP          | 1,766     | -                       |
| Photo Info         | 1,000     | -                       |
| pocketBRAIN        | 601       | -                       |
| Daily Focus        | 257       | -                       |
| Whip               | 66        | -                       |
| ScribbleHunter Pro | -         | 29                      |
|                    | **9,341** | **29**                  |               

Unfortunately, I could not manage to gather the full picture about ad related data, such as impressions, eCPM or revenue.
Microsoft seemed to have moved that from Microsoft Advertising, then to Microsoft PubCenter and finally to Microsoft Partner Center.
However, in neither of them I can find ad network related information anymore.

Last but not least, I want to add that money was never the main driver why I implemented all these apps and games at first place.
It for sure helped me to stay motived, but in the end, I just wanted to bring my ideas into reality and apply whatever I have learned so far.
However, all that money I earned as an alternative to a student job helped me to finish my studies without having to
rely heavily on money from my parents (who still sponsored me to pay half of my rent) or a student loan.
And together with my scholarship, I earned just enough to pay for my tuition, living cost and other hobbies.


## Summary

This this post, I'm closing my chapter of Windows App Development. I kind of did that already 5 years ago, but writing down these
words make it at least official for me. Within the next days, I will probably unpublish the majority of my apps. At least the ones
where the users reported in latest reviews that it is not fully functional anymore. Also, I will move the code for each of them from
my private BitBucket to [my GitHub account](https://github.com/b3nk4n) as public repositories. Maybe the source code of these apps
or games that have been used by millions of users might be helpful for at least somebody.

Thank you for reading this unusually long article!
I hope you enjoyed read as much as I enjoyed writing it.
