---
layout: post
title: Side Project Skill Creep
date: '2012-12-05 22:15:34'
tags:
- dotjunky
- hanzijs
- javascript
- node-js
- npm
- polyglot-link
- side-projects
---

<img class="aligncenter size-full wp-image-282" title="Building Blocks" src="http://res.cloudinary.com/daxztt3th/image/upload/v1412147199/8240281227_2a0aa5bcce_z_vadvys.jpg" alt="" width="640" height="360" />

In between completing my Master's, I spent a lot of time working on side-projects. When I look back over the year, I realized each side-project taught me new skills, like building blocks paving the foundation for the next one. The best way improve in coding is to build something and I did just that.

Here's how it went:
<h2>1) HanziJS: Request/Posts &amp; Jade Templating</h2>
<a href="http://hanzijs.com">HanziJS</a>, the <a href="http://github.com/nieldlr/hanzi">open-source project</a>, started before the site itself. I wanted to decompose Chinese characters for my research, so I thought why not make this available to other users. I posted it on <a href="http://www.reddit.com/r/ChineseLanguage/comments/r3g5m/hey_rchineselanguage_ive_created_a_character/">reddit</a> and got some great feedback, but one comment was specifically about how the site worked.

My total newbie self, created the channel between the front-end and back-end via websockets (Now.js), which was completely overkill for this type of project. I quickly learned about post/get requests. Epic facepalm moment there.

The reason I did websockets was because I wasn't sure how to embed data from Node.js from the backend into the front-end. So I learned Jade templating as well.
<h2>2) dotJunky: Sending Emails &amp; Forms</h2>
Althought <a href="http://dotjunky.com">dotJunky</a> is closed now (more on that later), I had to learn how to send emails using Node.js. I picked up the <a href="https://github.com/Marak/node_mailer">mailer</a> module and quickly learned how to send emails. I used SendGrid on Heroku.

I had to get email addresses via forms though. I had trouble at first as to how <a href="http://expressjs.com">ExpressJS</a> handled forms, but after a day or two I figured it out.
<h2>3) Chinese character experiments: Better Javascript data structures</h2>
Although not a side-project, out of curiosity I <a href="http://confusedlaowai.com/2012/08/learned-frequent-chinese-characters/">created an experiment on Confused Laowai</a>. I did a laborious 4 levels deep for loop through whole Chinese character dictionaries and the like. <strong>It was slow</strong>. Really slow.

With 50 characters the project ran for 7 hours!

I was absolutely absorbed for the next few days trying to make it more efficient. Lo and behold I found dictionary structures. I don't know why I never used this before.<strong> I'm a noob I know</strong>! Before I just iterated over the WHOLE array of over 100, 000 entries every single time I did a lookup to find a potential word in the Chinese dictionary.

I used this knowledge to improve <a href="http://github.com/nieldlr/hanzi">HanziJS</a> tremendously.
<h2>4) Polyglot Link: User Logins &amp; MongoDB &amp; Feed Parsing</h2>
<a href="http://polyglotlink.com">Polyglot Link</a> is a directory for language learning blogs. At first I wanted to create a flat html directory as an MVP, but then I realized this would just create more hassle down the line. So I decided to learn how to use MongoDB. It was actually quite easy in it the end! I used <a href="http://mongoosejs.com">Mongoose</a> as middleware.

However, now that I used MongoDB, I needed a way to work with the data in an easy way, because I have to moderate new blog submissions. Therefore, I created an admin section, but anyone could access it. Woops, user login time!

I used <a href="http://passportjs.org/">Passport</a> as my framework. I must admit, I scratched my head numerous times trying to figure how this works: sessions, authentication and more.

I did one more thing thanks to the ease of Node.js modules. I hashed my password using <a href="https://github.com/ncb000gt/node.bcrypt.js/">node.bcrypt.js</a>! Safety first.

After some time I added a feed that parses all the blogs listed on the site. I did this by creating a public Google reader folder and using <a href="https://github.com/danmactough/node-feedparser">node-feedparser</a>.
<h2>5) HanziCraft: Paypal Payments and Improved User Management</h2>
<a href="http://hanzicraft.com">HanziCraft</a> is an improved version of HanziJS. I'll do a blog post about that in the near future. I had to improve the user management system I created in <a href="http://polyglotlink.com">Polyglot Link</a> to allow for user creation and multiple users.

Furthermore I wanted to implement paid-for premium features. Paypal was my only option due to South African regulations and options. I spent numerous days researching options. In the end I created a nice workflow using <a href="http://paypal.com/ipn">Paypal's IPN feature</a>. This was integrated with the user creation process. I sent emails too using the knowledge I learned from dotJunky.
<h2>It all adds up</h2>
In the end it all adds up. I was lucky that each side project taught me something new, especially in such a linear manner. Each project built on the knowledge of the previous one.

I'm sure my coding is still terribly inefficient, but I've come a long way since the start of the year. If you want to learn just create!

Pic: <a href="http://www.flickr.com/photos/chiky/8240281227/in/pool-44124304756@N01/">Source</a>