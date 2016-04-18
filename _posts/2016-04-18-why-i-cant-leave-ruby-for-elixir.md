---
layout: post
title: Why I can't leave Ruby for Elixir
description: Contriving four language features by wishful thinking.
date: 2016-04-18T20:24:05+00:00
tags:
- Functional Programming
- Immutability
- Design
author: Peter Saxton
---

This post is not about the Elixir community or job opportunities with Ruby.
It is not really about Ruby vs Elixir at all.
What I want to explain is why I am uncomfortable hitching my bandwaggon to the movement from OOP to FP.

### Background

The first language I used professionally was Ruby.
I have been working with it for several years.
In that time I have looked at many ways to improve code quality.
One set of guidelines for improving code is [Domain Driven Design(DDD)]().
This is a methodology for writing programs which reflect the domain of the problem they are trying to solve.
DDD is applicable to FP or OOP but is far more often discussed against an OOP background.

More recently I have been employed to write Elixir.
Elixir is a [proudly functional language]() that is built atop the Erlang virtual machine(beam).
It has some Ruby inspired syntax but few other similarities.
Working with this new language was a thorough introduction to functional programming.

Elixir has some powerful concepts such as pattern matching, immutability and pipelines.
These concepts are common across functional programming languages and rarer in OOP.
Further exploration showed few of these concepts were fundamentally tied to FP.

### Which to choose

When starting with Elixir one comment from Dave Thomas stuck in my mind.
He said "I don't think in objects, I think in processes".
I wondered which one I thought in or even if there is a best way to think.

Intriguingly DDD has a suggestion on whether it is better to think in objects or processes.
Does the client(or any non technical stakeholder) think in processes or objects?
The answer to that question is the answer to whether FP or OOP is a more suitable way to model the domain.

Immutability can help make code predictable.
Developing with Elixir demonstrates this well.
However Ruby can have immutable objects.
In the end it comes down to the domain to see which paradigm is more suitable.

Thinking in processes can be helpful, but many of these processes will involve well-defined domain objects.

Browse the *Catalogue*
View that *Item*
Update your *Basket*
checkout == create an *Order*

In my opinion neither paradigm is superior.
And my advice is to stop trying to pick a side and enjoy learning both.

### What's next for me
Erlang has some superpowers when it comes to writing parallel, fault tolerant code and Elixir inherits these powers.
If a system is meant to manage many demands concurrently then I would use Elixir.
A web socket server is an example of such a system.
For a program with less strenuous requirements I would likely choose Ruby.

Learning Elixir taught me many concepts.
Fundamentally my preference for Ruby is that I can use most of these Elixir concepts in Ruby.
Ruby's support for functional concepts is better than working with objects in Elixir.
