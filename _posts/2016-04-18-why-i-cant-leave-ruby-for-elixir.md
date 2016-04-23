---
layout: post
title: Why I won't leave Ruby for Elixir
description: My take on Functional Programming vs Object Oriented Programming.
date: '2016-04-18T20:24:05+01:00'
tags:
- Functional Programming
- Object Oriented Programming
- Immutability
author: Peter Saxton
---

This post is not about the Elixir community or job opportunities with Ruby.
It is not really about Ruby vs Elixir at all.
What I want to explain is why I am uncomfortable hitching my bandwaggon to the movement from Object Oriented Programming(OOP) to Functional Programming(FP).

### Background

The first language I used professionally was Ruby.
I have been working with it for several years.
In that time I have looked at many ways to improve code quality.
One set of guidelines for improving code is [Domain Driven Design(DDD)](http://insights.workshop14.io/2015/07/14/domain-driven-design-introduction.html).
This is a methodology for writing programs which reflect the domain of the problem they are trying to solve.
DDD is applicable to all programming paradigms but is most often discussed in an OOP context.

More recently I have been employed to write Elixir.
Elixir is a [proudly functional language](http://elixir-lang.org/) that is built atop the Erlang virtual machine(beam).
It has some Ruby inspired syntax but few other similarities.
Working with this new language was a thorough introduction to functional programming.

Elixir has some powerful concepts such as pattern matching, immutability and pipelines.
These concepts are common across many functional programming languages but much rarer in most object oriented languages.

However as I became more familiar with these concepts I could find no good reason why they were limited to functional languages.
In particular creating immutable objects certainly is possible and seamed to be valuable.

### Which to choose

So I find myself in the situation do I want to program in a functional language or an object language.

When starting with Elixir one comment from Dave Thomas stuck in my mind.
He said "I don't think in objects, I think in processes".
I wondered which one I thought in or even if there is a best way to think.

Intriguingly I think DDD has a suggestion on whether it is better, as a programmer, to think in objects or processes.
Ask the following question.
*Does the client(or any non technical stakeholder) think in processes or objects?*
The answer to that question will be the same answer to whether FP or OOP is a more suitable way to model their domain.

I certainly value immutability in a programming language and would agree that it can help make code predictable.
My time developing with Elixir clear demonstrated this.
However Ruby can have immutable objects.
So in the end it comes down to the domain to see which paradigm is more suitable.

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
For a program with less strenuous requirements I would prefer to use Ruby.

So I have a preference for Ruby.
This is because; Ruby's support for functional concepts is better than working with objects in Elixir.
In Ruby I can leverage most of the lessons I learned from my time in with functional programming.

### Best of both
Some talks discussing immutability and objects.

- [Blending Functional and OO Programming in Ruby](https://www.youtube.com/watch?v=rMxurF4oqsc)
  Great talk from [Piotr Solnica](https://twitter.com/_solnic_) about his exploration of this area.
- [Boundaries](https://www.youtube.com/watch?v=yTkzNHF6rMs) Immutable OO as FauxO, brilliance from [Gary Bernhardt](https://twitter.com/garybernhardt)
