---
layout: post
title: Capability objects
description: JS control
date: 2015-11-26 16:39:05
tags:
- Functional Programming
- Immutability
- Design
author: Peter Saxton
---

**Bring predictability to you code through the use of Capability Objects**

Code that has side effects is often less predictable and therefore more difficult to test and reason about.
Some functional languages go to great lengths to control side effects, such as Haskell with its use of the IO Monad.
Capability objects provide a simple mechanism for controlling side effects in JavaScript.
There use can improve the rationality, readability and reusability of program components.

### What makes a function side effect free
A function is isolated from side effects when:

  1. The only result of it's execution is the return value.
  2. The return value is always the same given the same arguments.

*Point 1 alone makes a function side effect free.
Point 2 alone defines a pure function.
A function with both is said to be referentially transparent.*

Like many things these are easiest to demonstrate with an example.

{% highlight js %}
// Pure and side effect free
function add(a, b){
  return a + b;
}

// Impure but side effect free
function flip(){
  return Math.random() >= 0.5 ? "heads" : "tails";
}

// Pure but has side effect
function addAndLog(a, b){
  console.log("adding", a, b);
  return a + b;
}
{% endhighlight %}

There are many ways a function can become coupled to the outside world.
Including accessing global variables such as the window object, logging and throwing errors.
It is important to remember that a program cannot be useful without eventually causing a side effect.
The goal of a capability object is to control a function and to render it effectively isolated.

### Capability Objects and effectively isolated functions.
A capability object is simply an argument to a function that may be impure or have side effects.
An effectively isolated function is one that is pure when the capability object has only pure functionality and is side effect free when the capability object is side effect free.

We can rewrite our examples above to be effectively isolated as follows

{% highlight js %}
function flip(randomiser){
  return randomiser.random() >= 0.5 ? "heads" : "tails";
}

function addAndLog(a, b, logger){
  logger.log("adding", a, b);
  return a + b;
}
{% endhighlight %}

This simple change has many benefits, but to show them off lets use a more sophisticated example.
We have a simple dispatcher.
It is initialized with an array of callback functions and a logger (the capability object).
When dispatch is called with an action it needs to call each callback with the same action and log the action.
If any callback throws an error it needs to capture this so that the other callbacks are still called.
If there are no callbacks then we will log the action as a warning, we will assume that we should always have at least one listener.

{% highlight js %}
function Dispatcher(callbacks, logger){
  this.dispatch = function(action){
    callbacks.forEach(function(callback){
      try {
        callback(action);
      } catch(err) {
        logger.error(err);
      }
    });

    if (callbacks.length === 0) {
      logger.warn(action);
    } else {
      logger.info(action);
    }
  };
}
{% endhighlight %}

### Testing log messages
When testing the dispatcher we do not want to pollute the console with log messages.
However we will want to check that the correct messages are logged.

{% highlight js %}
function createTranscriptFunction(){
  var transcript = [];
  var func = function(value){
    transcript.push(value);
  }
  func.transcript = transcript;
  return func;
}
{% endhighlight %}

Jasmine after test check if test status is failed.
{% highlight js %}
describe("Dispatcher", function(){
  it("should inform of the dispatched action", function(){
    dispatcher.dispatch("action");
    expect(logger.info.transcript[0]).toBe("action");
    expect(logger.info.transcript[0]).toBe("action");
  });
});
{% endhighlight %}

### Controlled logging
In larger systems if is helpful to add labels to logs.
This can make log messages much more readable by including which section of the codebase was responsible for the log message.
In development logging every message is normal to help with debugging.
In production debug messages are normally over kill and we may only want to report logs at warning level or higher.
As we pass a logger to all parts of the codebase we can prevent info messages being logged by creating a debug method that does nothing.
We can leave the code that calls `logger.info` in place.

{% highlight js %}
// development
var logger = {
  info: function(message){

    console.info("logger", message);
  },
  warn: function(message){
    console.warn("logger", message);
  }
};

// production
var logger = {
  info: function(message){
    // No op ignore message
  },
  warn: function(message){
    console.warn("logger", message);
  }
};
{% endhighlight %}


### Reported errors

Throwing an error is a form of side effect.
To control this I replace calls to throw errors with calls on the passed in logger.
{% highlight js %}
throw new Error("some error");
// replaced with
logger.error(new Error("some error");)
{% endhighlight %}

This increases control again.
We can decide what behaviour should be the result of a call to `logger.error`
In testing we can throw the error that was passed in.

*The stack trace of an error is formed when the error is created and not when it is thrown.
This means that if we pass the error to a logger which then throws it we still get the correct stacktrace.*

In production we should not often throw errors.
In the case of our dispatcher one callback might throw an error but we want to dispatch the action to the other callbacks.
In this scenario our page might fail only in one area while the rest continues responding to the user.
We don't want the error to be unreported but instead of throwing it we can send it to our bug tracking system.

{% highlight js %}
var testLogger = {
  error: function(err){
    throw err;
  }
};
var testLogger = {
  error: function(err){
    MyErrorServer.notifyException(err);
  }
};
{% endhighlight %}

In development we can log or throw the error dep

### Is it worth it.

After having used this on a couple of projects I have found it surprisingly useful.
There are a number of things to bear in mind.

Passing a context object as the last argument is a pain if you are in the habit of creating functions that
accept a variable number of arguments.
If functions can cause a lot of different side effects then you will be passing many objects to function.
This is a pain but ultimatly a good thing because a function that needs acccess to more than two external effects is probably doing too much.
Leaving debug comments in your codebase makes is a bit larger. Not really a problem and if it turns out to be a problem the way to remove these is with a build step.
Set loglevel from query String, if loglevel not found use production logger.
Allows me to access the logs on the production site.
