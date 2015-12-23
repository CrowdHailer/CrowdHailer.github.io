---
layout: post
title: Why I can't leave Ruby for Elixir
description: Contriving four language features by wishful thinking.
date: 2015-11-26 16:39:05
tags:
- Functional Programming
- Immutability
- Design
author: Peter Saxton
---

**tl:dr Object Oriented Programming(OOP) vs Functional Programming(FP) is a distraction.
Both paradigms have there strength and can often be used together.**

This post is not about community or job opportunities or tooling.
It is not really about Ruby vs Elixir at all.
What I want to explain is why I am uncomfortable hitching my bandwaggon to the movement from OOP to FP.

My background is in Ruby.
It was the first language I used professionally and I have been working with it for several years now.
In that time I have looked at many ways to improve code quality.
Most often I was the person maintaining the code I wrote so very quickly I wanted to be writing the best code possible.
To this end I spent much of last year exploring [Domain Driven Design(DDD)](link).
 is a methodology for writing maintaining programs.

More recently I have been working with Elixir.
Elixir is a proudly functional language that is build atop the Erlang virtual machine(beam).
It has some Ruby inspired syntax but few other similarities.
Working with this new language was a thorough introduction to many of the ideas important to functional programming.

Some of the more eye opening ideas were pattern matching, Immutability and pipelines. Even Monads
As I explored them further though it became apparent that none of these were fundamentally opposed to Objects.
In particular the ideas from DDD seamed to be above technical considerations like OOP v FP.
DDD despite being agnostic to technology is firmly rooted in the OOP world.

When I started with elixir one comment from Dave Thomas had stuck in my mind.
It was this "I don't think in objects I think in processes".
What was interesting was that DDD had an answer to this.
Does your client(or any non technical stakeholder) think in processes or objects.
As our programs purpose is to model a domain the answer to that question would give you which bits of your system should be functional or object based.

When cast in this light it became clear that both views where useful.
Ideas like event sourcing can blur the line further.
There is always an object

Browse the *Catalogue*
View that *Item*
Update your *Basket*
checkout == create an *Order*

So stop trying to pick a side and enjoy learning both.

### Whats next for me
Erlang has some superpowers when it comes to writing parallel, fault tolerant code, Elixir inherits these powers
For anything with less rigourous requirements I will prefer Ruby.
Elixir taught me many things that I can use in Ruby, an apprechiation for immutable data structures among them.
However the fundamental factor is that Ruby's support for functional paradigms is better that Elixir's support for working with object.
It is also clear that this will not change any time soon.
