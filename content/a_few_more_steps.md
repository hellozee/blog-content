+++
title = "A few more steps"
date = 2019-07-18T09:01:28+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

Honestly, working on correcting the checkpoint procedure made the tool explode. So I decided to take a couple of steps back and rethink the strategy. And for inspiration, I fired up YouTube and started watching tutorials of Photoshop's Magnetic Lasso, cause that was the one which made me write this thing in the first place. Which, made me aware of some facts related to it,

- The anchor points are placed if there is a certain variation in the straightness of the edge
- The frequency decides the threshold of the variation and not after how many points an anchor will be placed
- There is a sub procedure inside it, cause the edge is not calculated from the anchors
- It checks the last best possible edge point and confirms the selection up to that point
- And proceeds to calculate the edge from that point until it finds another point like it

Well, those were some really cool observations and fortunately I have implemented all of them except that variance thing, seems complicated. I would keep it as an extended goal for now, cause the tool still works pretty nice even without it.

On top of that after a little bit of debugging, taking almost a day of mine, found out that, the Laplacian of Gaussian algorithm had an offset over the original image, the result gravitated towards the deeper sides of the edge. After a little chat with Dmitry, he confirms that we are using the wrong output of the algorithm. So if I consider that fixed, I might be able to put up a video or GIF showing the tool in action in the coming week.

See you next week, `:wq` for now, :)