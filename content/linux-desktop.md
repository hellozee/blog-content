+++
title = "This is the year of Linux Desktop"
date = 2019-05-17T19:46:48+05:30
tags = ["linux","gnome","kde","foss"]
categories = ["linux","open-source"]

+++

The title is a running joke now, please don't hit me, I know that this is one hell of an aloof conclusion. But why? Let's retrospect the situation.

- Linux is just the kernel
- Add a display server on top of it
- Add a window manager
- Add a compositor
- Add a display manager

You will get a desktop, yes a desktop and not a desktop environment. A desktop environment has a lot of stuff stacked onto the above-mentioned stack. If we introduce this many variables, we are bound to get a lot of combinations. And that while gives us a lot of freedom in choosing what we should use, also fragments the user base. It just not fragments the user base but also the number of developers working on those open source projects. I am one of the guys who still use OpenRC when the whole (most of) Linux world has moved to systemd. Say what I am also spoiled by freedom. This fragmentation is likely a major reason why Linux has yet to make a substantial footprint among desktop users.

Now, if we take a look at ChromeOS, we will find, there is a substantial market for it too, even though it is pretty new compared to something like Debian, it has a better footprint then the latter. I know ChromeOS is not exactly a typical Linux distro, but behind the scenes, it is using the Linux kernel right? which means the kernel is not the problem, the problem lies in the fragmented market and more or less hardware (this is 2019 duh).

Taking a step in the other direction, if we take a look at Android, it hard to believe that it is also being powered by the same Linux kernel (though with modifications) and is the only major player in the smartphone market if we ignore iOS for a second.

From those instances we can conclude that if we can unify both of the fragmented user base and developer base, we can at least have a bigger footprint than we have now, less confusion and more users jumping into the bandwagon.

As similar to any other human, I also like to have an opinion on everything and here are they, :stuck_out_tongue_closed_eyes:

#### 1. There are too many distributions

Honestly, this is a pretty easy problem to solve, so how to choose a distribution? There are a couple of factors by which I judge which distribution I should be using, one its release schedule and second the package manager. Nowadays we have snaps, flatpaks, and appimages, so the package manager should be a secondary thing. Talking about the release schedule, we have two kinds of the release schedule, point release and rolling release. So we would like to have a distribution which gives us both of these options, point release for the users who like rock-solid stability and rolling release for users who like to have bleeding edge stuff. The obvious answer would be Debian, given it has one of the largest userbases even after fragmentation, another option could be OpenSUSE but we would be going with what is already popular. So Debian it is.\

#### 2. Wow there are a lot of combinations when it comes to desktop stacks

Currently, we have no option other than Xorg since Wayland is still not yet mature enough to be used by everyone. But I would be vouching for it since if we use Wayland it would simplify the desktop stack by reducing a couple more variables. For what desktop environment we could be running on top Wayland, the choice seems easy to make, GNOME, even though I contribute to KDE, the plasma-shell doesn't make much sense to me. Too many unnecessary options offered, if I want to rice my desktop, I will be doing it by directly editing the configuration files. Talking about the GNOME Shell, it uses GTK3 which looks really nice on GNOME and gives it is own unique touch, with how they use the title bar. With that being said GNOME developers should also take into account to make the other UI toolkits to look good when used in GNOME, something which plasma does pretty well. In the end, the system applications which almost everyone would be using should be written in GTK3, while more specific applications like a Photo Editor, Video Editor or a Word Processor can use any UI toolkit.

Now, some of you might be telling me, GNOME takes a lot of RAM, but does it? If we take a look at Windows desktop, how much RAM does it use? obviously more than GNOME and how much of its user base did it lose by using that much more RAM. In 2019, almost everyone has 4+ gigs of ram and if you don't, please update, cause you can't even use a proper web browser without that much of RAM nowadays.

In my opinion, though GNOME is the best desktop environment, KDE has produced better applications which deal with specific stuff. Like for example, if we take Kdenlive, it is one hell of a video editor, no other FOSS video editor does come closer to the usability and features of what it offers, another would be KDE-connect, an application which connects your android phone to the desktop.

With that, it will be `:wq` for now, and yes it is the year of Linux Desktop. `*hides*`