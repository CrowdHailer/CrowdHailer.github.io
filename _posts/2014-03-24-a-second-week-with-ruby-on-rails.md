---
layout: post
title: A second week with Ruby on Rails
description: Exploring convention over configuration in Rails
date: '2014-03-24T21:11:39+00:00'
tags:
- Ruby
- Ruby on Rails
- Makers Academy
author: Peter Saxton
tumblr_url: http://crowdhailer.tumblr.com/post/80608215513/more-rails-taming-the-beast
---
<p><strong>At the start of this week I was not a fan of <a href="http://rubyonrails.org/" title="Ruby on Rails" target="_blank">Rails</a></strong>, However I can see the potential it has to make simple things exceptionally easy. One week of working with rails is far from enough to realise this potential and I felt it I was struggling to make any decent progress with it. </p>
<p>This week we were split into teams to work on a instagram clone, called <a href="https://github.com/Maikon/DeathStarPhotoService" target="_blank">snappy gram</a>. Working in a team of four this time two pairs programming would have made sense. However there was so much we didn&rsquo;t know we weren&rsquo;t able to pair effectively. Instead we sat on the sofa round the big TV and coded as a four. This worked quite well to discuss problems we came across but is definitely not the most productive way to organise a group in terms of code generation.</p>
<p><!-- more --></p>
<p>Working more, it became increasingly clear how important it is to embrace Rails, to use convention over configuration. If you do not do this then you are missing the point and potential. A good example is link tags. We were easily able to see how to create links by mixing erb statements into the html. Instead the rails way is to us a <a href="http://apidock.com/rails/ActionView/Helpers/UrlHelper/link_to" title="link_to" target="_blank">link helper</a> to make this just that bit easier. This has led me to formulate my golden rule of Rails.</p>
<ol><li>Google it first.</li>
</ol><p>Rails is an enormous project with a very active community, because of this is has a great number of gems which cover almost anything you could think to do in a project. This means that when you have a problem it&rsquo;s probably solved and the solution packaged into a gem. A great example from this week was the following. We wanted to make it possible for people to tag the uploaded images. We started down the route of database migrations before we came across the &rsquo;<a href="https://github.com/mbleigh/acts-as-taggable-on" title="acts as taggable" target="_blank">acts-as-taggable</a>&rsquo; gem. This makes making an object taggable ludicrously trivial. </p>
<p>The size and scope of these Rails plugins varies enormously. King of these gems is <a href="https://github.com/plataformatec/devise" title="Devise on github" target="_blank">devise</a>. This gem solves everything to do with user sign-up, sign-in, password storage and more. The magic is more than a little disorientating it really is impossible to understand everything it is doing in the time-scale we have. However we got it too work and the only downside seamed to be the mad English it introduces. Words such as omniauthable have now entered my vocabulary.</p>
<p>At the end of this week I am much happier with Rails. I see why purist developers can object to it but I also see the point of it. Most helpful to my understanding of rails this week was this excellent series of lectures of <a href="http://www.youtube.com/watch?v=ra8Q0M3DJYk" title="Efficient  Rails Test-Driven Development" target="_blank">efficient rails testing</a>. I can not recommend these enough. Even though they are a little older the are still worth watching. Also as an explanation of authentication this <a href="http://railscasts.com/episodes/270-authentication-in-rails-3-1" title="authentication in rails" target="_blank">rails cast</a> is helpful.</p>
