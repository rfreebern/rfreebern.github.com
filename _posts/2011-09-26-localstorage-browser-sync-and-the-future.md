--- 
published: true
title: localStorage, browser sync, and the future
body_class: post
layout: post
summary: Some thoughts about whether the data in a browser's localStorage should be synced to other devices, and how that syncing might be managed.
---

HTML5 localStorage and IndexedDB are awesome. Firefox and Chrome's built-in browser syncing is awesome. However, right now, [neither Chrome][1] [nor Firefox][2] make any attempt to sync localStorage. The fact that this isn't a settled issue is understandable: it's explicitly supposed to be local data, which is understood to mean that it's not automatically getting sent somewhere remote, which is what sync does by definition.

Do users even really want localStorage for a domain to get synced across devices? The data that a webapp stores in your desktop browser may not be pertinent in your phone's browser, or on your tablet, or at work. Plus, given the [W3C's "mostly arbitrary" 5mb limit][3], it may be preferable to keep each device's locally-stored data separate in order to maximise the amount each can store, rather than trying to combine it all.

I think the eventual solution to this, which I expect web developers to start asking for more and more often as usage of these technologies increases, is for some way to mark specific data as "data that should be synced" vs. "data pertinent to only the current device." I expect that, further, they will realize that in order to control what gets synced where, something along the lines of [CSS3 media queries][4] will need to exist: "sync this data only to other mobile devices" or "sync this data, but not to screenreaders".

And once syncing is part of the localStorage specification language, it, too, will suddenly fall under the purview of the W3C. With any luck, they will work with browser makers to define a secure, open protocol for syncing browser data and storage, which will open the door for more third-party sync services.

 [1]: http://code.google.com/p/chromium/issues/detail?id=47327 "Chromium bug 47327 -- allow extensions/apps to sync their own settings"
 [2]: https://bugzilla.mozilla.org/show_bug.cgi?id=500052 "Firefox bug 500052 -- Sync DOM storage"
 [3]: http://dev.w3.org/html5/webstorage/#disk-space "W3C Web Storage specification: Disk Space"
 [4]: http://www.w3.org/TR/css3-mediaqueries/ "W3C CSS3 Media Queries specification"
