+++
title = "Somewhat Usable"
date = 2019-07-22T11:42:29+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

Adding a feature by yourself is a lot satisfying than requesting someone to add that for you, cause now you are both the producer and the consumer. But to be honest, I never thought I would be the one implementing the Magnetic Lasso for Krita when I requested it 4 years back, leave the fact that I even getting paid for doing so. So here are the first tests being done on it.

{{< youtube GnvnKdCWGzo >}}

<br>

Took me a couple of months to reach that stage, can't help, not the smartest one in the room, anyway it works. I can complete a selection by pressing return, cancel one by pressing escape and remove points by undo-ing. It almost sticks to the edges, but still needs some fine-tuning. I guess, I need to adjust the coefficients, I use in the formula and also the checkpoint procedure which places the anchor points. Now I am curious what Photoshop does in the back, right now the frequency-based procedure kind of works, but not that great. My next deliverable is to have a panel to adjust those coefficients, so I guess, I should have that first, to fine-tune the algorithm more.

See you next time, `:wq` for now.