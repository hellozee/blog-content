+++
title = "C++ Rookie tries C#"
date = 2019-12-18T14:54:00+05:30
tags = ["cpp", "csharp", "graphics", "ray-tracer"]
categories = ["languages"]
+++

A little bit background, I am a final year undergrad student, looking for a job, which of course who isn't these days. With that being said, my job search isn't going quite well. I worked on C++/Qt stuff in the last couple of years, most of it is contributing to [Krita](https://krita.org/en/), an open source cross platform digital painting application. As I was looking for job openings in various places as a Tools Developer for graphics pipeline, I found out almost all of them require C# alongside C++, don't know why though. Thus I decided to give C# a try and see how tough it is to get going.

Being a Linux user it was tempting to setup my development environment in Linux itself but we all know C# and Windows go hand in hand. So set up windows in dual boot and installed Visual Studio in no time. And done, it was so easy, in next couple of hours I was able to setup a simple project with tests. This is getting even more easier.

Things went a bit too far when just putting `[Serializable]` was enough to make a class serializable and heck it even supported operator overloading. Coming from C++, I will be honest, a couple of features which are easy generics and operator overloading are enough for making me fall for any statically typed language. The reason being, I love doing math-fu and those features make my life just easier.

And what could be a nice project to try out those stuff other than writing a ray tracer. I have been hovering around the idea of writing one since last year. I first tried to write one in C, without overloaded operators it was really difficult to write and debug the equations. The second time I tried with C++, but then I got tangled in setting up the tests, documentation and all. I don't hate `cmake` but it is not that nice anyway.

Anyway a day in Windows was enough for me. Most of the time, it felt something has rendered me powerless, so was back to Linux. Visual Studio is not there for Linux but thanks to people in JetBrains, I got hold of a copy of Rider, an EAP copy, since that was free to get. I could have renewed my student license and got a stable copy of Rider, but well I am lazy sadly. Nonetheless, Rider seemed even better than Visual Studio.

Though I was unable to setup my NUnit tests on .NET core, it worked fine when I chose .NET framework, no idea what was the reason, but it worked. Had a bit of confusion on how parameters are being passed in C#, I thought, it was like Java. But I was wrong, thanks to [this](https://jonskeet.uk/csharp/parameters.html) awesome explanation for clearing things up for me. Also some shorthand notations like arrow functions really seems cool and save a lot of writing. I would love if someone could take a look at the [bullshit](https://github.com/hellozee/yart/) I have written in the last few days and point out the parts which are wrong.

In the end I would say, C# is a really nice and convinent language. Really easy to pickup thanks to all those tools built around the language and excellent documentation from Microsoft. Although there are couple of but's here. By default it is not as performant as C++, I know ray casting is not something light and I might be missing out a lot of optimizations but ¯\_(ツ)_/¯ . One more but would be, I don't write web apps or mobile apps, I don't see much application of it outside the Windows ecosystem. Though there are high chances that I might be unaware of ways it is being used outside Windows. And there is no WPF for Linux sadly, so right now, it is more of C# or Linux for me. Albeit there is Unity and Godot for game developement in Linux which support C# which I think I could give a try.

`:wq` for now, see you later, :)