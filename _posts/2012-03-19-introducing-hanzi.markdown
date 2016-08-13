---
layout: post
title: Introducing Hanzi
date: '2012-03-19 15:33:56'
tags:
- chinese-character-decomposition
- hanzi
- node-package-manager
- node-js
- nodejs-module
- radical-decomposition
---

This weekend I set out to solve a problem in Chinese learning I've had trouble with for some time. Chinese characters consist of radicals, which are the fundamental building blocks of each character. However, there was no way to automatically dissect it without consulting dictionaries, random websites and other untrustworthy sources.

<a href="http://niel.delarouviere.com/2012/03/introducing-hanzi/screen-shot-2012-03-19-at-3-29-29-pm/" rel="attachment wp-att-197"><img class="aligncenter size-full wp-image-197" title="HanziJS" src="http://niel.delarouviere.com/wp-content/uploads/2012/03/Screen-Shot-2012-03-19-at-3.29.29-PM.png" alt="" width="517" height="225" /></a>

I've been looking for a database for quite some time now and I have found some sources [<a href="http://www.kanjicafe.com/kradfile_license.htm">1</a>][<a href="http://groovy.codeplex.com/wikipage?title=cjk-decomp">2</a>]. I decided to go with number 2, which is a similar type of program for Python. Number 1 is focused on Japanese characters (Kanji) where in essence are the same as Chinese characters, but some characters are different, thus character decomposition will be different. Number 1's decomposition however is more thorough. Hopefully I'll combine in the future. I took the second database and wrote a module for Node.js, called <a href="http://hanzijs.com">Hanzi</a>. I know, how original. For the non-Chinese learners, Hanzi means Chinese characters in Chinese.

It was interesting to write my own module for Node.js, as it is something I have not done before. I always Node Package Manager for many awesome utilities in my Node.js projects. This time I filled a gap and <a href="http://search.npmjs.org/#/hanzi">published my own.</a>

It's a bit cumbersome at the moment and definitely has a few errors, but this is just the start. So head on over to <a href="http://hanzijs.com">HanziJS.com</a> to check the module in action.