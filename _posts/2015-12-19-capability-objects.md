---
layout: post
title: Taming side effects.
description: Bringing predictability to JavaScript with Capability Objects
date: 2015-12-19 16:39:05
tags:
- Functional Programming
- Immutability
- Design
author: Peter Saxton
---

**Introducing capability objects to eliminate side effects in JavaScript functions**

Side effect free code is predictable, and therefore easier to test and reason about than code with side effects.
Some functional languages go to great lengths to control side effects, such as Haskell with its use of the IO Monad.
This post shows how we get the same advantages.
Capability objects provide a simple mechanism for controlling side effects in JavaScript.
Their use can improve the rationality, readability and reusability of program components.

### When is a function side effect free?
A function is isolated from side effects when:

  1. The only effect of it's execution is the return value (*side effect free*).
  2. The return value is always the same given the same arguments (*pure*).
  3. A function with both has referential transparency.

It is easiest to clarify these three with some examples.

{% highlight js %}
// Side effect free
function flip(){
  return Math.random() >= 0.5 ? "heads" : "tails";
}

// Pure
function addAndLog(a, b){
  console.log("adding", a, b);
  return a + b;
}

// Referentially transparent
function add(a, b){
  return a + b;
}
{% endhighlight %}

There are many ways a function can become coupled to the outside world.
Ways include accessing global variables such as the window object, logging and throwing errors.
Finally any function that accepts a function as an argument (i.e. callback) will become polluted if that callback is impure or has side effects.

A program cannot be useful without causing some side effect, it must at least display it's result.
The goal of a capability object is to separate the logic of a function from any effects.
This separation pushes code with side effects to the edges of our program and renders the core effectively isolated.

### Capability Objects and effectively isolated functions.
A capability object is an object on which some of its methods may be impure or have side effects.
An effectively isolated function is one that is pure when the capability object has only pure functionality and is side effect free when the capability object is side effect free.

We make our examples effectively isolated by rewriting them to take appropriate capability objects.

{% highlight js %}
function flip(randomiser){
  return randomiser.random() >= 0.5 ? "heads" : "tails";
}

function addAndLog(a, b, logger){
  logger.log("adding", a, b);
  return a + b;
}

function add(a, b){
  return a + b;
}
{% endhighlight %}

### Ok, but why?

To show  off the advantages of pure and side effect free functionality we need a more sophisticated example.
Let's start with a naieve implementation of a dispatcher.

{% highlight js %}
function Dispatcher(callbacks){
  this.dispatch = function(action){
    callbacks.forEach(function(callback){
      if (callback instanceof Function) {
        callback(action);
      } else {
        throw new TypeError("Callback is not a function");
      }
    });

    if (callbacks.length === 0) {
      console.warn(action);
    } else {
      console.info(action);
    }
  }
}
{% endhighlight %}

This dispatcher dispatches an action to each callback in a collection.
Meaningful errors should be the result of any callback that is not a function.
A log is required for each action that is dispatched.
Finally if there are no callbacks our log should be a warning as we never want a dispatched action to have no effect.

The naieve implementation is tightly coupled to the world outside its scope.
It creates side effects when throwing errors and writing log messages.

To isolate the dispatcher we make the following changes.

{% highlight js %}
function Dispatcher(callbacks, logger){
  this.dispatch = function(action){
    callbacks.forEach(function(callback){
      if (callback instanceof Function) {
        callback(action);
      } else {
        var err = new TypeError("Callback is not a function");
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

In this version there is not a single side effect.
A logger is passed as a dependency, so it is within scope when we call methods on it.
Instead of throwing errors the dispatcher now reports errors via the logger.

Let us examine the advantages of these changes.

#### Detailed logs
In larger systems it is helpful to add labels to logs.
One such label might be the section of code that logged the message.
This can be achieved by starting the dispatcher with a logger that always adds a label to its log messages.

{% highlight js %}
var logger = {
  info: function(message){
    console.info("The Dispatcher:", message);
  }
  // etc...
};
{% endhighlight %}

#### Clean logs
In production we might only be interested in messages that are a warning or an error.
To set this up only our logger needs to know about a log level and we can just dispense with logs that are not important.

{% highlight js %}
var logger = {
  info: function(message){
    if (LOG_LEVEL <= INFO_LOG_LEVEL) {
      console.info(message);
    }
  }
  // etc...
};
{% endhighlight %}

#### Tested logs
We have described a dispatcher that logs at different priorities an action that has no callbacks to one that has at least a single callback.
This is the kind of behaviour it would be nice to test.
Stubbing would have been the only option open to us to test the original code.

Stubbing methods on the global console object would require a cleanup step which can be problematic if the test fails.
The effectively isolated dispatcher can use a fake logger when we are testing the log messages.
This logger will record each call to a method we are interested in.

{% highlight js %}
// This returns a function that records each time it is called
function createTranscriptFunction(){
  var transcript = [];
  var func = function(value){
    transcript.push(value);
  }
  func.transcript = transcript;
  return func;
}

var logger = {
  info: createTranscriptFunction(),
  warn: createTranscriptFunction(),
}
{% endhighlight %}

#### Reporting errors

*The stack trace of an error is formed when the error is created and not when it is thrown.
This means that if we pass the error to a logger which then throws it we still get the correct stacktrace.*

In production it is not useful to throw errors.
The customer is unlikely to be interested in a stacktrace.
Additionally one bad callback is no reason to not call the other callbacks.
The best case is that one bad callback is not important and its effect may not be visible to the user.
If errors are occurring in production we want to be notified about them and let the user carry on.

Conversely in development errors should be thrown.
As developers we want notification of broken code as soon as possible.
The dispatcher does not need to be aware of a choice of error handling strategy.
Instead it can simply be passed to an appropriate logger.

{% highlight js %}
// Development
var logger = {
  error: function(err){
    throw err;
  }
};

// Production
var logger = {
  error: function(err){
    MyErrorServer.notifyException(err);
  }
};
{% endhighlight %}

### Is it worth it.

So far only advantages have been highlighted, but what are the costs.

Passing around capability objects requires a bit more setup.
Failing to pass in a logger can result in code failing even if all the business functionality is present.
An option to handle when a logger is not present is to fallback to using the global console.
I do not do this as I think that a missing logger is something that I want to be a failure and in production missing logs is a problem to which I want to be alerted.

Leaving debug comments in your codebase makes it a bit larger.
Not really a problem as the amount of code is so small.
If it turns out to be a problem the way to remove the debug calls is with a build step.

If a function causes many different side effects then it will require several capability objects.
This is a pain but ultimately a good thing.
Any function that needs access to more than two external resources is probably doing too much.

http://joeduffyblog.com/2015/11/10/objects-as-secure-capabilities/
http://blog.jenkster.com/2015/12/what-is-functional-programming.html
