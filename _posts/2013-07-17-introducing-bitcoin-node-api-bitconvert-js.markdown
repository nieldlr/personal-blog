---
layout: post
title: Introducing Bitcoin Node API and Bitconvert.js
date: '2013-07-17 03:45:18'
tags:
- bitcoin
- javascript
- node-js
---

Since working on <a href="http://min.io">Min.io</a>, a Bitcoin project with my brothers, I've started doing a lot more Bitcoin development. I'm doing contract work for <a href="http://safepaperwallet.com">Safe Paper Wallet</a> as well, building and improving their paper wallet generator, which has been incredibly fun to work on. Besides those projects, I've created two new open-source projects: <a href="https://github.com/nieldlr/Bitcoin-Node-Api">Bitcoin Node API </a>and <a href="https://github.com/nieldlr/bitconvert.js">Bitconvert.js</a>.
<h2>Bitcoin Node API</h2>
While coding the payment server for <a href="http://min.io">Min.io</a>, I would communicate with the Bitcoin wallet using <a href="https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_Calls_list">JSON-RPC commands</a>. There's a <a href="https://github.com/freewil/node-bitcoin">module</a> that easily interfaces with it, but it's only for the back-end. Most often I would test payments and need to quickly debug something using a JSON-RPC command. I often had to stop the server, put in the command and run again. This was not ideal. I wanted to reach the commands quickly and effortlessly.

I then <a href="https://github.com/nieldlr/Bitcoin-Node-Api">created an Express middleware plugin</a> that maps JSON-RPC commands to any chosen url. So for example if you map the middleware to /bitcoin/api and then run http://localhost:5000/bitcoin/api/getinfo, it will return the data produced by the 'getinfo' command.

It makes rapid Bitcoin development really easy. Anyone can now interface with their wallet using query strings by just adding a few lines of code. In fact a whole Bitcoin Node API server is now just these few lines of code!
<pre>var bitcoinapi = require('bitcoin-node-api');
var express = require('express');
var app = express();

//Username and password relate to those set in the bitcoin.conf file
var wallet = {
  host: 'localhost',
  port: 8332,
  user: 'username',
  pass: 'password'
};

bitcoinapi.setWalletDetails(wallet);
bitcoinapi.setAccess('default-safe'); //Access control
app.use('/bitcoin/api', bitcoinapi.app); //Bind the middleware to any chosen url
app.listen(3000);</pre>
Not all commands are supported yet though. I'll be adding them as I go along. You also have access control available to secure your api. For example:
<pre>bitcoinapi.setAccess('restrict', ['dumpprivkey', 'sendmany']);</pre>
Setting that restricts access to the 'dumpprivkey' and 'sendmany' commands.

Check out the <a href="https://github.com/nieldlr/Bitcoin-Node-Api">Github Repo</a> if you want to contribute.
<h2>Bitconvert.js</h2>
<a href="https://github.com/nieldlr/bitconvert.js">Bitconvert.js</a> is a simple javascript script that converts any number within a user specified CSS class to and from Bitcoin &lt;-&gt; USD. It's written with no dependencies and gets the latest prices from MtGox. I wrote this so that any website owner can add a toggle for their prices into Bitcoin if they wanted to sell their goods using Bitcoin. It's also really simple:
<pre><code>&lt;script src="bitconvert.js"&gt;&lt;/script&gt;
&lt;span class="amount"&gt;$ 5.24&lt;/span&gt;
&lt;span class="amount"&gt;$ 1&lt;/span&gt;
&lt;button onclick="bitconvert.toggleConversion()"&gt;Toggle&lt;/button&gt;
</code></pre>
I've been enjoying Bitcoin immensely. It's great to work on something <a title="Six Reasons why I’m long on Bitcoin" href="http://niel.delarouviere.com/2013/05/reasons-long-bitcoin/">so incredibly exciting</a>.