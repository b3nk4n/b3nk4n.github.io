---
title: 9 Reasons Why Microsoft Should Revise the Action Center
author:
  name: Benjamin Sautermeister
categories: [Feedback, Windows]
tags: [windows, windows phone, uwp, action center]
pin: false
---

One of the best new features of Windows 10 is the introduction of the Action Center. It centralizes the most important
information of any app in just one place, is easy to access and also provides shortcuts to important settings.
In consequence, a feature in such a central position should be very well tested, right? Unfortunately, 
after spending a lot of time working with the Action Center,
especially with the API during the development of [Action Note](https://www.microsoft.com/store/apps/9NBLGGH6C03H?ocid=badge), it turns out to be kind of premature.
That’s why I wanted to collect all these issues, UI glitches and bugs in a list.
Hopefully this is contributing to improve the Action Center in the (hopefully) near future. So, here we go…

### 1. Input field of an adaptive tile can lead to a graphical glitch

**Affected platforms:** Windows 10

**Description:** The new adaptive tiles of Windows 10 are really awesome. But whenever a text input field is used,
the Action Center’s UI changes the font's foreground color for whatever reason.

![Action Center Glitch](/assets/img/posts/2015/multi-line-glitch-empty.png){: .shadow }
_Multi-line input in Action Center with unexpectedly inverted font color_

### 2. The input field’s cursor of an adaptive tile is obviously misplaced

**Affected platforms:** Windows 10

**Description:** It’s a small thing, but very obvious and just ugly. The cursor of an input field is misplaced
and shifted to the top left. I’m not sure why it has not been fixed since the release of Windows 10,
because it is so obvious.

![Action Center Cursor](/assets/img/posts/2015/misplaced-cursor.png){: .shadow }
_Misplaced cursor in Action Center_

### 3. An expanded toast sometimes collapses unexpectedly

**Affected platforms:** Windows 10

**Description:** When you expand a toast notification to access the hidden content, either just the full text
or even buttons or text input fields in case of an advanced adaptive toast, the toast sometimes collapses
immediately after expanding it or trying to click on a button or setting the focus on the text input field.
That tiny bug harms the usability a lot.

### 4. Input field’s placeholder text of an adaptive tile does not support line wrapping on every platform

**Affected platforms:** Windows 10 Mobile

**Description:** I am not sure if it’s a bug on Windows 10 Mobile or on the PC Version. But in my point of view,
all platforms should behave the same at least. While Windows 10 for PC/Tablet supports line wrapping for
the placeholder text (by using `\r`), this is **not** possible on Windows 10 Mobile.

![Action Center Cursor](/assets/img/posts/2015/multi-line-placeholder.png){: .shadow }
_Multi-line placeholder in Action Center_

### 5. Input field’s line wrap of an adaptive tile differs on both platforms

**Affected platforms:** Both Windows 10 and Mobile

**Description:** Again, this is a very minor issue, but I think all platforms should behave the same.
When a user enters a text that contains an ENTER to perform a line wrap, on Windows 10 Mobile `\r` is used,
while Windows 10 uses `\r\n`.

### 6. The toast history change type in a background task is always “Removed” and never “Cleared”, even when the user clears all notes

**Affected platforms:** Both Windows 10 and Mobile

**Description:** An app can register a background task to detect user manipulations on its toast messages in the Action Center.
And the `ToastHistoryChangedType` (see [docs](https://msdn.microsoft.com/EN-US/library/windows/apps/windows.ui.notifications.toasthistorychangedtype.aspx))
should tell us which kind of change it was. But currently it looks like it is not possible to distinguish whether the user just
removed a single toast message or all of them. Either by using the _“Clear all”_ button or my swiping the title to the right.

**Status:** Microsoft already commented on that in my [MSDN thread](https://social.msdn.microsoft.com/Forums/windowsapps/de-DE/ca1c3504-af74-4d22-931e-8d3ca7c8c151/toasthistorychangedtype-is-always-removed-when-doing-changed-in-the-action-center?forum=wpdevelop).
They confirmed the issue and are going to fix it.

![Action Center Cursor](/assets/img/posts/2015/action-center-clear.png){: .shadow }
_Clearing all notes in Action Center_

### 7. The removal of a toast notification does not tell the background task which toast ID was removed

**Affected platforms:** Both Windows 10 and Mobile

**Description:** This is clearly not bug, but I think a missing functionality of the API.
When you app is launched by a toast notification or a live tile, the API provides methods to identify
the notifications by which the app was launched. But when you want to detect which notification was removed
in a background task, there is no supported method provided by `ToastNotificationHistoryChangedTriggerDetail`
(see [docs](https://msdn.microsoft.com/EN-US/library/windows/apps/windows.ui.notifications.toastnotificationhistorychangedtriggerdetail.aspx)).
Currently you have to do an unnecessary workaround and save a list of all notification that have been pushed by the application,
as well as perform a diff with the currently shown notifications. A lot of horrible clutter code…

### 8. When a new toast notification is pushed using the property SuppressPopup = true, following changes to toast in the Action Center can have an unexpected behavior

**Affected platforms:** Both Windows 10 and Mobile

**Description:** When replacing a toast using tag/group, if you use `SuppressPopup` (see [docs](https://msdn.microsoft.com/en-us/library/windows.ui.notifications.toastnotification.suppresspopup.aspx)) on the new toast,
the toast will fail to be updated until you reboot the computer. And if you pop a subsequent toast without SuppressPopup,
it will appear as a new toast due to the previous broken `SuppressPopup` toast.

**Status:** Microsoft already commented on that in my [MSDN thread](https://social.msdn.microsoft.com/Forums/windowsapps/de-DE/d81a23bc-3c7d-4436-9f0f-7752694ea641/toastnotificationsuppresspopup-varies-behaviour-of-showing-toast-messages?forum=wpdevelop).
They confirmed the issue and are going to fix it. They also proposed a workaround, which could be sufficient for you.

### 9. Toast notifications cannot be muted

**Affected platforms:** Windows 10 Mobile

**Description:** There are several ways to make a toast notification silent when it is pushed to the Action Center.
First, the developer can set `silent=true` in the `<audio>` tag of the adaptive toast. As an alternative,
the developer could set “src=no_sound.wav”, so just reference an empty audio file. Secondly, the user is also able
the set or mute the sound of a toast notification for each app in the setting. Unfortunately, this is not properly working.
Because when the user has opened the Action Center on his mobile device, the default sound is played nevertheless.
This is pretty annoying in case of my latest app [Action Note](https://www.microsoft.com/store/apps/9NBLGGH6C03H?ocid=badge),
especially in combination with issue number 8 above and the suggested workaround of Microsoft. Think about the following scenario:
Our app shows 5 Notifications and we want to update the bottom one. Because we currently cannot just update it,
we have to recreate all notifications. When the user just having a look at the Action Center,
it follows that the sound is played 5 times in a row. My app Action Note currently has to recreate all notifications
every time the user creates a new note. And creating a note in the Action Center means that the Action Center
is always visible to the user. You can image the consequence when the user has about 10 notes in his list.
Sounds like a Jackpot in Las Vegas. Pretty annoying, right?

Have you found even more issues of the Action Center? Awesome! Wait … that was probably the wrong word. I’m quite sure I forgot something. Just in case you know even more, please write them down in the comments section. Thanks!