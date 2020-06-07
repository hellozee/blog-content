+++
title = "It is coming alive"
date = 2019-07-11T06:25:42+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

After digging for around a month and a half, I can finally do some selections with the Magnetic Lasso tool, which I wrote with utter laziness as I would say. Though it still demands a lot of work to be done, so it will be just polishing the existing code into perfection for the next one and half month.

### What did I do?

- Implemented a checkpoint based edge calculation, obviously if you know the edge points from A to B and you need to find out the edge points between A to C, you don't need to recalculate the whole thing, saving a lot of computation.
- Filtering and copying happens while initializing, so the tool would definitely be slow to start on bigger canvases, but once that is done, there is no such drop in performance.
- And yes, we can complete the selection by clicking on the starting point and use them.

### What is left to be done?

- Paint the checkpoints while making the selection, honestly I already tried to do it, probably missed something.
- Delete checkpoints on right click, this also seems trivial to implement, but yet to try, so no idea what kind of challenge it would be.
- Working on the algorithm, one thing I notice was the accuracy got down as soon as I started copying the stuff, need to take a look at it.
- An options dialog to mess with the parameters.

And as boud says, I got to add some spaces to the code. :laughing:

That should be enough for the week, `:wq` for now.