+++
title = "Commentary on the Qt situation"
date = 2020-04-16T19:37:44+05:30
tags = ["qt", "kde"]
categories = ["foss"]
+++

A lot of things have been going on with Qt these days. It all started with The Qt Company trying to get an increase in their revenues, specifically [this](https://www.qt.io/blog/qt-offering-changes-2020) blog post. And just like a proper PR team, they didn't talk about the changes clearly for the open-source folks who use the product. If I can summarize the whole thing for open source users, it boils down to,

- No extended support for LTS releases for open source users, we will get the release but we would have to manually backport the security patches. The Qt Company would backport them but only for the commercial customers.
- No offline installer for open source folks, if we want to install Qt from the _website_, we need to use the online installer.
- For using the online installer we need to have a Qt account, which was optional earlier.

These changes won't affect open source Qt that much, on the other hand, the last 2 points do make sense. The Qt company is paying for the server to host the builds, it would be wrong for us to expect them to do that for no charge. Other than that, the first point would mean the open-source community needs to do some extra work to backport security patches. A thing which distro packagers already used to do in the past when there were no LTS releases of Qt.

While the dust around this was trying to settle, something again popped up. A [mail](https://mail.kde.org/pipermail/kde-community/2020q2/006098.html) in the kde-community mailing list. The mail is a bit long, but the important thing to ponder over is, The Qt Company is losing revenue due to the ongoing pandemic. And so to increase their revenue they are trying to restrict the releases to 12 months for open source folks. Why 12 months? Cause that's the maximum that they can have, if they don't open-source the code by then, they would be forced to release Qt under BSD license legally as per the contract between KDE e.V. and the company.

To me, it is more like the company is just testing the water of how far they could go with restricting their product. As they retracted with a poorly written blog [post](https://www.qt.io/blog/qt-and-open-source) later. Notice that they have disabled comments on that post.

Now, why are they trying to do this?

- Increase their revenue, of course.
- The shareholders don't have much idea about open source.

What could be the consequences of this?

- Open source folks would lag with patches being open-sourced with a year delay.
- KDE forks Qt and it is being maintained by the community.

Both situations are not healthy. If open source releases lag by a year, it would mean the thousands of open-source software that relies on Qt would be devoid of all the security patches, making them vulnerable.

If KDE forks Qt, it would be a huge task on the community to maintain it on their own, especially parts like QtWebEngine. Though we could always backport all the patches to the fork after a year along with ours. If companies which rely on the LGPL Qt, come together, an open-source Qt fork could surely be maintained under KDE. It might be a bit of trouble to organize everything but it is not impossible at all.

Though in this scenario The Qt Company loses a lot,

- Less testing of their product, since no open source folks would be using it.
- No patches from open source contributors.
- They can't backport the patches from the fork to upstream.

Nonetheless, it would also be somewhat troubling for KDE too to manage all those stuff cause we don't how deep are the waters we are trying to swim in. Though I could be definitely wrong cause there are much more experienced folks in the community who are vouching for a fork.

This event at least made me realize a couple of things, one The Qt Company never acknowledges the open source contributions. I never saw a single mention of KDE in their blog post leave all other projects. Second don't rely on one thing too much. It is great that Qt makes C++ as easy as Java, but relying too much on it could have worse consequences.