+++
title = "Tons of Bug Fixes | Krita Weekly #3"
date = 2019-11-11T18:33:19+05:30
tags = ["krita", "foss", "open-source", "kde"]
categories = ["krita-weekly"]

+++

The number of bug reports have rose from 18 to 33 this week, out if which my magnetic lasso is guilty of a couple. I promise I will take care of them as soon as I get rid of the university exams which are coming up. Thanks to our awesome development team and the volunteers, the bug count has dropped on the contrary. Last week we managed to get rid of 42 bugs, a net decrease of 9 bugs, yay.

![ bug graph ](/img/kw3.png)

Most of the bugs were taken care of by Dmitry, I can't exactly get the number, cause a lot patches have been pushed but to note some of them,

- Random crashes while converting color spaces

- Undo of image colorspace conversion

- Data-loss in Transform Tool

- Slowdown in Warp Transform Tool

- Visibility of Reference Layer and Global Selection Mask in the Timeline

- Crash when opening image with a Clone Layer and Instant Preview active

- Color profile when loading image with non-default profiles

Other than a lot of feature and UX updates related to color spaces, altogether with making undo available for things like the assign profile action. Also the "Show Decorations" option has been removed from Transfrom tool for now.

Though we already got a notarized build for OSX, it was interesting to see that using the native file dialog for saving would fail silently, fortunately Ivan has taken care of that already.

Other than that, Wolthera has been busy working on the resource management for 4.3 release. Seems like she has been working on UI mostly. Tiar was busy implementing of loading abr brushes as resources in Krita. Along with the resource management stuff, Boud has also taken some time to add a couple of layouts for the multiple window setups.

That would be for this week, `:wq` for now. Don't hesitate to drop a message to any of the social media handles you can see below, if you have any questions.