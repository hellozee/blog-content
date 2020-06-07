+++
title = "Krita Weekly #4"
date = 2019-11-19T21:22:14+05:30
tags = ["krita", "foss", "open-source", "kde"]
categories = ["krita-weekly"]

+++

Phew, I am late this week for the update, kudos to my university exams nevertheless better be late than never. One more week passed, we are now closing on the 4.2.8 release. This week too we can see a steady decrease in the number of bugs. 17 bugs were reported and 23 were fixed, a net decrease of 6 bugs. The rate has gone down a little bit compared to the previous month, cause the folks are now mostly focusing on the resource rewrite.

![ the bug graph ](/img/kw4.png)

Dmitry like always is busy fixing bugs and if I can read the commit history correctly then,

- Fix saving non-srgb color profiles into PNG

- Fix brush rendering on low-precision levels (1 and 2)

- Fix transforming layers that have Onion Skins enabled

- Fix color space of onion skins cache device

- Fix undo of replacing vector selection

- Fix outline in Move Tool, when a layer has a Transform Mask

Though this is not all of it, he also fixed some random stuff happening while cloning. Thanks to Ivan, export dialog preferences would be saved from now on, also he is working on bugs related to the filters.

Just like the previous two weeks, Boud, Wolthera, and Tiar are neck-deep into resource rewrite. Wolthera can be seen working with the brush resources and Tiar with the tagging system. Tiar also worked upon having Adobe Style Libraries as a resource. Apart from working on the resource rewrite, Boud is busy preparing for the 2.8 release, expect a beta release tomorrow.

That's all for this week, `:wq` for now, :)

P.S: Since my University exams are coming up, I might not be that frequent till mid-December, at least.