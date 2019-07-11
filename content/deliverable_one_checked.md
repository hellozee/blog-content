+++
title = "Deliverable 1 : [✓]"
date = 2019-06-19T00:48:42+05:30
tags = ["krita","gsoc","open-source","kde", "cpp"]
categories = ["krita"]

+++

Finally done with the first phase of the [feature](https://forum.kde.org/viewtopic.php?f=156&t=126095&sid=3412fbb963f693811ec1a7605a991b9b) I wanted, 4 years back. Though just the unit test for the algorithm is implemented. At least for now, we can detect edges and stick to it. Here is one of the test results,

![Magnetic Lasso Teset](/img/mlassotest.png)

Seems okay, far better than the initial results. Although I should say, I deviated from what I thought I would need to write. First I assumed that I don't have to write another `boost::graph` wrapper for `KisPaintDevice`, but I had to. That was one heck of an experience. In one of the last few posts, I ranted on Dmitry's interpretation of the Graph, turns out we were on the same page but I understood his explanation the wrong way. I should put more attention to details from now on I guess.

All the pixels are connected to each other, but they only have an edge between them if they are adjacent. If in center, the out degree would be 8, if in corners, 3 and if in edges, 5. There are some other cases too, but I will leave them for the moment.

While writing the wrapper, I also got to know some of the cool features and techniques of C++, which I will be writing posts on as soon as I get some time, concepts, traits, avoiding virtual functions and what not. It is commendable that how `boost` approaches `boost::astar_search`, there is not a single virtual function, you don't have to inherit anything (you can though for safety), just templates and traits, you are done.

Another thing for me was, my effort on the heuristic function went to vain, cause it didn't improve the results over a normal euclidean distance function, at least for now, the tests results do agree with that, anyway I got a chance to channel my math instincts to, the function to optimize the bounding box, providing the minimum area to be searched, don't know if it works properly or not, but hey for now, it works fine, I shouldn't be worrying.

Now the UI part, this would be the most irritating as far as I can see but now I can get more people to help me, not like the earlier one. If everything goes well, I would be landing some final touches before what would I call my first international trip and that too solo & sponsored. 

And yes, the test is available on my branch, [here](https://invent.kde.org/kde/krita/tree/kuntalmajumder/T10894-magnetic-lasso).

In the end it all feels like, I just underestimated the amount of work I needed to do, well software engineering is not that easy. It was suppose to be a just applying Laplacian of Gaussian operator on the image and do an astar search, it turned out a lot more than that. Making people understand is easier but not that reliable, making computers understand seems hard, but results can be relied on, up to an extent.

But the best part is, I am able to do this while getting paid, Google Summer of Code, ftw.

Thats it, `:wq` for now.