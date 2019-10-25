+++
title = "One hell of a October"
date = 2019-10-25T20:32:56+05:30
tags = ["krita", "pycon", "twitter"]
categories = ["update"]

+++

October has been really great for me this year. It started with the Ada Lovelace Day meetup, or better, the after meetup party. The following week, my 6 months of effort got merged to master. Then it was just Pycon India. I have already written a lot about them, you can checkout my previous 3 blog posts. So this last week, I was busy setting up the analytics for my blog, cause why not, everyone loves numbers right? 

If you ask anyone about website analytics, their de facto suggestion is to use Google analytics. But lets be honest, you won't like if someone follows and tags you or do you? And just for that fact, I decided to setup a self hosted solution. I had a VPS which was just hosting my quassel server, so I had a lot of spare resources to churn in.

Everything is fine but no matter for how long you have been using linux, writing code, you can never ever configure a linux box in go. To setup my analytics software, which was [Matomo](https://matomo.org/), an open source solution, I needed to have either LAMP or LEMP stack installed and configured, cause Matomo is written in php. I choose to go with LEMP, taking the fact that I had enough share of problems in configuring Apache in the past.

Installing php, easy, installing nginx, peasy, installing MariaDB, hell no. I don't know why they removed prompt which asked for password during the installation. So I basically had to fight for around 3 hours digging into StackOverFlow and after multiple blog posts, I can't seem to remember how I made it work but I did make it work. Then again it was my first time setting up nginx, I had fair share of problems, nothing complicated though, all the answers were there in the page 1 of my search results. Though to be fair, if I had a prompt for setting up the password for MariaDB, it wouldn't have taken me that long to set this up. The only feasible solution for me to get around that problem is to use MySQL community edition from the MySQL repos, cause they ask for the password while installing.

Apart from that, my twitter timeline was filled with `#bcon19` posts, humph, I will go there at least once. Ton had a great keynote, in short, he was proud of where blender has come to and why shouldn't he be? Blender was the one who introduced me to Open Source, kudos to them. And [here](https://valdyas.org/fading/hacking/krita-hacking/back-from-the-blender-conference-2019/) is a blog post about it from one of the people who I follow, thats it `:wq ` for this month. Happy Diwali, :slightly_smiling_face:.​