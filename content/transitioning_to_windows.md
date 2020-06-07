+++
title = "Transitioning to Windows"
date = 2020-06-07T20:08:19+05:30
tags = ["open-source", "terminal", "powershell", "microsoft"]
categories = ["windows"]
+++

So, recently I started using windows for work. Why? There are a couple of reasons, one that I needed to use [MSVC](https://en.wikipedia.org/wiki/Microsoft_Visual_C%2B%2B), that is the Microsoft Visual C++ toolchain and the other being, I wasn't quite comfortable to ifdef stuff for making it work on [GCC](https://en.wikipedia.org/wiki/GNU_Compiler_Collection) aka, the GNU counterpart of MSVC.

All in all, the change wasn't a cakewalk, a part of which I can attribute to the fact that Windows does a lot of stuff in its own way which is just the opposite of the POSIX way. Though it was much better than what I expected, thanks to some all-new developer tools introduced by Microsoft. For now, most of them are still in an early phase, there is a start at least.

Installing Windows was the same as every time, easy process but taking a lot of time. And as always the first thing one does after installing Windows is to get a new browser, which I too did but not like the previous times. Previously I use to download Chrome or Firefox, whichever I was using in Linux. This time I downloaded neither of them. Instead of downloading the other browsers, went online and updated the Edge browser, since the new Microsoft Edge uses [Blink](https://en.wikipedia.org/wiki/Blink_(browser_engine)) browser engine, the same which is used by Chrome, Chromium, and a multitude of modern browsers. The UX has felt a bit better than the other Blink based browsers specifically the part where you can sort your downloads by type of the file downloaded.

![Download Page of Microsoft Edge](/img/edge_download.png)

Next stop, getting my development environment up and running. And similar to every other developer coming from a POSIX background, it is time to get a functional shell that aids instead of being a pain in the posterior. But before even getting a usable shell, we need a usable terminal emulator. And thanks to Microsoft, we have the Windows Terminal, miles ahead of the vanilla command prompt. Though, it is still far behind something like [Konsole](https://konsole.kde.org/), cause it sports the UX of [GNOME terminal](https://en.wikipedia.org/wiki/GNOME_Terminal), sadly. I don't know what is problem in having a proper title bar in GUI applications these days.

Eclipsing that, we have a new problem, Windows doesn't have a _proper_ Bash shell, what a bummer. Well, it comes with Powershell 6 preinstalled which is not bad, but just like the browser, it is a bit dated and needs to be manually updated to Powershell 7. Being open-source, as well as a part of the most popular desktop OS on the planet helped it a lot. While Powershell has a set of problems of its own, there are solutions that help to mend it to a place. The first one being, [PSReadLine](https://github.com/PowerShell/PSReadLine), and with the following commands, it feels more like home.

```powershell
Set-PSReadLineOption -EditMode Emacs
Set-PSReadlineKeyHandler -Key Tab -Function Complete
```
One of them gets the shortcuts like `Ctrl + a`, `Ctrl + e`, `Ctrl + w`, and the other makes the tab autocomplete function like the one in Bash. Woohoo, but wait what is the use of the terminal here in windows? We don't get any package manager or git here. Actually, we do, Microsoft has been working on a new package manager called [winget](https://github.com/microsoft/winget-cli) which looks like a ripoff of [appget](https://keivan.io/the-day-appget-died/), fortunately, we can talk about how Microsoft is screwing open source projects in some other posts but not today.

Nonetheless, it is still early considering it was announced just a few weeks back so I instead used [Chocolately](https://chocolatey.org/), a pretty solid package manager for Windows. And just like the Linux package managers, it needs administrative privileges to performs actions but Windows doesn't have `sudo`. So the first step was to install [gsudo](https://github.com/gerardog/gsudo), followed by `git`.

We have `git` now, * me plays the victory music *. Time to pimp the shell to the extreme. For assistance, we need a couple more modules, one is [posh-git](https://github.com/dahlbyk/posh-git) and the other being [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh). The first module enables tab completion for `git` and also, adds some info regarding the repository in the prompt and another is just the Powershell counterpart of `oh-my-zsh`.

Also coming from plasma and being a fan of the Breeze color scheme, I downloaded the same from [here](https://atomcorp.github.io/themes/). Boom, the terminal looks like this now, slick isn't it.

![Windows Terminal](/img/windows_terminal.png)

And here is my complete profile, a small one for now,

```powershell
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Avit
Set-PSReadLineOption -EditMode Emacs
Set-PSReadlineKeyHandler -Key Tab -Function Complete
```
###### Note: Avit is the `oh-my-posh` theme.

Oh, I also started playing with [PowerToys](https://github.com/microsoft/PowerToys) which includes a lot of power utilities for Windows but just like other stuff, it is still beta-quality substance, although promising.

That's all for today, see yall later, `:wq`. And FYI, I have installed vim in windows too, didn't pimp it to an extreme yet for now.