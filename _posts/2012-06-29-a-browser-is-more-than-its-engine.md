--- 
published: true
title: A Browser is More Than its Engine
layout: post
body_class: post
summary: iOS versions of popular browsers may be forced to use UIWebViews, but that doesn't mean they're just Mobile Safari with a different package.
---

Yesterday, Google announced [Chrome for iOS][1], on the heels of Mozilla's announcement of their [Junior][2] browser for iPad and Yahoo's entry in the area, [Axis][3]. The similarity between all these new browsers is that, due to Apple's limitations, they're all using the iOS-standard UIWebView, effectively an embedded version of Mobile Safari's WebKit engine, because there's no other way to render web content on the fly on iOS devices.

![Screenshot of Twitter showing tweets that all express the sentiment that iOS Chrome "isn't really Chrome"][img1]

_[A common sentiment is that iOS Chrome "isn't really Chrome"][screenshot]._

A gecko ain't a fox
--------------------

While the rendering engine is obviously an important piece of any browser, it's not the lone thing that defines the browser any longer. A browser today encompasses an entire platform and ecosystem of tools supporting it, including the UI, password and privacy management, bookmarks, sync services, developer tools, plugins and add-ons, installable webapp support, and more. The rendering engine helps drive all of that at a low-level, but the full browser experience is more than just how the HTML, CSS, and JavaScript are interpreted.

Today's browser is a brand, one that collects all these parts into a single, unified experience of the web. When Mozilla decided to build Junior for the iPad, they knew they couldn't bring gecko into Apple's walled garden. That wasn't the point. Instead, the goal was to allow the Firefox brand to carry over to the iPad, so that people who identify as "Firefox users" would have an option to maintain that identity on their chosen device, albeit in a limited fashion.

The engine still matters
------------------------

Mozilla and the open web still derive value from the gecko engine's existence -- the fact that a volunteer-supported non-profit open-source engine is in daily use by hundreds of millions of people matters to the health of the web and to Mozilla's ability to affect standards development and make sure they're as beneficial as possible to the ecosystem. Chrome's ability to push the boundaries of what's possible with web technology using its version of WebKit and the V8 engine is important for breaking new ground and exploring new frontiers. One implementation of WebKit will never be enough for a healthy web, and it would benefit everyone if Apple relaxed its restrictions on browser makers.

In the mean time, it still makes sense for the browser makers to make sure their users have options no matter what platform they choose to use, and, conversely, it's foolish to ignore a popular platform simply because part of the browser can't exist there, when your users would much rather use their preferred tool than something else that's just "good enough".

The proof of the pudding
------------------------

In essence, if you fire up a browser and it _feels_ like your usual browser, even if it behaves somewhat differently or the UI has changed, you might as well be using the same browser. If it can sync your passwords and bookmarks, and respond to the same commands you're used to, and support the tools and use-cases you need, neither the cosmetic differences nor the fact that it's reporting a different user-agent matter. What matters is that, whether you consider yourself a Chrome user, a Firefox user, an Opera user, or something else entirely, you should have the option to be who you are no matter what device you're interacting with.

 [1]: https://www.google.com/intl/en/chrome/browser/mobile/ios.html "Chrome for iPhone and iPad"
 [2]: https://air.mozilla.org/product-design-at-mozilla/ "Product Design at Mozilla -- Junior"
 [3]: http://axis.yahoo.com/ "Yahoo! Axis"
 [screenshot]: https://twitter.com/search/isn%27t%20really%20chrome "Twitter search: isn't really chrome"
 [img1]: /assets/img/post_images/2012-06-29-a-browser-is-more-than-its-engine/isnt-really-chrome.png "A common sentiment is that iOS Chrome &ldquo;isn't really Chrome&rdquo;."
