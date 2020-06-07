+++
title = "Krita Weekly #5"
date = 2019-11-26T09:11:28+05:30
tags = ["krita", "foss", "open-source", "kde"]
categories = ["krita-weekly"]

+++

This week we got 13 new bug reports while 22 got fixed, a net decrease of 9 bugs. The bug tracker says that there are about 415 bugs remaining, so still a long way to go. And last week the 4.2.8 beta was released. Thanks to all the folks who participated in testing it. You can expect the 4.2.8 release this Wednesday.

![the bug graph](/img/kw5.png)

If we take a look at the commit history, Dmitry can be seen busy fixing bugs as usual. There were a lot of new changes introduced but to mention some of them: the constness in KisLocklessStack got fixed, crashes when moving a layer under a transformation mask as well and KisDecorationsWrapperLayer was made to set up default bounds correctly.

Ivan fixed some inconsistency in the visuals of the line endings. And coming to the resource rewrite, Boud has been working on to make document storage work like bundles. Tiar has been busy with tagging, a working combobox can be found in the corresponding branch to filter resources. And Wolthera has been dabbing with the storage widget ui. Collectively they also fixed some missing parts of the API involved with the resources. 

Also thank you Carl for helping us to setup a funding platform for Krita similar to that of Blender. Here is an early preview of what he is into.

![ screenshot of the fund website ](/img/fund.png)

`:wq` for now, see you next week, and don't hesitate to drop a message in any of the social media links below, if you have anything related to Krita, :slightly_smiling_face:.