---
layout: post
title: Starting with Node.js and Npm
description: Reflecting on my journey and what I did next
date: '2014-04-30T11:29:58+01:00'
tags:
- Node
- JavaScript
author: Peter Saxton
share-image: https://31.media.tumblr.com/6bd789ccae1134869390db07051720dd/tumblr_inline_n4u8h03SsT1s4ay8u.png
tumblr_url: http://crowdhailer.tumblr.com/post/84311910118/starting-with-node-js-and-npm
---
<p><strong>What is Node?</strong></p>
<p>JavaScript is a language that was designed and built initially to only run in the <a href="http://en.wikipedia.org/wiki/JavaScript#History" title="JavaScript Histroy" target="_blank">browser</a>. At the time this required it to be very lightweight. Ass JavaScript was typically being delivered from untrusted sources certain features were unnecessary or worse a security problem. For example a webpage has no need to access your computers file structure and so this was omitted from the language. </p>
<p><a href="http://nodejs.org/" title="Nodejs.org" target="_blank">Node</a> puts these missing features that every language require back in. This means that you can run JavaScript applications outside the browser. What Node isn&rsquo;t is a server framework/librabray. <a href="http://expressjs.com/" title="Express - node.js web application framework" target="_blank">Express</a> and many <a href="http://codecondo.com/7-minimal-node-js-web-frameworks/" title="7 minimal Node.js Frameworks" target="_blank">others</a> build upon Node to make a web application framework.</p>
<p><img alt="image" src="https://31.media.tumblr.com/6bd789ccae1134869390db07051720dd/tumblr_inline_n4u8h03SsT1s4ay8u.png"/></p>

<p><strong>What is Npm?</strong></p>
<p>Node packaged modules (<a href="https://www.npmjs.org/" title="NPM" target="_blank">npm</a>) is the official package manager for Node. It fills the roll of bundler for Ruby. It facilitates simple downloading, upgrading and tracking of libraries added to a Node application.</p>
<p><!-- more --></p>
<p><strong>Installation</strong></p>
<p>This installation guide has been tested for myself using <a href="http://www.linuxmint.com/" title="Main Page - Linux Mint" target="_blank">Linux Mint</a> and should probably work on Ubuntu. The core ppa contains a node version however the ppa maintained by <a href="https://launchpad.net/~chris-lea/+archive/node.js/" title="node.js: Chris Lea" target="_blank">Chris Lea</a> is bundled with npm and provides a very convenient choice for downloading. First add his ppa and the fetch nodejs.</p>
<blockquote>
<p>$ sudo add-apt-repository ppa:chris-lea/node.js<br/>$ sudo apt-get update<br/>$ sudo apt-get install nodejs</p>
</blockquote>
<p>This should have added the command &lsquo;node&rsquo; and 'npm&rsquo; to your terminal. running 'node&rsquo; will enter the <a href="http://en.wikipedia.org/wiki/REPL" title="Read-eval-print loop Wiki" target="_blank">read evaluate print loop (repl)</a> for node. </p>
<p><strong>Starting a node project</strong></p>
<p>All details of a node project are kept in 'package.json&rsquo;. This file contains information such as name, author, version number and dependencies. Npm provides an init method which runs a helper to generate the package file. Starting a project looks like this</p>
<blockquote>
<p>$ mkdir node-project<br/>$ cd node-project<br/>$ npm init</p>
</blockquote>
<p>To install a node package to the project use install with the save switch or optionally the save-dev switch for packages that are only required when testing/developing.</p>
<blockquote>
<p>$ npm install &lt;name&gt; &ndash;save<br/>$ npm install &lt;name&gt; &ndash;save-dev</p>
</blockquote>
<p>Some packages will need to be installed globally. This is likely the case for ones that are adding a utility to your terminal. Such as <a href="http://gruntjs.com/" title="grunt">'grunt&rsquo;</a>, <a href="http://bower.io/" title="Bower" target="_blank">'bower&rsquo;</a>, etc. This is achieved with the global switch</p>
<blockquote>
<p>$ sudo npm install -g &lt;name&gt;</p>
</blockquote>
<p><strong>Sharing a node project</strong></p>
<p>Packages installed locally will, by default, be saved in the directory node_modules. These dependencies can be populated by npm from package.json and so do not belong in version control. Ensure that you add 'node_modules&rsquo; to your .gitignore file before committing.</p>
<p>When cloning a node project you will need to add the dependencies. Running npm install with no arguments will fetch dependencies specified in the package file and add them locally.</p>
<p>That covers the basics of starting a project with node. Node is relatively new with its first release in 2009. <a href="http://www.makeuseof.com/tag/what-is-node-js-and-why-should-i-care-web-development/" title="What is Node.js and why should I care" target="_blank">This</a> article covers why its worth taking notice while <a href="http://www.toptal.com/nodejs/why-the-hell-would-i-use-node-js" title="What the hell is Node.js" target="_blank">this</a> one covers where to use node.</p>

<p></p>
