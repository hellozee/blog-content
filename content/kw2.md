+++
title = "JPEG 2K, Auto Precision | Krita Weekly #2"
date = 2019-11-04T13:46:10+05:30
tags = ["krita", "foss", "open-source", "kde"]
categories = ["krita-weekly"]

+++

This week in Krita has been more around features, rather than bug fixing. We had around 18 bug reports but at the same time 18 bugs were fixed too. 

![](/img/kw2.png)

We can now import jpeg2000 files into Krita. The support for jpeg2000 was removed from Krita a while back due to bugs in openjpeg and people often confused it with the regular jpg. If you are confused do give [this](https://en.wikipedia.org/wiki/JPEG_2000) a read. Now the next step is to support jpeg2000 exports.

The Android build also gained a usability fix, it has a back button to come out of the full screen mode.

Meanwhile Dmitry has been busy in rewriting the Auto Precision option in the brush setting. He basically substituted the old implementation with simpler heuristics.

- If brush size is below 30px, full precision is used.
- If brush has a texture, scatter, mirror, rotation or airbrush option, then subpixel precision is disabled.

Ivan was able to obtain a Apple developer account and subsequently was able build a notarized version of Krita for OSX. 

Other than those, webp exports have a quality setting and if you are using the text tool, recently used fonts are automatically pinned to top.

As the 4.3 release is approaching, Boud, Wolthera and Tiar are working hard on rewriting the resource management, this week too, they put a lot of work. In between that Tiar also made the file dialog to handle the file extensions more gracefully.

On top of everything, folks from the Krita community have kickstarted a discourse forum geared towards helping Krita users. Do check out [Krita Artists](https://krita-artists.org/). `:wq` for now, until next post.