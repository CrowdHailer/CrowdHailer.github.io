---
layout: post
title: JavaScript testing with Karma and Jasmine
date: '2014-06-28T09:01:12+01:00'
tags:
- JavaScript
- node
- TDD
- Test Driven Development
author: Peter Saxton
tumblr_url: http://crowdhailer.tumblr.com/post/90139965671/javascript-testing-with-karma-and-jasmine
share-image: https://31.media.tumblr.com/42570fe7d7898e6ad26fafd182811b3d/tumblr_inline_n4sr1sTZA71s4ay8u.png
---
<p>I have been using <a href="http://jasmine.github.io/" title="Jasmine: Behaviour-Driven javascript" target="_blank">Jasmine</a> running in the browser to test my JavaScript for a while now. Coming from the background of <a href="http://rspec.info/" title="rspec homepage" target="_blank">RSpec</a> the syntax is reassuringly similar. However running tests in the browser has several downsides. First there is a rather annoying html file that is required to hold the code and tests together. Second running the tests like this means opening up a browser and moving away from the terminal. This is an annoyance most of the time and completely unsuitable to work with continuous integration. The solution to both this problems is to work with a command line tool, in this case karma.</p>
<p><img alt="image" src="https://31.media.tumblr.com/42570fe7d7898e6ad26fafd182811b3d/tumblr_inline_n4sr1sTZA71s4ay8u.png"/></p>
<p><!-- more --></p>
<p>Karma runs on node.js and is easiest installed using the node package manager (npm). If you have not got either of these installed checkout my post on getting started with <a href="http://crowdhailer.tumblr.com/2014/04/30/starting-with-node-js-and-npm.html" title="starting with nodejs and npm" target="_blank">node and npm</a>.</p>
<p>Karma is a test runner and requires a test framework to work with. Supported frameworks are jasmine, qunit and mocha. A discussion of the differences between these is beyond this post. In summary I chose Jasmine as it is the most complete without add ons.</p>
<p>Karma also requires a browser to run the tests and a plugin to handle that browser. Supported browsers are Chrome, ChromeCanary, FireFox, Safari, PhantomJS, Opera and InternetExplorer.</p>
<p>Getting started the first step is to initialise a node project then add the test dependencies to package.json.</p>
<blockquote>
<div class="line" id="LC17"><span class="nt">&ldquo;devDependencies&rdquo;</span><span class="p">:</span> <span class="p">{</span></div>
<div class="line" id="LC18">    <span class="nt">&ldquo;karma-jasmine&rdquo;</span><span class="p">:</span> <span class="s2">&ldquo;~0.1.3&rdquo;</span><span class="p">,</span></div>
<div class="line" id="LC19">    <span class="nt">&ldquo;karma-phantomjs-launcher&rdquo;</span><span class="p">:</span> <span class="s2">&ldquo;~0.1.1&rdquo;</span><span class="p">,</span></div>
<div class="line" id="LC20">    <span class="nt">&ldquo;karma&rdquo;</span><span class="p">:</span> <span class="s2">&ldquo;~0.10.6&rdquo;</span><span class="p">,</span></div>
<div class="line" id="LC21">    <span class="nt">&ldquo;karma-spec-reporter&rdquo;</span><span class="p">:</span> <span class="s2">&ldquo;0.0.12&rdquo;</span><span class="p">,</span></div>
<div class="line" id="LC27">  <span class="p">}</span></div>
</blockquote>
<p>Running <em>&lsquo;npm install&rsquo;</em> will install all of the packages locally to node. At this point to run any of the karma commands you will be required to enter the whole path, to run the tests for example is likely to be.</p>
<blockquote>
<p><span>$ ./node_modules/karma/bin/karma start</span></p>
</blockquote>
<p>This is tedious and fortunately karma also has a tool to add these commands to your path. To add the command karma to the terminal the package karma-cli needs to be installed globally. </p>
<blockquote>
<p>$ npm install -g karma-cli</p>
<p>$ karma start  // same as long command above</p>
</blockquote>
<p>The configuration settings are kept in karma.conf.js. Here you set how you would like to format the output, whether to run continuously and what files to load. There are a lot of whys to set up karma, this is my preference.</p>
<blockquote>
<p>module.exports = function(config) {<br/>  config.set({<br/>    basePath: &ldquo;,<br/>    frameworks: ['jasmine&rsquo;],<br/>    files: [<br/>      'bower_components/path/to/dependency.js&rsquo;,<br/>      'src/*.js&rsquo;,<br/>      'spec/**_spec.js&rsquo;,<br/>    ],<br/>    reporters: ['spec&rsquo;],<br/>    port: 9876,<br/>    colors: true,<br/>    logLevel: config.LOG_INFO,<br/>    autoWatch: false,<br/>    browsers: ['PhantomJS&rsquo;],<br/>    captureTimeout: 60000,<br/>    singleRun: true<br/>  });<br/>};</p>
</blockquote>
<p>An important thing to note is to remember to load up all your dependencies, also when using wildcards the files will be added in alphabetical order. When the order is important then that will need to be declared specifically. It took me a while to spot that one as the first three projects I did the correct order was alphabetical order</p>
<p>I always use the test suite as a single run through. As the test suites I have written so far take less than 1 sec I have always been happy to explicitly run them. This also works well with continuous integration.  </p>
<p>Finally the <a href="https://github.com/mlex/karma-spec-reporter" title="karma-spec-reporter" target="_blank">'spec&rsquo; reporter</a> is not included by default and needs to be added through node</p>
<blockquote>
<p>$ npm install karma-spec-reporter &ndash;save-dev</p>
</blockquote>
<p>That&rsquo;s getting started with karma, but doesn&rsquo;t cover writing any of the tests. That is because karma can run many different flavours of tests. A simple test framework to start with is <a href="https://github.com/pivotal/jasmine" title="jasmine - github" target="_blank">Jasmine</a>, which has an exceptionally clear <a href="http://jasmine.github.io/2.0/introduction.html" title="Introduction to jasmine js" target="_blank">introduction</a> to the basics and several more powerful techniques. There is also a great supply of plugins for handling fixtures, asynchronous code and more. Because Jasmine offers such a complete solution I have not always found it the easiest to integrate plugins with. For this reason I want to try <a href="http://visionmedia.github.io/mocha/" title="Mocha, the fun, simple, flexible javascript test framework" target="_blank">mocha</a> which is an alternative test framework that can be run on karma, and will hopefully be reported on in the future.</p>
