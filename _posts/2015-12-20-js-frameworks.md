---
layout: post
title: Three JavaScript frameworks for 2016
description: Opinions on a few of the more interesting JS projects.
date: 2015-11-26 16:39:05
tags:
- JavaScript
- Design
author: Peter Saxton
---

**Three modern JavaScript frameworks that are interesting and have something to teach you.**

As we know keeping track with the latest JavaScript framework is exhausing.
They come out much quicker than anyone can keep up with.
Recently I have had sometime to explore some of the offerings and this selection are worth a second look.
Each is a well thought through effort, that.
Most importantly they all have great documentation, learning about them is valuable even if you do not use them.

###  [Redux](http://redux.js.org/)

##### Flux -> Reflux -> Redux

![Flux logo](http://img.stackshare.io/service/1275/flux.png)
The flux architecture was labeled as such by Facebook.
They coined the term to describe a recommended setup when using React.

The key tennant is a unidirectional dataflow. Actions cause updates in a store(nee model).
The model generates a view and this finally updates the DOM.
User interaction is mapped to actions to close the loop.

Redux is one of the latest iterations.
It proposes a single data store for all state in the application.
This drastic limitation has some interesting payoffs.
All buisness logic is separated state management, sanitising your system.
It is also integral to putting together a timetravelling debugger.
Invaluable when debugging a process with many steps.

The documentation contains a really sucinct series of videos that explain the concept.

Downside Single global state can grow when inluding rich text editing.

![Cycle logo](http://cycle.js.org/img/cyclejs_logo.svg)

### [Cycle](http://cycle.js.org/)

##### Haskell -> ReactiveX -> Cycle
Cycle asks the question what if the user was a function.
The result for this frame work is that all key components are implemented as reactive.
This means lots of observables (Cycle is layered atop RX.js).
Modeling the user as an observable is certainly unusual.

Semantically I am not convinced that the system really should be an observable.
To me the observable pattern is useful when the object being observed is not aware or caring about the behavior of its observers.
This is not the case for any real system where the user cares quite a lot about whether the program responds or not to its actions.


![Vue logo](http://vuejs.org/images/logo.png)

### [Vue](http://vuejs.org/)

##### Backbone -> MV* -> MVVM

A more familiar library to those who have developed in one of the MV* frameworks that make up its ancestry.
Vue focuses on dealing with the view and ViewModel layer.
Something I like as it does not get in the way when implementing the rest of the application.
There is some history and the template syntax is concise and well reasoned about.
Again the documentation is excellent it describes why it is an MVVM framework in particular where much documentation muddles all the MV* frameworks together.
If even goes so far as to say that a few choice in your domain model will allow you to create a flux architecture. (Very important to be buzzword compliant).

### Conclusion

All of these projects have ideas I have been able to use going forward.
Perhaps the most significant for me was having one store of state in the app.
Herinrik Jorteg showed an example where he made the router just a view into this state.
In my current project the app state is encoded completly in the url and refreshing the page will not loose any information.

So which do I recommend. All of the above.

If my next project was a had lots lists of items I would employ Vue, and its nice encapsulation of components.
But I would let my design be inspired by redux and reduce stateful components in my system.
Perhaps for a more interactive project, I would employ cycle where the observable model would be very nice for handling rich input from the user.

Well those are my three favourites for the moment I am sure you have others that you can suggest. In my next post I hope to talk more about what I have been working. on.
