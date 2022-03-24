---
title: Bug in ComboBox of UWP Apps when using Custom Styles
author:
  name: Benjamin Sautermeister
categories: [Software Engineering]
tags: [windows phone, uwp, csharp, bug]
pin: false
toc: false
---

I'm investigating a weird issue for some of my app users since a while already, which I'm not able to reproduce on my PC,
Surface tablet or Lumia phones. However, in the reviews of my [Action Note](https://www.microsoft.com/store/apps/9NBLGGH6C03H)
app, I can read that some users seem to have troubles to open the settings page. First, I thought these are wrong reports.
But after reading it a couple of times from different users made me thinking. And at least after I received the first bug
report via Email, I realized this requires a closer look. After some detailed analysis I could figure out that these crashes
must be related to the `<ComboBox />` control. But I could not find anything useful that could help to resolve this problem.

After even more problem analysis, debugging and testing, I could finally narrow down that the root cause of the problem:
**Custom Styles** used in context of a ComboBox. It even does not matter how this style is defined. Even using the generated
default style from [Microsoft Blend](https://en.wikipedia.org/wiki/Microsoft_Blend) ends up with the same effect. Consequently,
there seem to be only two options left:
a.

<ol type="a">
  <li>Use a ComboBox without any Custom Style</li>
  <li>Use a completely different control</li>
</ol>

Furthermore, I could figure out the following:
- The problem does not seem to appear on Windows 10 **Mobile** devices
- Only a few users on Windows 10 PC are affected
- It seems only PC users are affected that installed Windows 10 via update, instead of doing a clean installation

Consequently, the use of `<ComboBox />` in a Windows 10 UWP app requires attantion at the moment, as it can very unexpectedly
cause instability. More details and progress of resolving this issue can be followed in my
[thread in MSDN](https://social.msdn.microsoft.com/Forums/de-DE/ca755a6e-e3ee-4e65-a018-960b08a10fda/uwp-application-error-in-windowsuixamldll-comboboxselecteditem-?forum=wpdevelop).

**Edit:**
It looks like I was indeed looking into some sort of nasty bug deep down in the Universal Windows Platform:

> @Benjamin Sautermeister,
>
> It's really nice that you post the research result to here. I've purposed your answer since I think it will also be good for other customers who meet the same problem.
> 
> Best regards,
> Barry