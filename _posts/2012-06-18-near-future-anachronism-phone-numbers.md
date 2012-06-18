--- 
published: true
title: Near-Future Anachronism -- Phone Numbers
layout: post
body_class: post
summary: Phone numbers are an inefficient, unnecessary throwback to the pre-Internet age. They should be eliminated and replaced with standard internet addressing.
---

> "I am not a number. I am a person!"
> -- The Prisoner, 1967

Human memory is fallible: we suck at remembering more than a handful of items in a list, whether they're numbers or groceries. We constantly write things down because we know our brains aren't trustworthy when it comes to minor but crucial details. We meet a group of people and have forgotten their names minutes later. We attend an event and forget all but the most important details within weeks, if not days. Our brains are designed to hold onto only what we really need, and to gloss over the little stuff.

![Closeup crop of a rotary phone dial][img1]
_[1920's phone in B & W by Mark Mathosian / CC-BY-NC-SA 2.0][photo]_

Unfortunately, one type of little stuff is something we need and use practically every day: phone numbers. There are few things that are so ubiquitous in our lives and yet so antagonistic to the way memory works than an arbitary string of digits with no implicit relationship whatsoever to the person or company to whom they belong. Continuing to use phone numbers as a primary means of estalishing contact is actively hostile: we stress about remembering them, about making sure everyone who contacts us has the right one. It takes far too much brainpower to try and move these meaningless strings of digits around from device to device, person to person.

My friend [Vitorio][1] approached this problem by actively seeking out a meaningful phone number: you can [contact him by dialing 858-VITORIO][2]. While a clever solution, this isn't available to everyone. However, two of the proposals in [ICANN's list of gTLD applications][3] give an inkling of a possible general solution: either *.CALL* or *.PHONE* lends itself nicely to a system for mapping meaningful, memorable names to our existing arbitrary phone numbers.

Imagine: instead of meeting someone and typing a string of 10 digits into your phone, you just type _alexanderbell.phone_. When you tap on his contact, your phone quickly does a DNS lookup and figures out that his domain maps to +1-123-555-0190 and places the call. It caches all these lookups based on the standard DNS TTL rules, and in areas of limited connectivity can do low-bandwidth lookups when necessary just by asking a cell tower. Using the common _hostname.domain_ format, users can map _mobile.alexanderbell.phone_ to their mobile number and _work.alexanderbell.phone_ to their office number, if desired. If he changes his number, he just updates the DNS record on his nameserver, and the change propagates to everyone who might need to call him.

It's far easier to remember and communicate a straightforward _.phone_ domain name than an arbitrary string of digits. Introducing a system like this would remove a common frustration and introduce all sorts of possibilities for simplifying and improving communication, which is exactly the sort of thing at which computers excel.

 [1]: http://vitor.io "Vitorio Miliano, designer"
 [2]: tel:+1858VITORIO "Vitorio Miliano, designer"
 [3]: http://newgtlds.icann.org/en/program-status/application-results/strings-1200utc-13jun12-en "ICANN list of proposed new gTLDs"
 [photo]: http://www.flickr.com/photos/markgregory/4393615812/ "Photo by Mark Mathosian / CC-BY-NC-SA 2.0"
 [img1]: /assets/img/post_images/2012-06-18-near-future-anachronism-phone-numbers/rotary.jpg "As communication technology evolves, the way we use it must evolve as well."
