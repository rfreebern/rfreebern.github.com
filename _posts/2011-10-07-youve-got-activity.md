--- 
published: true
title: You've got activity!
body_class: post
layout: post
---




If you use app tabs (or pinned tabs) in Firefox, Chrome, or Opera (I don't know if IE offers this feature), you're used to noticing the little highlight that indicates that the content on an app tab has changed. The de facto standard for triggering the highlight is to do it when the tab's document title has updated, and most web apps respect this and update their title to indicate how many new items there are for you to view.

I was musing to myself about this earlier when [David Ascher tweeted along the same lines][1]. Why shouldn't this behavior be more user-controllable? I would love it if browsers offered a javascript API for highlighting a tab. Perhaps the (old, non-standard, mostly-deprecated) `window.getAttention();` [method][2] could be repurposed for this?

An API like this could allow web apps to be a bit more unobtrusive about alerting the user to new activity while still changing the document title as needed to indicate the current page state, if desired. If this API existed, it would be easy to allow the user to tweak how often they're alerted to new changes.

 [1]: https://twitter.com/#!/davidascher/status/122368718067085312 "A tweet from @davidascher on Twitter"
 [2]: https://developer.mozilla.org/en/DOM/window.getAttention "window.getAttention on the Mozilla Developer Network"
