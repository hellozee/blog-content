+++
title = "C++ daily #1: Compilers"
date = 2019-06-16T16:44:49+05:30
draft = true
tags = ["cpp","compiler", "cpp-daily"]
categories = ["cpp-daily"]

+++

On some recent outings, I found there is a lot more to explore, than I initially thought, so I would love to take apart them one by one, understanding more about them, also improving my documentation reading skills.

Compilers seem to be an interesting topic to start with, notably cause I am tired of seeing this screen every time a sit for a practical exam in the lab,

![Turbo C++](/img/tc.png)

Ahh, that hurts, I am not sure what make Indian students and teachers use this terrible thing, lack of knowledge? resistance to change? I don't know. What does wikipedia say about this?

- Last release: September 2006, that is almost 13 years now
- Only available for Windows
- Ugly IDE, meh, 'nuff said

So what are the alternatives? There are fortunately some nice compilers out there, some 'em are,

- Intel C++ Compiler
- Microsoft Visual C++ Compiler
- GCC
- Clang

### Intel C++ Compiler

It's about page says, it produces code which is more optimized for Intel processors and probably that is only selling point for it, other than it being available for Windows, OSX, Linux and Android. But being a proprietary and specialized I am yet to try it out, probably I can get the SDK for free with my student account. Anyway not worth the effort, I am yet to attain the power of writing optimized code, using it won't reap any benefits for me.

### Microsoft's Visual C++ Compiler

This one is, kind of big player in the world of compilers, only available for windows. Well, of course changing ABIs on every other major release doesn't sound good, but hey they are doing it and still is used by a lot of people. It earlier came separately but now only comes along with that mighty Visual Studio, thats so lame move from Microsoft. Anyway again, I haven't used that thing much apart from some lab classes in college which has an optical fiber backbone where I can download this shit, just tested a couple of my program whether they can go cross platform or not. Ohh and another point the Wikipedia page says it only partially supports C++17.

### GCC

The GNU Compiler Collection's C++ frontend, one of the oldest in the game and the most popular one too.