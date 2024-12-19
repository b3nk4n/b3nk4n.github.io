---
title: Speed Up Your Windows Phone App
author: bsautermeister
categories: [Software Engineering, Windows]
tags: [windows, windows phone, performance]
pin: false
---

You have a Windows Phone app and are not happy about its **performance**? Well, I had this feeling with a few
of my apps recently. But don't worry. There are a few simple tweaks you could do to gain significant improvements.

### Fast app switching

Each Windows Phone app can be in a differnt state based on the app's
[lifecycle](https://social.technet.microsoft.com/wiki/contents/articles/27613.windows-phone-application-life-cycle-windows-phone.aspx).
When the user quits your app or switches to another one, it will either end up in the _dormant_ or _tombstoned_ state. While the first
one means the apps data is still in main memory, the latter one however causes the app to be destroyed to make space for other apps.
Consequently, when an app resumes in _dormant_ state then there is **no need** to reload data from `IsolatedStorage`, the web or similar.
All that data is still available. That's the reason why this technique is called
[fast application switching](https://lnluis.wordpress.com/2011/09/25/fast-application-switching-in-windows-phone/), as it reduces the
loading time when switching between apps. And it's implementation is rather either, because all you need to do is to check the
`Activated` event of your application whether the `e.IsApplicationStatePreserved` property is set.

```csharp
if (e.IsApplicationInstancePreserved)
{
    // data is still in memory
}
else
{
    // TODO: load data here...
}
```

More details about this is available in the
[MSDN blog](http://blogs.msdn.com/b/abhinaba/archive/2011/10/24/windows-phone-mango-under-the-hood-of-fast-application-switch.aspx).


### Fast app resume

You might know this feature from popular apps such as _WhatsApp_ or _Facebook_. You quit an app from a sub page,
but the user ends up on the same page when you start the app once again from the launcher. While this is honestly something that
might be only interesting for more complex apps with many different pages, it is worth mentioning that this is quite easy to
implement. In a nutshell, all you need to do is to edit the `WMAppManifest.xml`{: .filepath } and adjust the _page stack_.
You can find further implementation details in the
[Windows Phone Developer Blog](http://blogs.windows.com/windows_phone/b/wpdev/archive/2013/09/19/windows-phone-fast-app-resume.aspx).

### Loaded vs NavigatedTo event

In the past, I was always a bit puzzled whether it is better to load the apps data in the `Loaded` or the `NavigatedTo` event.
When looking at examples in the web, it seems that most developers did not think about this too much.
This is probably no general rule, but I noticed it can be worth it to load data in the `NavigatedTo` event.

First of all, it is imporatant to know that the `NavigatedTo` event is fired **before** `Loaded`. The latter one is fired after
all control elements have been loaded. And due to the fact that most apps use page transition animations when switching from one
page to another, it can make a significant difference when you already start to load data asynchronously while the animation
is in progress. This has the effect that users perceive your app to respond faster.

### Further optimization techniques

There are of course many other techniques to optimize your apps performance, such as lazy loading or caching.
I can recommend that you look at your app's performance from a critical perspective. Or even better ask a good friend to be
less technically biased. And based on that feedback, think about ways to improve that performance. Is there manybe anything
that could be done in parallel that is currently done in sequence? Are you loading the same data again and again?
Trust me, your users will appreciate that.