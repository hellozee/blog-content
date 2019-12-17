+++
title = "Do it, you may learn something new"
date = "2018-06-05T22:04:56+05:30"
draft = false
tags = ["golang","build system","c++"]
categories = ["projects"]
+++

Frankly speaking Computer Graphics is a subject which is not appreciated by most of students who study Computer Science just like Real Analysis in Mathematics but being a nerd, this were the perfect subjects which could act like stimulant for my neurons. 

It has been about a year that I was trying to understand it, shaders, pipelines, gimbal lock, well I finally made it around New Year's Eve last year (don't judge me now, I am not that friendly anyway). At last I could write a piece of code which could display a cube and be modular at the same time, it was hard to understand OpenGL with concepts of Computer Graphics for the first time. 

Wonderful, that does sound like a happy time but wait as the size of my code grew overtime, it became quite irritating to wait for the program to build for the slightest of change I make to a single file. Well the answer was simple, use a Makefile generator like CMake which had plugins to take care of stuff like that and reduce the build times. 

While I started learning, how to write CMake scripts, from somewhere a thought poked my mind that I should write my own build system, using CMake will be overkill for such thing and immediately my guts be like "Do it you idiot, you may learn something". Enough for motivating me, 😄 .

So what should I have done? 

> Learn how to write CMake scripts. 

What I did? 

> Decided to write a build system of my own for that. 

Fast forward a month, I had a workable prototype ready, which was well, pretty damn slow. It was so slow that I could type the entire command needed to compile my program and compile while my build system was still busy, couple that up with a poorly written parser, it was not something I was proud of.

It was only after the next 2 months that I could use it, it was fast enough for me, it could have been more faster given that `go` has concurrency inbuilt but for now it was adequate for the size of the programs, I wrote.

What I learned from it?

- What is a Lexer?
- What is a Parser?
- About different hashing algorithms

More than that, to write the lexer/parser stuff I dived into go's source code, learning more about the language itself. Even though the lexer was nicer than I thought, the parser is a little rough (still going through the dragon book, :stuck_out_tongue:) and there is neither any concurrency nor any import feature but fear not I am working on it. You can check the source code [here](https://github.com/hellozee/cook).
