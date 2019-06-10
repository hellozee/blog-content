+++
title = "Caring about the directories"
date = 2019-01-19T20:05:44+05:30
tags = ["pycon","golang","project","open-source"]
categories = ["pycon","conference","golang"]

+++

The story begins in [PyCon India 2018](https://in.pycon.org/2018/), I, with a tired soul (registration desk is not a quite nice place for resting), shivering in freezing cold, after a dosage of Paracetamol, asked [fhackdroid](https://farhaan.me/) to tell me about any project which uses Go, so that I can also put some patches during devsprint. Unfortunately, he only told me about OpenEBS and I am not a quite big fan of containers, thus spent the devsprint without a single patch, poor me. :tired_face:

After the devsprints were over, the day I was returning to Delhi, I got to know about a [project](https://github.com/dgplug/dexer) for [dgplug](https://in.pycon.org/2018/) on which fhackdroid was working on, know what? That project used Go and believe me, from that date I am still waiting to meet fhackdroid in person. :angry:

Moving on, as I went through the code, it rang to me that, the way the code was written was not the idiomatic go style that you would find in any other upstream project. I decided to mend that up, but before that, I needed to learn about the project, so I created an issue for having a `Makefile`, which would ease the process of development and in a couple of days a corresponding patch taking care of that. As soon as the patch was merged fhackdroid added me as a collaborator for the project. 

Adding me as a collaborator gave me enough liberty to work it my way, though was warned by fhackdroid to not to push anything directly on master, well, rules are meant to be broken right? In the coming week, I moved the code into separate packages of their own, tried to follow a standard layout for the directories, right at that point I understood the importance of having a directory structure, how magically I can maintain code, write tests easily, if I follow a proper directory structure, wow.

Coming on the project, the problem statement was simple enough, needed a service through which we can search through the dpglug summer training logs for any specific keyword about which we are discussing out. Simple enough, fhackdroid already left the heavy lifting to bleve, the file indexer and made an API around it, I just came and added hot reloading and a UI. Thanks to the inertia of hacktoberfest, we also got some outside contributors mainly helping us in writing the Dockerfile, which eventually I overwrote cause it was not working out of sudden. After pushing the project to a [PyDelhi](http://pydelhi.org/) devsprint, I managed to get 2 contributors, one who redid the README and another enabled travis-ci for automatically testing the project.

Though Go is like my second language but this project now made me follow strict directory layouts for even my C++ projects which is apparently still my first language, you can ask me why. And fhackdroid if you are reading this, I did my part, the blog post but you still haven't followed me [Twitter](https://twitter.com/hellozee54) neither recommended me on [Linkedin](https://www.linkedin.com/in/mkuntal/).

Enough of rants, `:wq` for now. :satisfied: