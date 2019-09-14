+++
title = "Finding the Edge"
date = 2019-09-08T17:12:20+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

Three months of fighting with `boost`, `qt`, having a proper plan, multiple individuals to get help from and still unable to hit the target in time. That will be software engineering 101 for me.

To be honest, I didn't expect my algorithm to become that slow, when I started formulating the plan, but it was and still is, the difference is, now I know the places where it can be optimized. Continuing about my algorithm, people seem to get bored when I start talking about it. With confused faces over the term "convolving" and depressed over "derivative". 

**Note:** If you are not able to understand, what I am talking about, take a look at the last 12 or 13 blog posts for the context.

So making you both depressed and confused, here is LoG or Laplacian of Gaussian filter or Marr filter. Why is it depressing? cause it calculates the second-order spatial derivative of an image and why is it confusing? it does that with the help of a convolution filter. I would leave the explaining of all the math behind it to [this](https://homepages.inf.ed.ac.uk/rbf/HIPR2/log.htm) page and cutting to the main part, we were using it for getting an idea of the pixels which have a high chance of being on edge.

Well, to be honest, when I talk about such things, some people be like, hey you can just use OpenCV and get it done, it shouldn't take more than a week. But no. One thing common among those folks is they mostly work in a quirky language whose quirks force them to use OpenCV, a language which makes feel^W someone specially-abled.

The first month was spent particularly fighting with `boost`, hush, please someone tell them to update their documentation site, I have tried, but well they probably need some hearing aid. The filter was already there, done for me, so didn't have to waste time on that. And I learned about abstracting a real-world object into a data structure, credits goes to the flexibility boost provided. I am really impressed.

Month 2, was mostly spent learning the existing tool infrastructure and how can I hack mine into it. And understanding a 20-year-old codebase is not fun. Every time you get something to work, the next day you find out, you cant move ahead this way, cause the core functionality for this is not built into the infrastructure. And to hack in that functionality we have to refactor, literally all the classes which use that code. Though had something to present by the end.

Final month was somewhat getting it to the usable state. The feedback loop was fast, since everyone was on-site, thanks to the amazing sprint we had in Deventer, Netherlands. It was only in the last week that, I found out, that, umm, I have to discard almost 2 months of work of mine, not completely but well, discarding anything you have put your efforts into is always going to be tough. Though this time I am more aware of the quirks of the codebase was able to change the whole user experience inside a week. Now it is probably going to take another month or two, to get that into master.

And what you read was not a GSoC report, it is just me trying to keep up my post frequency, haven't done much this week, busy fighting with the bureaucracy. Ohh, talking about GSoC, I recently wrote a post for cracking GSoC, do give that a read. I really feel ashamed sometimes when I see, students crying over a T-Shirt, Google referrals cause on the top of that, almost all of them belong to my own country. Over the last couple of years, I have learned one thing, that is, don't be overambitious, be happy with what you get, persistence is the key, if you are persistent you will surely be rewarded.

That will be enough for today, `:wq` for now.

