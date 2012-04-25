--- 
published: true
title: Making twirssi work for me
body_class: post
layout: post
---




[Irssi][1] is my chat client of choice. Natively it handles IRC quite well, easily maintaining connections to multiple networks and keeping track when people are looking for me. It also has [many useful scripts and plugins][2] that make it work in other ways, such has handling [XMPP][3] for me, [acting as a proxy for a GUI IRC client][4] (if I desire), and more. Last week, while experimenting with running [TTYtter][5] inside an irssi window (which worked fine but was less than optimal for various reasons), I came across [twirssi][6], a Twitter client written as an irssi plugin.

I got twirssi set up and running, and was quite impressed. It did everything I wanted in a Twitter client, including things like filtering out tweets based on substrings that I had been looking for everywhere (hooray, no more foursquare tweets!), and integrated nicely with an environment I already knew. It did have one shortcoming, though: trying to skim through a screenful of tweets looking for a specific twitter nickname was difficult.

![Screenshot of twirssi without nickname colorization][img1]

Rather than just put up with frustration, I [forked the code on github][7] and [added persistent hash-based nickname colorization to it][8], which made each twitter nickname have a specific text and background color, so when I want to see [@BrendanEich][9] and [@glazou][10] having a conversation about -webkit- CSS prefixing, it's dead simple to visually find all the relevant tweets.

![Screenshot of twirssi with nickname colorization][img2]

The code I wrote was reviewed and accepted by [@zigdon][11], the creator and maintainer of twirssi, and is now part of the codebase. If you use irssi and Twitter and want to give twirssi a try and see my colorization code in action, just install the plugin, run `/twirssi_upgrade` to pull the most recent beta code from the master branch on github, and `/set twirssi_nick_color rotate`. I think it makes a huge difference in twirssi's usability, and the whole process was a great demonstration of how open-source software can work.

 [1]: http://irssi.org/ "Irssi, a console IRC client"
 [2]: http://scripts.irssi.org/ "Irssi Scripts"
 [3]: http://cybione.org/~irssi-xmpp/ "Irssi plugin to support XMPP, the eXtensible Messaging and Presence Protocol"
 [4]: http://irssi.org/documentation/proxy "Irssi proxy module"
 [5]: http://www.floodgap.com/software/ttytter/ "TTYtter, a console Twitter client"
 [6]: http://twirssi.com "Twirssi, an irssi-integrated Twitter client"
 [7]: https://github.com/zigdon/twirssi "Twirssi on github"
 [8]: https://github.com/zigdon/twirssi/pull/50 "Pull request #50 adding nickname colorization"
 [9]: https://twitter.com/#!/brendaneich "Brendan Eich, creator of JavaScript"
 [10]: https://twitter.com/#!/glazou "Daniel Glazman, W3C CSS working group co-chair"
 [11]: https://twitter.com/#!/zigdon "Dan, the creator of twirssi"
 [img1]: /assets/img/post_images/2012-02-12-making-twirssi-work-for-me/twirssi_no_colors.png "Twirssi without nickname colorization"
 [img2]: /assets/img/post_images/2012-02-12-making-twirssi-work-for-me/twirssi_colors.png "Twirssi with nickname colorization"
