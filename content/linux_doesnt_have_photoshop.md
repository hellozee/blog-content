+++
title = "Linux doesnt have Photoshop"
date = 2019-12-28T21:12:14+05:30
tags = ["photoshop","krita","kde", "linux"]
categories = ["rant"]
+++
> Linux doesn't have Photoshop.

One common rant I get to hear when I try to help someone to switch to Linux. It is almost 2020 and say what? people still agree with this statement. Of course, they are right, cause Adobe didn't port Photoshop to Linux. But are we as open-source software developers so incompetent that we can't even put together an image editing solution that people can look up to? Let's try to dig that a little bit.

A little bit of disclaimer first, I have been associated with Krita Development for the last year or so, nothing much just a volunteer developer who drops a random patch every now and then. So the post is obviously all about Krita and how it differs from the so-called "industry standard".

I started using Photoshop when I was in High School and obviously it was a pirated copy. Used to do little catalogs and textual illustrations for the art gallery of the school. After a couple of years of usage I switched to Linux, tried out GIMP for a while and Krita but at that moment I didn't like any of them. I was using the same pirated copy over wine. As far as I remember it worked better than the Windows version at the time, though had a bunch of quirks of its own too. Fast forward by the time I was leaving school, I was more of a developer than a designer. And as a developer, I tried to make my own Photoshop which I later ditched and decided to hack on Krita instead.

In the last year, I have come across a lot of complaints regarding Krita. For which I didn't have the answers at that time. So I will try to answer some of them here now.

#### Why don't you folks copy the PS's interface, it would be much better, you know right?

Krita doesn't actually have the same UX as Photoshop so, copying that is impossible. Krita offers many more options when it comes to creating stuff from scratch and a UI like Photoshop would just hide a lot of stuff. If you have any suggestion, please feel free to open an issue on the bug tracker and discuss with the developers.

#### Krita is so unstable, it just crashes, I just can't use it, shitty software.

You know right, Krita doesn't have a budget like Adobe to do thorough testing. So please report a bug on the bug tracker. If you take a look at the [team](http://savage.si/) which makes Procreate, they have 17 employees. 17 people for a digital painting app that is available for a single platform. Now imagine how underpowered Krita team is, considering there are only 5 paid developers and Krita is available for Windows, Mac, Linux & now even Android.

#### Krita doesn't work with my tablet, bad Krita.

There is a lot of possibilities, try checking the FAQs. If still after applying the suggestions it does not work, it is just a bad tablet manufacturer. Krita adheres to the standard APIs provided by the Operating System. Unfortunately, your tablet manufacturer is a stupid one, who just checked whether the tablet works with Photoshop or not to save costs.

#### The text tool is horrible, how could you even ship it?

Yes, all of us know the text tool is horrible but at least it is a bit better than the last one which was just pure shit. I am trying to look into it, but at the moment, I am just going through the `SVG2` text specification and trying some experiments so I won't promise anything.

#### That is such a basic thing how can they miss it, the developers are idiots.

We have a bunch of artists whom we ask before implementing a new feature or altering an existing one. If you still think we are doing wrong, you free to open an issue on the bug tracker and have a discussion, please.

#### There is no clone, smudge, burn, dodge, blur or eraser tool, what a piece of trash, meh.

Ahh, just check the brush presets, Krita's brush engine is so powerful that all of them can be shipped as brushes. By the way, that reminds me, how Adobe copied our `Erase` mode into Photoshop, lol.

#### You folks talk about non-destructive editing, but you don't even have smart objects.

Actually, we have them, they are called file layers and for non-destructive transforms use the Transform Masks.

#### Krita has all the bases covered, you only need to add _*these*_ things and I can ditch GIMP/Photoshop.

The feature you are requesting is probably for Photo editing or manipulating images that are currently not in our focus. Though we don't mind accepting patches regarding them. For example, I worked on Magnetic Lasso this summer, which is coming under image manipulation stuff and it did land in the `master`. So you need to do that yourself or need to find someone to do it for you.


There were some more, but I can't remember them at the moment so I would keep them as the content for future posts. Krita has assistants and reference images which Photoshop doesn't have, at least I didn't find one. And as far as I know, it just got the stabilizer last year along with the `Erase` mode for brushes. That mandala brush which they got recently, meh, we had that for years. So definitely Krita offers more when it comes to creating stuff from scratch. On the other hand, Krita also misses a lot of Photoshop features, while most of them aren't relevant for Digital Painting, some are. We would definitely like to have some of them which are related of course. But at the moment the focus is on bug fixing.

On another note I did Krita Weeklies every week and I still do, it is that this is holiday season and 2 of the main developers are spending a little bit of time with their families, so I gave Krita Weeklies a small rest.

Oh, in the post I told everyone to open issues on the bug tracker but most of the people don't find the KDE's Bugzilla instance to be user-friendly. For those folks, we have a brand new discourse forum for the same thing, do pay a visit to the Krita Artists.

**Bugzilla**: https://bugs.kde.org

**Krita Artists**: https://krita-artists.org

You can also drop a message to any of my social media handles below, I would be happy to assist. `:wq` for now.

**P.S:** This post got longer than I imagined, so being lazy, sorry for any typos and mistakes.