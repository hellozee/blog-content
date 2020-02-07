+++
title = "Krita Weekly #8"
date = 2020-01-07T22:15:59+05:30
tags = ["krita", "foss", "open-source", "kde"]
categories = ["krita-weekly"]
+++

The number of bugs has risen to 457 as it was a vacation season. Also, Dmitry is on parental leave, so the increase is quite normal.

![bug graph](/img/kw8.png)

As Boud is back from vacation, he is sharing his time between, bug fixing & triaging and administration stuff. If you want to lend a hand and do some bug triaging, do head over to the [bug-tracker](https://bugs.kde.org/buglist.cgi?bug_status=UNCONFIRMED&bug_status=CONFIRMED&bug_status=ASSIGNED&bug_status=REOPENED&list_id=1699962&product=krita&query_format=advanced) and try to reproduce the bug.

Tiar fixed some regressions and is planning to fix some bugs this week too since Dmitry is a bit busy now.

Ivan is on updating python 3.8 on OSX. Also, he updated OpenJPEG to be compiled but the plugin does not allow to open jpeg2000 images at all. He would also return to bug fixing and triaging this week.

Unfortunately, Wolthera was busy fighting with the bureaucracy as well as somewhat sick, hopefully, she will get better in the coming days.

Apart from that, we had a lot of fixes from the volunteers, here are some,

- Default to TouchGesture for Kinetic Scrolling in android
- Set the default location for restored files to QStandardPaths::PicturesLocation
- Improve rendering of predefined default rect dab
- Make "Add Subbrush" off on changing multi brush tool's type from copy translate
- Prevent crash on the addition of color to deleted palette with color picker
- Fix PaletteDocker not showing palettes