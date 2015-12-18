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

### [Redux](http://redux.js.org/)

##### Flux -> Reflux -> Redux

![Flux logo](http://img.stackshare.io/service/1275/flux.png)
The flux architecture was labeled as such by Facebook.
They coined the term to describe a recommended setup when using React.

The key tenant is a unidirectional dataflow. Actions cause updates in a store(aka model).
The model generates a view and this finally updates the DOM.
User interactions are mapped to actions to close the loop.

Redux is one of the latest iterations on this idea.
It proposes a single data store for all state in the application.
This sounds a drastic limitation yet has some interesting payoffs.
Redux offers a time-travelling debugger.
Invaluable when debugging a process with many steps.

To get a quick introduction watch the excellent series of explanetory videos available.


![Cycle logo](http://cycle.js.org/img/cyclejs_logo.svg)

### [Cycle](http://cycle.js.org/)

##### Haskell -> ReactiveX -> Cycle
Cycle takes inspiration from functional technologies such as Haskell and ReactiveX.
Don't be detered by these advanced concepts as there is a limited number and they are explained when needed.

Cycles design starts with the question, what if the user was a function.
The result for this frame work is that all key components are reactive.
Much of Cycle is built on observables, which are leveraged from RX.js.

Modeling the system as an observable to a user is certainly unusual
To me the observable pattern is useful when the object being observed is not aware or caring about the behavior of its observers.
This is not the case for any real system where the user cares quite a lot about whether the program responds or not to its actions.

That said there are a few examples where this approach results in very elegant programs.
The concept is well explained on the cycle website, have a read through and decide if your system makes sense as an observable.

![Vue logo](http://vuejs.org/images/logo.png)

### [Vue](http://vuejs.org/)

##### Backbone -> MV* -> MVVM

Vue uses the Model-View-ViewModel(MVVM) pattern.
Focused on dealing with the View and ViewModel layer.
It rides the line between library and framework quite expertly.
A router is included yet leave the core business model for the user to implement.

Vue will be more familiar to developers who have used MV* frameworks in the past.
Vue is decended from existing MV* frameworks.
This background will make it familiar to many developers, yet it moves forward in several areas.
Widgets can be encapsulated in single `.vue` files
These component files contain HTML CSS and JS.
It has a template syntax that is concise and well reasoned about.


I particularly like the way it does not interfere with implementing the core application.
A few choices and the domain model will implement the flux architecture.
Important for your project to remain buzzword compliant.

The documentation is excellent and it describes the MVVM pattern well.
Particularly valuable when most explinations muddle all the MV* frameworks together.

### Conclusion

All of these projects have ideas I have been able to use going forward.
Perhaps the most significant for me was having one store of state in the app.
Herinrik Jorteg created an example where the router was just a view into the state.
In my current project the entire app state is encoded in the url.
Refreshing the page will not loose any information.

So which do I recommend, all of them.
They all have great documentation, learning about them is valuable even if you do not use them.

If my next project had lots collections, I would use Vue to create coherent components.
But my design would be inspired by redux and reduce the number of stateful components.
For a more interactive product, I would employ cycle.
The observable model would be very nice for handling rich input from the user.

Well those are my three favourites at the moment I am sure you have others that you can suggest. In my next post I hope to talk more about what I have been working. on.
