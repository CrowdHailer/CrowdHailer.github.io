---
layout: post
title: 'Makers Academy: Penultimate Week'
description: Starting our final group project.
date: '2014-03-31T07:37:00+01:00'
tags:
- Heroku
- Git
- TDD
author: Peter Saxton
tumblr_url: http://crowdhailer.tumblr.com/post/81270534766/makers-academy-penultimate-week
---
<p><strong>This week is the first of two on our final project.</strong> After a somewhat drawn out process at the end of last week we had come together to form four project groups. I was in the largest and the six of us were going to build a platform to show off ourself as <a href="http://ma-student-directory.herokuapp.com/" title="Student Directory" target="_blank">Makers Academy Graduates</a>.</p>
<p><img alt="image" src="https://31.media.tumblr.com/6f3da632ced4a793ddcee874c3eda1a0/tumblr_inline_n38m9hwGuO1s4ay8u.png"/></p>

<p><strong>On Monday we started by initialising a rails project adding devise and then struggling to sort out <a href="https://github.com/intridea/omniauth" title="intridea/omniauth" target="_blank">omniauth</a>.</strong> Omniauth is using another sites authentication for our own. In our case from github. This was surprisingly difficult and took us all of Monday to get nowhere. Come Tuesday two of us had worked it out, eventually. I had found this <a href="http://thecrentist.com/2013/11/02/how-to-set-up-authentication-ruby-rails-omniauth" title="How to set up authentication in Rails 4" target="_blank">link</a> which was useful at explaining what should be done but still is not perfect. </p>
<p>As it turned out omniauth is possible without devise so Tuesday we restarted from a blank canvas. Two hours in and we had done more than all of the previous day. </p>
<p><!-- more --></p>
<p><strong>A group of six was the largest I had worked in so far.</strong> One difficulty was dividing up work at the start, because when setting up the foundations your can find yourself working on something that touches everything. This means that three pairs working simultaneously is not possible. By midweek we were able to start working as three pairs and then code generation was surprisingly rapid, I was often checking our <a href="https://github.com/CrowdHailer/Final-Project/network" title="Network Graph - CrowdHailer/FinalProject" target="_blank">repo&rsquo;s network graph</a> to see what was happening.</p>
<p>With a bit more freedom it was easy for us to volunteer only to work on the bits of the project we were most interested in. It was quickly apparent that as a group we were more keen on developing the back end over dealing with styling issues. It also turned out that not everyone was convinced by the value of refactoring tests. I am and therefore when working alone it turned out that this was were I spent my time. After one early morning start, the test suit was completely over hauled by the time 9 am rolled around. This refactoring showed its worth when it next came to adding a field to our user model. With only one line of code we had all the tests to allow a user to save a linked in address. </p>
<p>This week I discovered <a href="https://github.com/bblimke/webmock" title="Webmock" target="_blank">Webmock</a>, a test mocking framework. With it all requests to the outside world can be blocked. This ensures that you don&rsquo;t over use calls to an API. Combined with some custom rake tasks to generate JSON data this turned out to be very powerful. I will have to write a post on this and maybe even a Gem.</p>
<p><strong>One very positive thing in our group was the desire for proper testing and git practices</strong>. The pressure to move forward was notably higher but all of us were making best attempts towards best practices. Mihai in particular forced me to up my game on how I merged in commits and pushed. </p>
<p>As always seams to happen when focusing on one thing another can be neglected. This week that thing was running the tests. We had written good tests. When merging I would make sure all my merges where on feature branches and not the master. However as we concentrated on the correct merge order actually running the tests passed slipped my mind. A few hours later over half the tests were failing because no one had rerun them as they merged. We quickly addressed that but the procedure for merging in feature branches was now getting extensive. The work flow was as follows.</p>
<ol><li>commit last change on feature branch</li>
<li>run tests</li>
<li>switch to master</li>
<li>pull from origin (github)</li>
<li>switch to feature branch</li>
<li>merge from master branch</li>
<li>run tests</li>
<li>switch to master</li>
<li>merge from feature branch</li>
<li>run tests</li>
<li>push to origin (github)</li>
<li>push to Heroku</li>
</ol><p>I&rsquo;m not sure how many times I managed all 12 steps in the correct order this week. Hopefully it will be more often next week. I can see why people incorporate tools such as git flow but for the moment I want to work on getting the practise.</p>
<p>Two interesting links to share from this week. First <a href="https://www.mashape.com/" title="Cloud API" target="_blank">Mashape</a> a showcase and market place for 100&rsquo;s of API&rsquo;s. Second a <a href="https://github.com/showcases/" title="Github Showcases" target="_blank">showcase</a> of some of the most interesting projects on github.</p>
