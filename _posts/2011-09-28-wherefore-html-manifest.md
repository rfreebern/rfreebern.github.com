--- 
published: true
title: Wherefore HTML manifest?
body_class: post
layout: post
---




The first time I read [details about offline web apps and the cache manifest file](http://diveintohtml5.info/offline.html), one of my first thoughts was "why did they choose *that* syntax?"

    <html manifest="cache.manifest">

It doesn't really make sense to me. Yes, an offline web app has HTML as its basic ingredient. HTML defines the structure of the data and lays the groundwork for every other part of the app. But are the caching instructions really an attribute of the HTML tag?

Ideally, I think, the cache would have been specified like this:

    <link rel="cache manifest" type="text/cache-manifest" href="cache.manifest" />

Link tags are the canonical way to say "here's another resource related to the current document in some explicit way." It just made sense that something like a manifest describing what items to cache for offline use would be considered a related document.

I dug through the WHATWG mailing lists to try and find an answer. [Ian Hickson](http://hixie.ch) made [the first offline web apps proposal](http://lists.whatwg.org/htdig.cgi/whatwg-whatwg.org/2007-August/012418.html) way back in August 2007, and right there in his first email on the subject is the following:

> My proposal is that we add a new attribute to the `<html>` element, which flags that the page is a Web app that wants to be pinned for offline execution and that when you next fetch the file or one of its subresources while online, it should try to update all the subresources atomically.

> `<html application>`

> This could either trigger the different behaviour automatically, or only when requested by the user, or we could say this applies to any page, butthat the user must enable it, or we could provide an API which triggers this for the page. I kind of like the explicit attribute, though.

The email thread continues for several months, with dozens of people debating most of its points&hellip; but not this one. The proposal eventually turned into [a draft](http://www.w3.org/TR/html5/offline.html), which has been implemented by all the major browsers, using an attribute on the HTML tag to specify the cache manifest.

Unable to find any sort of justifcation (beyond Hickson's original "I kind of like it"), I decided to go to the source, and found Hickson on Mozilla's IRC server. I asked him his reasoning, and he replied:

>   <tt>&lt;Hixie> &lt;link> is how I would have liked to do it, but &lt;link> unfortunately comes too late</tt>

>   <tt>&lt;Hixie> it really has to be the earliest possible thing in the page</tt>

So, there you have it. It's in the HTML tag because that's the first thing on the page that the browser parses, and if it encounters a manifest attribute it knows to check that first before trying to download any of the app's other related resources. A link tag would have been nicer semantically, but by the time the browser encounters and is acting on the link tags, it's already possibly begun fetching network resources, which is unintended behavior when the cache manifest hasn't yet been parsed.
