---
layout: post
title: The 5 challenges I faced in developing my new project HanziCraft
date: '2013-01-18 05:01:30'
tags:
- chinese-character
- chinese-radicals
- hanzicraft
- hanzijs
---

In 2012 I had a coding rebirth. I needed to improve my coding skills for my degree and went straight into Node.js as it was the quickest to pick up coming from front-end web design. While coding for my research I also spent some time on side-projects, that <a title="Side Project Skill Creep" href="http://niel.delarouviere.com/2012/12/side-project-skill-creep/">in the end taught me a lot</a>!
<p style="text-align: center;"><a href="http://niel.delarouviere.com/2013/01/5-challenges-faced-developing-project-hanzicraft/screen-shot-2013-01-18-at-10-32-13-am/" rel="attachment wp-att-301"><img class="aligncenter  wp-image-301" alt="HanziCraft" src="http://res.cloudinary.com/daxztt3th/image/upload/v1412147197/Screen-Shot-2013-01-18-at-10_32_13-AM_rzxjfy.png" width="640" height="270" /></a></p>
I now introduce my biggest project yet: <a href="http://hanzicraft.com">HanziCraft</a>. This site has been in development for a few months. I did all of the coding myself, however, the site is based on my open-source Node.js module, <a href="http://hanzijs.com">HanziJS</a> (here's the <a href="http://github.com/nieldlr/hanzi">Github Repo link</a>), which has one more active contributor (thanks <a href="https://plus.google.com/114101734864850163495/posts">Dusan</a>!). He helped me refactor a lot of the code. I learned a lot with that.
<h2>Challenges</h2>
<h3>1) Payments</h3>
One of the big challenges for HanziCraft was to make it available as a payable project from the start. I had to figure out to how work with a payment processor. I ended up choosing <a href="https://www.paypal.com/ipn">Paypal IPN</a>, mainly due to the fact that most processors require US bank accounts. It was tough to figure it out at first, but I managed to get it to work in the end.

Besides the countless hours trying to figure it out (I wish the documentation was easier to understand), I actually quite like the simplicity of it now.
<h3>2) User Flow</h3>
Only users that have accounts will be able to use the premium features on the site. So I needed to figure out how to make this buy process and account creation process as smooth as possible. After consulting with <a href="http://simondlr.com">Simon</a>, we came up with a smooth system.

User buys with Paypal -&gt; Server creates blank user -&gt; User receives email to register his account (this includes password + username + contact email) -&gt; User gets a secret link to fill this in -&gt; Ta-da new premium user!

This way the disconnect between user account &amp; payment does not occur.
<h3>3) Actual users!</h3>
Most of my either sites have passive users (besides <a href="http://socialmandarin.com">Social Mandarin</a>, which is based on Drupal), thus they only interact with the content without contributing. If they need to, they just fill in a form, such as adding a blog on <a href="http://polyglotlink.com">Polyglot Link</a>. Now, <a href="http://hanzicraft.com">HanziCraft</a>, is the first project where I had the responsibility towards paying customers (and their data).

I had to make sure that the way they use the site was going be what they expect from websites: forget password features, user profiles, security etc.

I realized there are more things to add than you think and it's not necessarily the part I like coding that much. <strong>I like solving problems, not merely coding database/server logic into a system</strong>. However, now that I've coded those elements, I can easily just use it again for future projects!
<h3>4) Information Dense Design</h3>
I still don't think I've gotten the perfect design for HanziCraft yet (<a title="7 Lessons I Learned from Blogging" href="http://niel.delarouviere.com/2012/09/7-lessons-learned-blogging/">I'm a redesign junkie</a>), but it's definitely an interesting design challenge. A dictionary-like service needs to be clever on how to present information as it's usually text heavy:
<ul>
	<li>&gt; Don't overwhelm the user</li>
	<li>&gt; Use ONLY what is needed.</li>
	<li>&gt; Aesthetic elements need to improve readability. Anything else should be removed.</li>
	<li>&gt; Keep the colour scheme simple.</li>
	<li>&gt; Make sure that the design does not leak into each other, this causes confusion (this I think I still need to work on).</li>
</ul>
In any case. I love this challenge. I'll be tweaking HanziCraft's design for a long time to come. If you have any suggestions, let me know!
<h3>5) The relationship between open-source &amp; product</h3>
As I said earlier. HanziCraft is based on my own open-source module (<a href="http://hanzijs.com">HanziJS</a>). I had to walk an interesting line in how I handle the relationship between the two: what do I submit for the open-source part &amp; what do I code into the site?

For instance, one of the premium features of HanziCraft is the ability to submit more than one character at a time. Before I wanted that as premium feature, it was not available as a function in HanziJS. So I decided to add a decomposeMany function to the code. This allows other developers to use such a feature, but also helped me with my site.

Another example of the relationship between the two. <strong>I created a merged relationship for messy input handling</strong>. What happens if I submit non-Chinese characters? HanziCraft first removes all non-Chinese characters form the field &amp; then sends this to HanziJS. Here, I validate the data to see if it's still good or not. However, <strong>it's not really necessary, because I know all elements that I send to HanziJS, will be clean.</strong>

However, if I just use HanziJS and give it messy input, such as a null input or non-Chinese character, it will just return "Invalid Input" for that specific character.

This mixed method allows me to create solid function for HanziJS, but I went a bit further in HanziCraft to make sure that what is sent to HanziJS doesn't contain any wrong input. This feature is not necessarily needed for HanziJS, <strong>because it it's up the developer to decide what he wants to send to function</strong>. What if he wants to determine non-valid input? This allows him to.
<h2>Conclusion</h2>
<a href="http://hanzicraft.com">HanziCraft</a> is an absolute blast to work on. I love working with Chinese characters &amp; trying to solve my own problems regarding info I want for learning Chinese. I've already had a few sales for premium accounts &amp; the response so far has been positive. If you're learning Chinese, <a href="http://confusedlaowai.com/2013/01/introducing-hanzicraft/">check my post on Confused Laowai</a>, regarding the reasons behind why I created HanziCraft.