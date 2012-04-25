--- 
published: true
title: JavaScript pre-processing with Uglify
body_class: post
layout: post
---




My JavaScript is full of debugging statements. `console.log()` all over the place, dumping loop indexes, JSON strings, AJAX responses, etc. When I deploy code, I obviously don't want all my debugging information showing up on every visitor's console. It's unnecessary, unprofessional, and makes the code unnecessarily large. So, I painstakingly remove all these helpful bits of code before deploying, but that's annoying, and if the debugging code was potentially useful in the future, I would just have to add it later.

Today I learned that the [Uglify JS][1] compressor has a handy feature for just this sort of situation. By defining (but *not* declaring) a global variable and wrapping all my debug statements in conditionals dependent on that variable, I can tell Uglify to replace that variable with the value `false`, thereby turning those blocks into dead code, which gets removed. The resulting minified code won't have any debugging code in it, making it as small and clean as possible, but my development copy will still contain my useful debugging statements and functions.

For example, this code defines the global variable `DEVMODE` and sets it to `true`, so when I'm testing locally, the block dependent on `DEVMODE` executes normally:

    if (typeof DEVMODE == 'undefined') DEVMODE = true;
    for (var i = 0; i < 10; i++) {
         if (DEVMODE) console.log('i is ' + i);
         myFunction(i);
    }

When I run Uglify on this, I give it the `--define DEVMODE=false` parameter, and the result is:

    for(var i=0;i<10;i++)myFunction(i)

The minified code contains no references to my `DEVMODE` variable and is as compact as possible, but my development version still has my useful debugging statement intact.

 [1]: https://github.com/mishoo/UglifyJS "Uglify JS -- a JavaScript parser/compressor/beautifier"
