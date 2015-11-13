---
layout: post
title: Dreamcoding my ideal language.
description: Devising a language by wishful thinking
date: 2015-11-8 06:56:05
tags: Language
author: Peter Saxton
---

Dreamcoding is the process of writing down the code you wish to see, without consideration of actually making it work.
This post is what happened when I tried to apply that concept to a whole language.

As a developer I am excited to build new things.
A complete programming language I'm sure would be fun to build.
The reality is that this would be [yak shaving]() of epic proportions, so I decided to dreamcode my language instead.

In my career I have worked with JavaScript, Ruby and Python, most recently I have been working with [Elixr]().
Elixir is a great language, it has really stretched me to think about what it meant to have concurrency in a systems.
<!-- I am interesting in combining the actor model with a type system and some Object Oriented ideas for handling side effects. -->

I was first introduced to the concept of dreamcoding on the [nobackend.org]() site.
https://www.youtube.com/watch?v=gULkBpl3e7c
Conceptually it is very similar to 'coding by wishful thinking' that I have seen from Corey Haines.

### What I want
So to start with I need to be able to express what my dream language would look like.
These are some of the things that I value in a programming language.

I value code that is
- clear and concise, not concise at the cost of clarity.
- low on surprises, read have immutable data structures
- is easy to isolate and has controlled side effects
- quick to express domain concepts

What I want to add quickly is that I don't think Functional programming vs Object Oriented Programming is a very interesting discussion.
I see more similarities than differences.

**DISCLAIMER: These features might be harmful.**
I think all these features might be interesting but as I have not implemented them they could contain any problems

#### Named Curried Functions
When working with first class functions the ability to partially apply(curry) functions is very useful.
Named arguments are helpful in expressing the intent of code.
To combine both might look something like the following.

```
def divide(numerator, denominator)
  numerator / denominator
end

divide(numerator: 4, denominator: 2)
# => 2

half = divide(denominator: 2)
half(numerator: 6)
# => 3

# perhaps is the function has arity 1 then the name of the argument can be omitted
half(6)
# => 3
```

#### Objects as Partially applied Modules
I can't remember the source but I had immutable objects described as partially applied modules.
Calling a module with some arguments will return an 'instance' of that module.

```
module User
  first_name
  last_name

  def name(first_name, last_name)
    first_name ++ " " ++ last_name
  end
end

User.first_name(first_name: "Dave")
# => "Dave"

User.name(first_name: "Dave", last_name: "Little")
# => "Dave Little"

dave = User(first_name: "Dave", last_name: "Little")
# => {User, {first_name: "Dave", last_name: "Little"}}
dave.name
# => "Dave Little"

littles = User(last_name: "Little")
# => {User, {last_name: "Little"}}

littles.name(first_name: "Dave")
# => "Dave Little"
```

#### Object instantiation
Any behaviour that is needed in the instantiation process of an object can be done my a module function
```
module User
  def new(first_name, last_name)
    # validate length of last name
    User(first_name: first_name, last_name: last_name)
  end
end
```

```
module User
  {first_name:Name, last_name:Name} -> instance of User
  def new(first_name:Name, last_name:Name)
    {User, {first_name: "Dave", last_name: "Little"}}
  end
end
```



#### Side Effects always Dependencies
When defining functions the context does not include access to an IO module.
This IO module must be an explicit dependency.
For testing purposes side effects can alway be contained.

```
module Greeter
  def welcome(guest, logger)
    logger.log("hello #{guest.name}")
  end
end

module ConsoleLogger
  def log(string, io \\ IO)
    io.puts(string)
  end
end

ConsoleGreeter = Greeter(logger: ConsoleLogger)
ConsoleGreeter.welcome({name: "test name"})

ConsoleGreeter.welcome({colour: "brown"})
# Should fail at compile time as the structure lacks a name method
```

interfaces are global
```
interface Printable
  def to_string
  end
end
Printable is an interface on the world
implement World.Printable

# Could just be a module with some type specs
Weird.interface Printable
  to_string :: Any -> Num
end
in bounded contexts use Weird.Printable


Weird.module Weird
  def to_string({value: _value})
    5
  end
end

Weird.Weird
```

```
interface Enumerable
  to_enum :: (Any) -> func/0

end

module Enumerator
  next :: (Enumerator[Any]) -> {Any, Enumerator[Any]}
end
module Each
  def map(enumerator, mapper)
    do_map(enumerator: enumerator, mapper: mapper, result: [])
  end

  defp do_map(enumerator, mapper, result)
    {value, enumerator} = enumerator.next
    result = [mapper(value) | result]
    do_map(enumerator: new_enumerator, mapper: mapper, result: result)
  mismatch {Enumerator, :no_match}
    result
  end
end
```
