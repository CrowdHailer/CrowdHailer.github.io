---
layout: post
title: Three JavaScript frameworks for 2016
description: Cutting edge ideas from emerging JavaScript frameworks.
date: 2016-03-23 14:00:00
tags:
- JavaScript
- Design
author: Peter Saxton
---

**Three modern JavaScript frameworks that are interesting and have something to teach you.**

Keeping track of the latest JavaScript frameworks is exhausting.
It is difficult to separate the genuinely interesting from the crowd.
Recently I have had some time to explore the current offerings.
This selection are my favourite and worth a second look.

### [Redux](http://redux.js.org/)

##### Flux -> Reflux -> Redux

![Flux logo](http://img.stackshare.io/service/1275/flux.png)
Flux was coined by Facebook to describe the recommended architecture to use with React.

The key concept is that of a unidirectional dataflow.
Actions cause updates in a store(aka model).
The model generates a view and this finally updates the DOM.
User interactions are mapped to actions to close the loop.

Redux is a recent addition to the flux family tree.
It develops on flux by confining all application state to a single store.
This sounds a drastic limitation but creates some interesting payoffs.
One of these benefits is that Redux offers a time-travelling debugger.
This works by keeping a record of each version of the state and allowing a debugger to replay through this history.
It is invaluable when debugging a process with many steps.

To get a thorough introduction to Redux there is a series of explanatory videos.
These run through all the basic concepts very quickly.

![Cycle logo](http://cycle.js.org/img/cyclejs_logo.svg)

### [Cycle](http://cycle.js.org/)

##### Haskell -> ReactiveX -> Cycle
Cycle takes inspiration from functional technologies such as Haskell and ReactiveX.
Don't be deterred by these advanced forebears.
Only a limited number of concepts are used and they are explained when needed.

Cycles design starts with a proposition - what if the user was a function?
The result is a unidirectional data flow, in common with FLux.
However all key components are reactive instead of proactive.
Much of Cycle is built on observables, which are leveraged from RX.js.

Modelling the system as an observable to a user is certainly unusual.
To me the observable pattern is useful when the object being observed does not care about the behaviour (or even existence) of any observers.
This is not the case for any real system.
The user cares quite a lot about whether the program responds or not to its actions.

That said there are a few examples where this approach results in very elegant programs.
The concept is well explained on the Cycle website, have a read through and decide if your system makes sense as an observable.

![Vue logo](http://vuejs.org/images/logo.png)

### [Vue](http://vuejs.org/)

##### Backbone -> MV* -> MVVM

Vue uses the Model-View-ViewModel(MVVM) pattern.
It is a focused toolset for dealing with the View and ViewModel layer.
A few further core components of an app are included, such as a router.
Apart from these the core business logic is completely in the hands of the developer.

Vue evolves the MVVM pattern forward in several respects.
Complete widgets can be encapsulated in single `.vue` files
These files contain HTML, CSS and JS.
The databinding syntax that glues the View to ViewModel is concise and explicit.
These changes create a powerful framework that will be familiar to developers who have used other MV* frameworks.

Vue rides the line between library and framework quite expertly.
I particularly like the way it does not interfere with implementing the core application logic.
It is quite possible to implement a flux architecture within a Vue project.
Important for your project to remain buzzword compliant.

The documentation does a great job of describing the MVVM pattern.
Particularly valuable when many explanations muddle all the various MV* patterns together.

### Conclusion

All of these projects have ideas I have been able to use going forward.
Perhaps the most significant for me was having one store for the state of an app.
In my current project the single store has just been a wrapper around the history API.
Encoding the entire app state in the URL has given the app the some nice properties.
First is refreshing the page will not lose any information.
Second the back button neatly steps through the history of the application.

So which of these three should you use?
All of them, in the correct situation.
They all have great documentation and learning them is valuable even if you do not use them.

If my next project had lots of collections, I would use Vue to create coherent components.
But my design would be inspired by Redux and reduce the number of stateful components.
For a more interactive product, I would employ Cycle.
The observable model would be very nice for handling rich input from the user.

Well those are my three favourites at the moment;I am sure you have others that you can suggest.

<!-- Put as an example in the links -->
Herinrik Jorteg created an example where the router was just a view into the state.
link to old webcomponents frp post.
