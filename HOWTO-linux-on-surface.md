# HOWTO: Installing Linux (Mint) on an old Surface Go [posted 04.01.2026]

Three small disclaimers before I start:
- I am not a power user/professional. This is the method that worked for me. There may be glaring issues if you know what you're doing, but this worked after repeated headaches
- I have never, ever used Linux before this. THis is why I opted for Mint and chose the MATE edition over Xfce, which would probably be more performance-efficient.
- This is what I would call a "reverse cooking recipe" - meaning you get bullet points of what to do first, and then my life's story afterwards. So if you're only interested in the how-to, read on. If you want a spelled-out story instead, consider reading the second part first 😁

Side note: I am doing this on a Surface Go Gen1 with 8GB RAM and 128 GB storage coming from a Win 11 installation. Keep that in mind for all my comments on performance - also, stuff might be in different places in other versions.

## The Method How-To

0. Ensure that you're able to access your current Windows installation. If you can't (because of a forgotten password etc.), create a Windows boot stick and reinstall Windows from scratch.
1. Ensure that `Device Encryption` (and/or BitLocker) is disabled in Windows. Wait for it to finish decrypting if you have to change this setting.
    - Win 11: `Settings`-> `Privacy & Security` -> `Device Encryption` option
2. Turn off `Secure Boot` in the Surface's UEFI (`Security` -> `Secure Boot`)
    - Power down your Surface, wait a few seconds, and then hold **both the Volume Up and Power button** pressed to open the UEFI.
    - After making this change, you'll see a red lock warning pop up with every Surface start. Don't worry about it.
3. While you're in the UEFI, change the `Boot configuration` so that `USB Storage` has the highest priority.
    - Optional: Check that your Windows still loads after exiting the UEFI with these changes
4. Download the Linux distro/version you want to install. I opted for the MATE edition of [Mint](tab:https://www.linuxmint.com/download.php), which runs fine. Xfce might perform better, but will require more manual tweaking.
5. Create a Linux USB boot stick using [Rufus](tab:https://rufus.ie/).
    - Choose at least a 4GB stick to be safe.
    - In Rufus, make the following change: `Partition scheme` -> Switch to `GPT`
6. Insert your Linux USB stick into your Surface, and power it on. With luck, it will actually load from the stick and allow you to proceed with installing Linux. If not, read on:
7. If it booted you into Windows instead of the USB stick, reboot into the advanced startup options:
    - Win 11: `Settings` -> `System` -> `Recovery` -> `Advanced startup` option
8. In the advanced startup options, choose `Use a device` to look for your USB stick. For me, I had to choose a `Linpus` option to proceed, as the normal USB option did nothing when selected.

That was all I had to do to get into the Mint desktop and start the installation process proper.

## The Life Story

I have been a Windows user for basically forever. Outside of the many (smart)phones I've had - do these even count? - I don't think I ever used a different desktop operating system.  
However, with Windows being Windows in recent times (see Win 8/10/11 and especially [everything that happened in 2025](tab:https://www.windowscentral.com/microsoft/windows-11/2025-has-been-an-awful-year-for-windows-11-with-infuriating-bugs-and-constant-unwanted-features)), I felt it was time to dip my toes into alternative systems. And with Apple being outside of my price range, that only left Linux as the only viable alternative.

However, I didn't want to blindly jump into something that I knew nothing about, especially since Linux has had a reputation in my mind of being mostly for professional programmers and sweaty tryhards that live on the command line. As an avid enjoyer of a good GUI, this made me extremely skeptical of a full switch without at least toying around in a "safer" environment beforehand.  
That is to say nothing of the hundreds and thousands of Linux distros that exist out there, with new ones popping up every second week - and every website and person online having a different opinion of which distro would be "good" or even suitable for normal people. To make a long story short, after some research I stumbled upon [Mint](tab:https://www.linuxmint.com/), which seemed like a decent version for a normal person, while still being relatively lightweight.  

From my experiments as a fledgling university student a decade ago, I still had an old Surface Go (first generation, and genuinely ass) laying around. I would say that it has been gathering dust ever since these first experiments, but I reformatted it as a portable Win 10 writing tool for my girlfriend in late 2022 - so it had only been gathering dust for a bit over three years since she never really used it (this will be important later).  
Anyway, this seemed like the perfect victim for my experiments. After some consulting with ChatGPT, I settled on the medium-load MATE version of Mint for my experiments. While Xfce would have probably been the better choice performance-wise, I wanted to have a more user-friendly experience and avoid the command line as much as possible for the start.

So I followed the installation instructions on the Mint website, created a boot stick using Etcher, inserted it into my Surface, changed the boot priority in the UEFI, turned it on and ... landed in Windows. Huh. That's not what should have happened. Some confused web searching later (is Ducking the equivalent to Googling for DDG or how do we handle that mess?), I stumbled upon the solution: Apparently, Surfaces (and maybe Windows more general) ignore boot sticks if Secure Boot is enabled in the BIOS/UEFI. Well, that's easy to fix. Simply open the UEFI one more time, turn off Secure boot and we should be good to proceed.

Except that, of course, Windows noticed that something changed in the security settings, tried to update BitLocker (since the standard setting of the Surface was to enable device encryption), and then ... Bluescreened. Repeatedly. Every single time.  
Well, that sucks balls. Should be easily fixable though, right? I just need to turn on Secure Boot again. So here goes me trying to time the "keep the power button pressed for 10 seconds to force a shutoff" against the background of "the device bluescreens after roughly 11 seconds trying to re-initialize BitLocker and then instantly reboots", which took longer than I want to admit. After that, simply re-enter the UEFI, re-enable Secure Boot, re-exit, and it still crashes constantly without any way of stopping it.

After some more back-and-forth with ChatGPT, it insisted that just manually powering it off repeatedly triggers an extended startup for system recovery. Fortunately, I have become quite good at timing the 10 seconds. Unfortunately, this did literally nothing. No extended startup, no interruption of the bluescreen loop. THe only thing it gave me was this quote from ChatGPT that lightened my mood more than it had any right to: "On many Surfaces this *forces* recovery, but yours sounds stubborn."

At this point I said "Screw it" and went for the nuclear option: Creating a Windows boot stick, so that I can install a fresh version of Win11 for the sole purpose of turning off device encryption and install Linux. I even have a USB stick lying around I can use. Granted, I'd have to re-make the Linux boot stick afterwards, but I have time. Except that this is a 4 gig stick, and Windows apparently needs at least 8 gigs of space (for comparison, the final Mint stick needs 3 gigs). One rummaging through a drawer of mostly-smaller-than-8-gigs USB sticks and a long load time for Windows to create a boot stick later (seriously, what are they doing that takes so long?), I was set and ready to go.  
And apparently, Surfaces have a physical option to force boots from USB sticks by holding `Volume down` + `Power` pressed at startup. SO I gave it a whirl with the Windows stick (worked flawlessly) and thought to myself "Why am I doing all this? If there is a 'Force USB' key, I can simply take my Mint stick and skip everything!" - except that this force only works for the Windows stick, and not the Linux stick 🙄

Anyway, Windows 11 installed from boot stick - Side Note: 1st Gen Surface Go is not built to handle Win11, it runs like garbage and navigating the installer is a pain on several levels - device encryption turned off, secure boot turned off, no bluescreens this time, and finally ready to install Linux for real this time. Except that my Mint boot stick still isn't recognized...

At this point I did the only sensible option and called a good friend and professional Linux user to suffer with me. After breaking his brain with the occurrences of the last three hours (!), his first advice was to re-check the USB stick by making it using Rufus instead of Etcher.  
One would think that with professional help, the installation would run without issues. One would be wrong, because Rufus cannot handle the current Linux Mint version (22.2), as the Syslinux version used by it (6.04/20240408) is newer than the one Rufus supports (6.04/pre1). I thought nothing of it and downloaded Mint 22.0 instead to see if that fixes things, only to be told by Rufus that this version was retracted due to security concerns - in a message that basically read "Are you sure you want to install malware?" Ominous.

After some Googling on his part (I have no idea what his search engine is, so no funny verb here), we found out that the proper way to do things is to switch the `Partition scheme` option from the default to `GPT`, after which the stick was created without issues.  
Well, apart from the small problem that the Surface still didn't want it. Not with changed boot options, not with the Power + Vol down trick (which he also found online, so ChatGPT probably hadn't made that up). After some head-scratching, we remembered that advanced startup can be forced from inside Windows, and we tried that to see if it even lists the USB stick. To no one's surprise, a) it did list the stick in the available options, and b) selection that option did absolutely nothing and booted us back into Windows.  
However, there was another external USB stick listed that none of us recognized - not via the UEFI, but instead via something called "Linpus" which neither of us have ever heard of. Reading through the [Wikipedia article](tab:https://en.wikipedia.org/wiki/Linpus_Linux), it seem that we can add 1st Gen Surface Gos to the list of devices that come with it pre-installed.

As none of us had ever heard of this Linpus thing and the available information sounded more like malware than an actual useful program, we were skeptical - with my friend even proclaiming to uninstall everything and move into the forest if this works - but it's not like we had anything to lose or more options left.  
As a surprise to everyone involved (we had a few more friends as bemused onlookers), this option worked instantly and without issues, so now I have a Surface Go with Mint ready to be used 😊

As far as performance on the Surface Go 1 is concerned - it seems fine so far? After a bit of toying around, it feels like most normal stuff runs pretty okay on it. I'll maybe switch to a more lightweight internet browser, as default Firefox does eat a good chunk of resources and take some time to start - but that was also a problem under Windows.  
Outside of that, time will tell how much I'll actually use this device going forward. Maybe it'll continue gathering dust, the same way it has for most of the last decade. I have different priorities than worrying about device usage rates anyway. A very good friend of mine will leave society and live the rest of his life in the woods, and I have to mentally prepare for both saying goodbye to him and living with the guilt of forcing this on him for the rest of my civilized and comfortable life ...