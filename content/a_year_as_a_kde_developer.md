+++
title = "A year as a KDE developer | The KUnity Setup"
date = 2020-02-11T17:25:45+05:30
tags = ["kde", "krita", "open-source"]
categories = ["open-source"]
+++
It has been more than a year that I had push rights for all the KDE repositories. So this is an obligatory anniversary post.

I got introduced to Linux while searching for development environments that came with all sorts of compilers & interpreters by default and I don't have to manually install those stuff. It was 2012 as far as I remember, Ubuntu 12.04 just came out and it was the first solution suggested by the search engines. Though the unavailability of a proper internet connection meant, that I had to wait a couple more years when one of my friends downloaded a copy of Ubuntu 14.04 for me.

That's all and nice, but where does KDE come into the picture? After trying out Ubuntu 14.04, I decided to give Kubuntu 14.04 a try and honestly I didn't like it. I did give plasma another try when I started using CentOS, as it was the recommended distro for using Autodesk's and The Foundry's tools, though GPU woes sent me back to Ubuntu.

How I got introduced to Krita, I don't know but what I liked about it was the striking similarity of it with Photoshop UI. Though later I was disappointed a bit since one of my favorite tools aka the Magnetic Lasso wasn't in there but GIMP had one. I did ask about it in the [forum](https://forum.kde.org/viewtopic.php?f=156&t=126095#p333692), probably the first feature request I did for any program.

After Krita's 4.0 release, I became interested in it again, why? Since right before that there was a Kickstarter that promised a better text tool with SVG support. Though I found it a bit disappointing. I mean come on, no on canvas editing? no control over kerning? why? who does that? That was the point where I decided, seems like they don't even care about the text tool, let's see how tough it is to fix it. And boy it is tough. I did get a [patch](https://phabricator.kde.org/D10202) to allow me to adjust the letter spacing, but Boud forgot to change the author while commiting and since I eventually gave up working on the other aspects of kerning, the branch was never merged and I vanished from the scene.

Three quarters of the year passed and owing to some _realisations_, I decided to start hacking back on Krita. But I was smarter this time, picked up a task marked as Junior Job worked on it. The task was supposed to be easy as remarked by Dmitry but ended up being not easy. I had to do multiple patches for having the feature eventually merged.

Still, I am not sure, why I was given the [push rights](https://twitter.com/hellozee54/status/1087052525532921856) after the first commit. The official article about this mentions at least 2 or 3 patches and the bar is even higher for a project like Krita. Consequently and surprisingly, I was invited to the [sprints](https://www.hellozee.dev/krita_sprint_2019/), wow, this is getting special now.

Though I wanted to work on the text tool I ended up working on the [magnetic lasso](https://www.hellozee.dev/to_be_merged_in_master/), last summer, given the fact I was new to the codebase and text tool was not a rookie's walk in a park. I am still figuring out how to _fix_ the text tool, if you have something to share, do poke me [here](https://github.com/hellozee/qt-libraqm-test).

All of these but why?


>Hello,
>
>i just came across your blog articles about the upcoming magnetic lasso tool in krita. I can't tell you how much i look forward to use it. I'm using krita for photo retouching and composing (switched to krita after a decade using gimp!).
So this is definatively a feature that will help me a lot!!!
>
>.
>
>.
>
>.

For such E-Mails which just make your day, :3

Also, the fact being a KDE dev helped me realize how slick Plasma is. And since I am a Unity fanboy, I adjusted Plasma to mock Unity desktop of Ubuntu. Have a look.

![](/img/plasma1.png)
Latte Panels with [this](https://store.kde.org/p/1274975/) Global Menu.

![](/img/plasma2.png)
Disabled the window decorations on maximized by adding `BorderlessMaximizedWindows=true` under `[Windows]` in `~/.config/kwinrc` and added window buttons in the panel with [this](https://store.kde.org/p/1272871/) plasmoid.

![](/img/plasma3.png)
Super awesome [plasma-hud](https://github.com/Zren/plasma-hud) which is using rofi, would be cool if this feature can be added to krunner.

![](/img/plasma4.png)
And of course the [simple menu](https://store.kde.org/p/1169537/), so elegant, I hope the menu can stick to edges in the future. I wonder if I can hack Simple-Menu to include a hud and of course position those categories in the bottom.

`:wq` for now.