---
layout: post
title: Quick intro to Bower
description: Packet management for the web with bower.
date: '2014-06-25T08:30:00+01:00'
tags:
- Bower
- JavaScript
author: Peter Saxton
tumblr_url: http://crowdhailer.tumblr.com/post/89842223952/quick-intro-to-bower
---
<blockquote>
<p><em><a href="http://bower.io/" title="Bower" target="_blank">Bower</a> is a <a href="http://en.wikipedia.org/wiki/Package_management_system" title="package management - wiki" target="_blank">packet manager</a> for the web.</em></p>
</blockquote>
<p>Because of JavaScript&rsquo;s unique place as the browser of the browser it is a slightly different flavour of packet manager. Bower is built to use git and allows you to gather remote packages that you can then use in your web application. Where bower differs from others is that, unlike <a href="https://www.npmjs.org/" title="npm" target="_blank">npm</a> for node, it is not responsible for loading the packages into your runtime environment.</p>
<p><!-- more --></p>
<p><strong>Getting Bower</strong></p>
<p>Bower itself is a node package and so first you must ensure that your system has node and npm. You can see my <a href="http://crowdhailer.tumblr.com/2014/04/30/starting-with-node-js-and-npm.html" title="Starting with node and npm" target="_blank">blog post</a> on starting with these. Now you have these on your system you can start with bower. Install Bower globally with the following command.</p>
<blockquote>
<p>npm install -g bower</p>
</blockquote>
<p><strong>Bower packages</strong></p>
<p>Packages can be installed directly and bower  will save the them to the <em>bower_components</em> directory by default.</p>
<blockquote>
<p>bower install &lt;package-name&gt; </p>
</blockquote>
<p>Bower can also use a <em>bower.json</em> file to install packages. There is an init function that will interactively create one, providing helpful defaults for name and version.</p>
<blockquote>
<p>bower init</p>
</blockquote>
<p>If you are only creating a private project this file is most useful for saving dependencies. Packages can be manually added to the json file. The install command also includes a switch to automatically save installed packages</p>
<blockquote>
<p>bower install &lt;package-name&gt; &ndash;save</p>
</blockquote>
<p>In the future running bower install will automatically install all dependencies mentioned in the json file.  </p>
<p>There are a huge number of available packages, from simple utilities to full frameworks such as <a href="http://ionicframework.com/" title="Ionic - Mobile App framework" target="_blank">ionic</a>.</p>
<p><strong>Registering a package</strong></p>
<p>Running off git it is fantastically easy to create a bower package. First make sure that the bower.json file is created and contains information such as name, author and keywords. Then the package can be registered using</p>
<blockquote>
<p>bower register &lt;name&gt; &lt;url&gt;</p>
</blockquote>
<p>The name is the name the package will be registered under and has to be unique. The url is to a public git repository where the package is located. And that&rsquo;s it.</p>
<p>Built on top of git creating a new release is as simple as tagging a commit in your repo and pushing it to the remote storage.</p>
<p><strong>Using Bower</strong></p>
<p>Registering a package is so simple that I have found it an easy way to manage code even within projects. Recently I have been writing an application to manipulate SVG images. During development I have created several useful utilities that I wanted to factor out of the main code base. Instead of storing them in separate files, but still in the main repository, and combining them using a grunt task. I have added them as bower packages. This makes them far more accessible to future projects. Most importantly this has made them available to others and helps to grow opensource code bases. Something that I can feel good about even if they may not have been used by anyone. My bower packages so far are:-</p>
<ol><li><a href="https://github.com/CrowdHailer/cuminjs" title="cumin js" target="_blank">Cumin</a>, <span>utilities library favouring curried functions and functional operations</span></li>
<li><a href="https://github.com/CrowdHailer/belfry.js" title="Belfry.js" target="_blank">Belfry</a>, a<span> simple publish subscribe library returning curried functions to work with cumin</span></li>
<li><a href="https://github.com/CrowdHailer/SoVeryGroovy" title="SVGroovy" target="_blank">SoVeryGroovy</a>, convenient API for generating SVG components</li>
<li><a href="https://github.com/CrowdHailer/Hammerhead2" title="Hammerhead2" target="_blank">Hammerhead2</a>, The main graphics functionality calling all the above as dependencies</li>
</ol>
