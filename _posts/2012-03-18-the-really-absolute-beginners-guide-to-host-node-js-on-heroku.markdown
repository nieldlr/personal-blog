---
layout: post
title: The Really Absolute Beginner's Guide to Host Node.js on Heroku
date: '2012-03-18 09:51:37'
tags:
- heroku
- hosting
- node-package-manager
- node-version-manager
- node-js
---

I'm not a coder. Well, just a little bit. I've only had Java at high school. The rest I've taught myself. I mostly do front-end stuff now like HTML, CSS and jQuery. I can reverse-engineer PHP if I want to. But code from scratch, nope. Now, I've recently starting coding in Node.js. I really enjoy it. I've managed to write some cool apps that I'll expand on later. I wanted to host these apps online for further testing. I chose Heroku. Mostly as a first choice, but boy did I have trouble getting my app running. The <a href="http://devcenter.heroku.com/articles/node-js">Heroku Node.js documentation</a> is severely lacking for complete noobs. I spent almost two days just trying figure out what the hell I need to do. However, look no further! Here's a more in-depth guide for the complete beginner:

I'm going to assume that you have already programmed your app and can run it locally. This is not a HOW TO program Node.js post, but rather a tutorial on how to get the app online on Heroku.
<h3>Heroku Prerequisites</h3>
<del><span style="text-decoration: underline;">1) Switching to Node.js v0.4.7</span></del>

<em>Edit: This step is not needed anymore. You can use any version of Node.js, as far I as I know, by setting it in the package.json file. See step 3.1 for more details. The paragraph below is kept for historical purposes. Move along to step 2.</em>

Heroku says that you need to use Node.js v0.4.7 as this is what their servers use. It's also a stable version. I was coding however in &gt; v0.5. How do you change your Node.js version? <a href="https://github.com/creationix/nvm">Node version manager</a> is your candidate! This simple script allows you to have numerous Node.js versions running on your computer. The github page has easy instructions to get this going. <em>Warning</em>: if you reboot your computer, Node.js defaults back to your originally installed version. Just activate Node Version Manager again, as this might create errors when you try to run your app again. Something like this:
<pre>FATAL ERROR: v8::HandleScope::Close() Local scope has already been closed</pre>
<span style="text-decoration: underline;">2) Using variable ports</span>

Before hosting on Heroku I used fixed ports for my apps. You need to change this as Heroku does not like this. Where you define on what port your app should listen to, just add this:
<pre>var port = process.env.PORT || 3000;
	app.listen(port);</pre>
This is expressjs documentation. But the "process.env.PORT || 3000;" is the important part. You also set this up later on Heroku where you need the variable port.

<span style="text-decoration: underline;">3) Adding the correct files</span>

Now this is where I struggled a lot, because Heroku does not really explain these things to the n00bs like me. You need a package.json and Procfile in the root of your Node.js package. These two files help Heroku determine how to startup your service when you deploy it. Think of them as files that act on your behalf to start the server. They are instruction files.

<span style="text-decoration: underline;">3.1 package.json</span>

First create a package.json file that sits in your root folder where your node app is running from. Here is an example that I used for <a href="http://dotjunky.com">dotJunky</a>.
<pre>{
  	"name": "DotJunky",
	"author": "Niel de la Rouviere",
	"description": "A Static File Site that sells domain names",
  	"version": "0.0.1",
  	"dependencies": {
    	        "express": "2.5.x",
		"now": "0.8.x",
		"mailer": "0.6.x"
  },
  "engines": {
        "node": "0.6.18"
    }
}</pre>
Those are the bare minimum details that you need. The main importance of the package.json file is to manage your Node.js module dependencies. If you need Heroku to install modules using <a href="http://npmjs.org">NPM</a> (Node Package Manager), then you need to add the dependencies. In the case above, you can declare the version numbers. The 'x' is a wildcard.

<em>Edit: You also tell Heroku which version of Node.js you want installed in the "engines" field. I recommend this as the default probably changes as time goes on.</em>

To test if your package.json file works correctly, run "npm install" in your command line in your root directory, where the package.json file is, and it will, if configured correctly, install the dependencies locally under the folder "node_modules". Just add a .gitignore file also to your root directory that ignores "node_modules" as this does not need to be sent to Heroku, because Heroku creates this itself by using your package.json file.

<span style="text-decoration: underline;">3.2 Procfile</span>

The Procfile tells the Heroku server which file (and command) needs to executed to run your app. Think of this as the command line "node app.js", but in a file. A general Procfile looks like this:
<pre>web: node index.js</pre>
Replace the "index.js" with whatever your first file is to run, "server.js", "app.js" whatever your preference is. The "web" prefix tells Heroku's stack which Dyno/Process needs to run which command. As you can get workers and more web processes in Heroku, the Procfile will get more complex. You'll need <a href="https://github.com/ddollar/foreman">Foreman</a> to start your Procfile on your local machine to test it. I now use Foreman to run all my Node.js projects. Its as easy as:
<pre>foreman start</pre>
This triggers your Procfile.

Just a note of warning, the Procfile needs to be capitalized, otherwise it won't be found by Heroku.
<h3>Getting it online</h3>
<span style="text-decoration: underline;">4) Create a local git repo</span>

Now that you have your node app, your package.json file and Procfile ready, you can start uploading it. However, first init a git repo in your folder. If you have a git repo already, then skip this step.
<pre>git init
git add .
git commit -m "First commit"</pre>
<span style="text-decoration: underline;">5) Install Heroku</span>

Now that you have a local repo, you need to install Heroku on your local machine. It's fairly simple. Just <a href="http://devcenter.heroku.com/articles/nodejs#local_workstation_setup">choose one of these options</a>, in my case MAC OSX. This adds "heroku" to your command line. Everything on your local machine is now in order.

Now we are heading towards Heroku. First login:
<pre>heroku login</pre>
You'll be prompted for your details and to add a ssh key. Enter them and add one.

<span style="text-decoration: underline;">6) Creating a Stack</span>

Now you need to give heroku a command to create a stack for you. This is where your app will reside.
<pre>heroku create --stack cedar</pre>
If everything runs smoothly, you'll see this type of response:
<pre>Creating sharp-rain-871... done, stack is cedar
http://sharp-rain-871.herokuapp.com/ | git@heroku.com:sharp-rain-871.git
Git remote heroku added</pre>
<span style="text-decoration: underline;">7) Push to Heroku</span>

Heroku automatically adds a remote repository address for your local git repo under the name "heroku". Now push your git file to heroku.
<pre>git push heroku master</pre>
This takes a bit more time as it installs the dependencies and starts the app. If everything runs smoothly, you'll get a response like this:
<pre>Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 923 bytes, done.
Total 9 (delta 2), reused 0 (delta 0)

-----&gt; Heroku receiving push
-----&gt; Updating alpha language packs... done
-----&gt; Node.js app detected
-----&gt; Vendoring node 0.4.7
-----&gt; Installing dependencies with npm 1.0.8
       express@2.1.0 ./node_modules/express 
       â??â??â?? mime@1.2.2
       â??â??â?? qs@0.3.1
       â??â??â?? connect@1.6.2
       Dependencies installed
-----&gt; Discovering process types
       Procfile declares types -&gt; web
-----&gt; Compiled slug size is 3.2MB
-----&gt; Launching... done, v2
       http://sharp-rain-871.herokuapp.com deployed to Heroku

To git@heroku.com:sharp-rain-871.git
 * [new branch]      master -&gt; master</pre>
<span style="text-decoration: underline;">8) Final Heroku Configurations</span>

Before you run your app, you need to send Heroku some configurations.
<pre>heroku ps:scale web=1</pre>
This scales how many dynos you use for your "web" process. 1 is enough for small apps and sites. It's free too!
<pre>heroku config:add NODE_ENV=production</pre>
This is the variable port, but you need to add this so that expressjs can use it in some instances like caching (don't ask me!).

Now, if you have done this all correctly, your node app will be online and ready to kick some ass. The emphasis on this tutorial is to first make sure everything locally is in order BEFORE you send it to Heroku. I don't know how many times I pushed to heroku, got errors, went on troubleshooting, pushed again and repeat. In summary, make sure you have Node.js version 0.4.7, Procfile and package.json correctly configured as well as variable ports. If all these are in place, then pushing to Heroku will be easy. Good luck running those apps!