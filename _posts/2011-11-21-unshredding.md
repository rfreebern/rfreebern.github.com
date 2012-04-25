--- 
published: true
title: Unshredding
body_class: post
layout: post
---




A week ago, [the Instagram engineers posted a challenge on their blog][1]: given an image "shredded" into a set of equal-width strips, write an image processing algorithm to "unshred" the image and put the original back together. When [@nigelbabu mentioned this][2], I was intrigued, and decided that it was a good excuse to learn some new stuff about image processing and using the HTML5 canvas element.

![Example of shredded image and properly unshredded image][img1]

By the end of that day, I had hacked together a messy chunk of javascript that *mostly* solved the problem, with the notable problem that the strips, while almost in order, were wrapped horizontally by about six strips. My admittedly simplistic color-comparison algorithm was working nearly perfectly, except it was getting thrown off by the darkened edges of the sample photo.

![Unshredded image aligned improperly][img2]

My thought upon seeing this was that perhaps I needed to neutralize the lightness/darkness of the pixels before comparing -- but before I could get into that, the code needed to be rewritten to be cleaner, because doing the necessary tweaks to get it in working order wasn't practical the way it was.

Cut to: a week later. Life, being what it is, conspired to keep me from having enough free time to really dig into the code again. In the meantime, everyone and their sister finished and released their own solutions in various languages, which I studiously avoided -- I wanted my solution to be as un-influenced as possible. There was one notable exception: after seeing several people mention how awesome it was, I went and looked at [Joe Lambert's solution][3], but didn't check out his code.

Meanwhile, I tried to figure out the best way to approach a solution, and read various Wikipedia articles, like [root mean square][4] and [YUV][5], both of which turned out to be instrumental in eventually coming up with a solution.

The root mean square is exactly what it says on the tin: the square root of the mean of the squares of a bunch of terms in a sequence. In other words, it's the standard deviation from the mean of a function's output, which I could use to tell when two columns of pixels were significantly different from each other.

The YUV colorspace is an alternative to the "usual" RGB(a) respresentation of color data. YUV has a "luma" (lightness/darkness) component and two color components that map to a Euclidean colorspace. It was designed to work well with human color perception, which I think makes it ideal for a task like algorithmically determining if an image "looks right". By converting the image's RGB data to YUV, I could effectively ignore the Y (luma) and just compare the change in color value, which eliminated the difficulty caused by changes in the image's lightness level.

With these tools at my disposal, I was able to tweak my algorithm to the point where it could not only correctly analyze and reassemble the example image created by Instagram, but do the same with similarly shredded images.

My final result is called [Image Unshredder][6]. It will take any photo that has been divided into equal-width stripes and shuffled and attempt to determine the stripe width and then sort the stripes into the correct order. It won't work perfectly on every image or every stripe width, but it does a good job most of the time.

If I wanted to spend more time polishing it, I would memoize the result of some of the functions, try to find speed and memory-usage enhancements, refactor it into a reusable class, separate the image processing code from the DOM manipulation code, and maybe try to turn it into a web worker so that it doesn't lock the UI while it does its processing. But for now, it works!

 [1]: http://instagram-engineering.tumblr.com/post/12651721845/instagram-engineering-challenge-the-unshredder "The Instagram Unshredding Challenge blog post"
 [2]: https://twitter.com/#!/nigelbabu/status/136000425034911744 "Nigel Babu on Twitter"
 [3]: http://www.joelambert.co.uk/unshred/ "Joe Lambert's HTML5/JS solution to the Instagram unshred challenge"
 [4]: http://en.wikipedia.org/wiki/Root_mean_square "Root mean square on Wikipedia"
 [5]: http://en.wikipedia.org/wiki/YUV "YUV on Wikipedia"
 [6]: http://rfreebern.github.com/instagram-unshredder "Image Unshredder, rfreebern's Instagram Unshredding Challenge entry on github"
 [img1]: /assets/img/post_images/2011-11-21-unshredding/instagram_example.png "Example unshredding solution"
 [img2]: /assets/img/post_images/2011-11-21-unshredding/badly_wrapped.png "Badly wrapped unshredding solution"
