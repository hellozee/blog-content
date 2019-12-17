+++
title = "Magnetic Lasso for Krita is here"
date = 2019-08-17T16:27:27+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

I won't say that I am done with Magnetic Lasso now, but the results are a lot better now to be honest. Take a look at one of the tests that I did,

{{< youtube nhT3cbzBpOk >}}

<br>

Looks pretty cool right? But there is a little bit of offset between the selection and the edge, which on the first thought, made me think of writing a better filter such as the Canny Filter for a better approximation. To my surprise, Dmitry added some magic code to the LoG filter and countered the offset. Of course, he wrote the filter, knows far better than me how the thing works. And this is the current state of the tool.

{{< youtube VA3pRSm4HxQ >}}

<br>

Looks fine, but it still has many places where we need to add some bits to make it more complete,

- `Ctrl + Z` to undo the last point is kind of broken, cause the tool undoes the last stroke instead of undoing the last point during a selection. It is possible to make it work, though the whole selection tool subsystem would require a little bit of refactoring to make it possible, also right now, there are 3 different shortcuts to undo anchors, would have to make them uniform across tools though.
- No auto-scroll available, well, I thought this would be easy as overriding a virtual function, but it seems like, auto-scroll only works when a mouse-button is pressed, so this would again fall in the refactoring job.
- Compress mouse signals, right now for every mouse move event, it tries to guess an edge, this is technically useless if you move your mouse too fast, then it would be wise to ignore the events in the middle, saving a lot of computation.
- Caching of pre-filtering, we pre filter the image for initial guess at the edges, for now, it happens when you switch to the magnetic lasso or change the radius of the kernel in the tool options. If the image is big, it might take a lot of time to pre-filter the image. Caching the results and do filtering only when requested would surely improve the speed of the tool.
- We of course need some better cursors for the tool, right now, it doesn't look bad but at the same time it is not good looking as the one PS has, ehhhh.
- Last one, sometime ago I thought I have to write a new edge detection filter, but since Dmitry patched his filter for the tool, I don't think, I would need to write a new one for it in the near future. Though, would definitely try it out once I am done with all of the above.