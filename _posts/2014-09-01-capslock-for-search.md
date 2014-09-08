---
layout: post
title: Using Caps Lock for Windows 8 search
category: articles
comments: true
tags: productivity
---

Since upgrading to Windows 8, I've found that even with [Classic Shell](http://classicshell.net), I'm using the Windows 8 search function in pretty much every situation I would access the Start Menu.

Before Classic Shell, I was triggering the search by pressing the Windows key, then typing on the Start tile screen. However, I found it too distracting.

A much less distracting search is the one triggered by pressing `Windows + S`; it slides in from the side. However, it's also a fiddly key combination. It would be much easier if I could map a unused key on my keyboard specifically to that; something like Caps Lock.

I did some investigation into the best way to remap it, and I couldn't seem to find anything on how to change the Search trigger from `Windows + S` in the registry. I looked into [scancode remapping](http://www.experts-exchange.com/OS/Microsoft_Operating_Systems/Windows/A_2155-Keyboard-Remapping-CAPSLOCK-to-Ctrl-and-Beyond.html), however while I have seen Windows 8 laptops with a dedicated search key, it doesn't appear it is mapped to a scancode.

# The Solution
It seems like the best approach was to develop an [AutoHotkey](http://autohotkey.com) script for the purpose.

I downloaded, installed, and opened AHK, choosing Yes to create the "sample script". After some testing, to get what I wanted I needed to remove the sample code and add;

{% highlight autohotkey %}
; CapsLock performs search
CapsLock::#s
{% endhighlight%}

instead, then place a shortcut to the script (it's in My Documents) in `%AppData%\Microsoft\Windows\Start Menu\Programs\Startup`. This causes the AutoHotkey script to run at startup, configuring the Caps Lock key to trigger `Windows + S`. 

Another script that I found on the [AutoHotkey foums](http://www.autohotkey.com/board/topic/4554-entering-commands-using-double-tapped-shift/) was repurposed to toggle Caps Lock by double-tapping the Shift key. However, I have turned this off, as my typing style seems to trigger it accidentally: Your mileage may vary.

{% highlight autohotkey %}
; Double-tapping Shift enables CapsLock
Shift::
if (A_PriorHotkey <> "Shift" or A_TimeSincePriorHotkey > 300)
{
   ; Too much time between presses, so this isn't a double-press.
    KeyWait, Shift
    return
}
	if GetKeyState("CapsLock", "T") = 1
	 {
 	  SetCapsLockState, off
	 }
	else if GetKeyState("CapsLock", "F") = 0
	 {
	   SetCapsLockState, on
	 }
return
{% endhighlight %}

While simple, I've found both these scripts to be very useful.