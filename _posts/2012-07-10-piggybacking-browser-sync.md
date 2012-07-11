--- 
published: true
title: Piggybacking Browser Sync for Fun <strike>and Profit</strike>
layout: post
body_class: post
type: side
summary: If a user's browser is set up to save &amp; sync passwords, that functionality can be extended to sync arbitrary data.
---

Last fall, [I wrote about localStorage and browser sync][1], and posited that it would be nice if browser syncing was standardized and had an API so that apps could specify what locally-stored data should be synced to other browser instances. Today I threw together a hacky proof-of-concept showing how, when the browser is set up properly, an app could piggyback on the existing browser sync functionality to send arbitrary data between instances. You can check out my [data sync example][2] at jsFiddle.

In a nutshell: as long as the browser is set to save and sync passwords, javascript code can write arbitrary data to a password input in a form, and (as long as the browser thinks it's a real password field) it'll get synced to another instance of the browser eventually. Then when the page is loaded in the other instance, the password field is auto-filled by the browser, and the javascript can read the data in that field and act on it.

It's obviously a hack -- not only does it require specific settings that can't be tested for, but it pops up a message asking to save or update the password every time the form is submitted, and there's no notification or control over when the data sync actually occurs. However, I think it's an interesting subversion of the sync system, and shows what could be done with a sync API.

 [1]: http://blog.rnf.me/2011/localstorage-browser-sync-and-the-future.html "localStorage, browser sync, and the future - I ? the web"
 [2]: http://jsfiddle.net/rfreebern/7Wf9Z/ "Data sync by rfreebern on jsfiddle"
