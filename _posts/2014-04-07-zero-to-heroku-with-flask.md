---
layout: post
title: Zero to Heroku with Flask
description: Experimenting with microservices in my last week at Makers Academy
date: '2014-04-07T10:50:33+01:00'
tags:
- linux
- heroku
- python
author: Peter Saxton
share-image: https://31.media.tumblr.com/49fa738badbf3b0da52dbec0810d836e/tumblr_inline_n3nnbnAtWa1s4ay8u.png
tumblr_url: http://crowdhailer.tumblr.com/post/81978869488/zero-to-heroku-with-flask
---
<p><strong>This week I tried my hand at some Python for the first time in a long time.</strong> The goal of this was to simply create a &lsquo;Hello World!&rsquo; application on <a href="https://www.heroku.com/" title="Heroku" target="_blank">Heroku</a>.</p>
<p>Linux Mint comes with Python as standard and this post will be entirely about working with Mint. The useful tools I set up are on the recommendation of &rsquo;<a href="http://twoscoopspress.org/products/two-scoops-of-django-1-5" title="Two Scoops Press" target="_blank">Two scoops of Django</a>&rsquo; and their chapter on environment setup.</p>
<p><img src="https://31.media.tumblr.com/49fa738badbf3b0da52dbec0810d836e/tumblr_inline_n3nnbnAtWa1s4ay8u.png"/></p>

<p><!-- more --></p>
<p>First I needed <a href="https://pypi.python.org/pypi/pip" title="Python Package Index" target="_blank">pip</a>, a package management system for software written in python. Second <a href="http://www.virtualenv.org/en/latest/" title="virtualenv" target="_blank">Virtualenv</a>, which is used to create isolated Python environments. This addresses the same role as Ruby Gemfiles and Bundler. These two are installed with apt-get.</p>
<p><em>    $ sudo apt-get install python-pip<br/>    $ sudo apt-get install python-virtualenv</em></p>
<p>Also recommended was the nattily named virtualenvwrapper. This can be installed in the same way but requires some further setup. To set the location of project and the python environments I had to add the following to my bash profile. </p>
<p><em>    export WORKON_HOME=$HOME/.virtualenvs</em><br/><em>    export PROJECT_HOME=$HOME/Devel</em><br/><em>    source /usr/local/bin/virtualenvwrapper.sh</em></p>
<p><strong>With this setup the project can now be started making full use of the tools installed above.</strong> Amazingly these tools mean that it is possible to have a project live on Heroku with only 10 commands from the terminal. I have split these into two groups of 5. The first being</p>
<ol><li><em>$ mkproject hello</em></li>
<li><em>$ pip install Flask gunicorn</em></li>
<li><em>$ pip freeze &gt; requirements.txt</em></li>
<li><em>$ touch hello.py </em></li>
<li><em>$ echo 'web: gunicorn hello:app&rsquo; &gt; Procfile</em></li>
</ol><p>So what happened here? mkproject is a command from virtualenvwrapper, it creates an environment called hello and and project called hello. Then it switches to the project directory and starts the created environment. Both Flask and gunicorn are python packages that we install to the enviroment. pip freeze lists all packages that are currently in use, saving them to requirements.txt allows Heroku to install the same ones. we then create an application file called hello.py and a Procfile to give instructions on starting the application.</p>
<p>At this point we can write an application in the hello.py file. For a quick example I just used the sample application for Heroku for <a href="https://devcenter.heroku.com/articles/getting-started-with-python#hello-py" title="Getting started with python and Heroku" target="_blank">getting started</a>.</p>
<p><strong>So at this point we have a working application that can be run locally with foreman. </strong>Next is to push this to Heroku. These steps should be familiar if you have previously used Heroku however I have listed them below for completeness. </p>
<ol><li><em>$ git init</em></li>
<li><em>$ git add .</em></li>
<li><em>$ git commit -m 'init&rsquo;</em></li>
<li><em>$ heroku create</em></li>
<li><em>$ git push heroku master</em></li>
</ol><p><strong>At this point your application is live on Heroku.</strong> Running a final 'Heroku open&rsquo; will open the application in your default browser to prove the point. </p>
<p>These tools are brilliant but this is only the slimmest of introductions. For a fuller overview is this <a href="http://www.clemesha.org/blog/modern-python-hacker-tools-virtualenv-fabric-pip/" title="Python Hacker tools" target="_blank">blog post</a>.</p>
