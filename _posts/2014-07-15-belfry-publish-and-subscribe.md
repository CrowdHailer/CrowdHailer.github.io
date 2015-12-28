---
layout: post
title: Publish Subscribe pattern in JavaScript
description: Implementing a simple pub-sub object in JavaScript
date: '2014-07-15T08:42:03+01:00'
tags:
- JavaScript
- Functional Programming
author: Peter Saxton
tumblr_url: http://crowdhailer.tumblr.com/post/91830951758/belfry-publish-and-subscribe
---
<p>An ever present consideration when making software is it&rsquo;s maintainability. A code&rsquo;s maintainability is tightly linked to its accessibility, how easily the next person looking at it can understand it. To make code understandable it must either have a familiar structure, be broken into manageable sensible chunks or perhaps both. There are several guiding principle is to achieve this. Reduce coupling and and increasing cohesion and the Single Responsibility principle are all about this goal. </p>
<p>Following a given structure is a common practise for Rails developers and can produce great results. However what happens when one section begins to grow and the standard structure no longer offers further division. This happened to me recently with the front end JavaScript code. As it depended on more user click events, I rapidly entered a <a href="http://blog.caplin.com/2013/03/13/callback-hell-is-a-design-choice/" title="Callback hell is a design choice" target="_blank">callback hell</a>.</p>
<p>The solution, the publish subscribe pattern. There are standalone pieces of code that you can use to implement this. A really good one is <a href="https://github.com/addyosmani/pubsubz" title="pubsubz - gitub" target="_blank">pubsubz </a>from <a href="http://addyosmani.com/blog/" title="Addy Osmani blog" target="_blank">Addy Osmani</a>. However it seamed small enough for me to roll my <a href="https://github.com/CrowdHailer/belfry.js" title="belfry.js - github" target="_blank"><em>own version</em></a>.</p>
<p><img src="https://31.media.tumblr.com/809c9ead2fbc62a2b7f4b72c64eedfbe/tumblr_inline_n8qtdpvii81s4ay8u.jpg"/></p>
<p><!-- more --></p>

<p><strong>Principles</strong></p>
<p>A globally accessible object is responsible for passing a messages that is triggered on one channel to all subscribers of that channel. The other objects in the software system are only activated by broadcasts on the channel they listen to and can only communicate the results they generate by broadcasts. Importantly they will have no idea who is listening. </p>
<p>As an example a completed ajax callback may take the returned data and broadcast that new data is available. A separate object can then write the data to the screen. The original ajax object does not know or care what happened to the data it retrieved. </p>
<p><strong>Advantages</strong></p>
<p>The events are universal and can easily be re-purposed. In the example above if data is loaded by another means, perhaps from local storage, the same event can be fired and with no further changes it will be written to the screen. Tests and logging can be added implemented on the same events. </p>
<p><strong>Disadvantages</strong></p>
<p>If an event is lost, for example objects are broadcasting on channel while the screen writer is listen on a different on, are lost permanently. There is no true/false return for successful completion of an action. In reality this is normally a good thing as waiting for those confirmations particularly in asynchronous code leads to alot of code spaghetti. However when testing it was something that I learnt to check first when tests where failing. </p>
<p><strong>Implementation</strong></p>
<p><em>Control object</em></p>
<p>The <a href="http://addyosmani.com/resources/essentialjsdesignpatterns/book/#singletonpatternjavascript" title="design patterns" target="_blank">singleton pattern</a> is very useful for this as it is imperative that all calls to broadcast reach the same object. The following code creates a tower instance the first time it is called and in all subsequent calls returns the first created instance.</p>
{% highlight js%}
function(global){
  var instance;
  function init(){
    // code goes here
    return instance
  }
  global.Belfry = {
    getTower: function(){
      if (!instance) {
        instance = init();
      }
      return instance;
    }
  };
());
{% endhighlight%}
<p><em>Subscribing</em></p>
<p>Each channel is an array on a channels object. When subscribing a function to a channel the function is added to the corresponding array. </p>

{% highlight js%}
function subscribe(topic, reaction){
  var channel = channels[topic] = channels[topic] || [];
  channel.push(reaction);
}
{% endhighlight%}

<p>Publishing</p>
<p>When a broadcast is made each function in that channels array is called with the content that is to be added to the broadcast.</p>

{% highlight js%}
function publish(topic, content){
  _.each(function(action){
    action(content, topic);
  })(channels[topic] || []);
}
{% endhighlight%}

<p>And that is in essence the components of a pubsub. Checkout my library <a href="https://github.com/CrowdHailer/belfry.js" title="Belfry.js - github" target="_blank">belfry</a> to see a full implementation. There are several embellishments, such as the ability to unsubscribe. The functionality is also curried as this allows broadcast functions for individual channels to be generated which can then be passed around. This reduces the chances of broadcasting on the wrong channel. </p>
<p>This pattern is closely related to other approaches. <a href="http://stackoverflow.com/questions/15594905/difference-between-observer-pub-sub-and-data-binding" title="stackoverflow" target="_blank">This is a nice explanation of some of those</a>. I have also tried using events instead of callbacks after watching <a href="https://www.youtube.com/watch?v=eIovclygbwM" title="Custom events and the Observer Pattern" target="_blank">this talk on the observer pattern</a>. </p>
