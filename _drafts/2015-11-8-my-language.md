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
I think all these features might be interesting but as I have not implemented them they could contain any problems.

All examples are highlighted as Ruby thats just because they look more interesting than unhighlighted and Ruby gives alot of freedom.

#### 1. Named Curried Functions
Currying is the partial application of functions.
Sophisticated concepts can be expressed concisely with curried functions.
Named arguments in functions clearly express the intent of code.
If we combine both might if be possible to have expressive concise code.
Such a combination might look like.

```ruby
def divide(numerator, denominator)
  numerator / denominator
end

divide(numerator: 4, denominator: 2)
# => 2

half = divide(denominator: 2)
half(numerator: 6)
# => 3

invert = divide(numerator: 1)
invert(denominator: 4)
# => 0.25

# Perhaps if the function has arity 1 then the name of the final argument can be omitted
invert(4)
# => 0.25
```

#### Immutable objects
Objects a useful abstraction in many cases to model a domain.
The most useful objects are normally small [value objects]().
Most immutable languages just pass data.
They do not have a way to attach domain information to custom objects.

We can replace Classes inheritance to simply create objects as partially applied modules. It would also be possible to have modules applied to different degrees

```rb
module User
  def first_name(first_name)
    first_name
  end

  def name(first_name, last_name)
    first_name ++ " " ++ last_name
  end
end

# Here we just ignore the unexpected argument passed in.
User.first_name(first_name: "Stuart", last_name: "Little")
# => "Stuart"

User.name(first_name: "Stuart", last_name: "Little")
# => "Stuart Little"

stuart = User(first_name: "Stuart", last_name: "Little")
stuart.name
# => "Stuart Little"

littles = User(last_name: "Little")
# => {User, {last_name: "Little"}}

littles.name(first_name: "Stuart")
# => "Stuart Little"
```

If logic is needed to instantiate objects this can be added as a function on the module.
For example if we wanted to create a user from a CSV row.

```rb
module User
  def from_csv_archive(archive_string)
    id, first_name, last_name = archive_string.split(' ')
    User(first_name: first_name, last_name: last_name)
  end
end
```

#### Side Effects always Dependencies
A well structured way of handling side effects is important when writing modular code.
If we access IO through an `IO` module it should not be in the global namespace.
But it should be possible to access it in a function argument list.
Making IO always an explixit dependency might have advantages that the computer can assume functions without this declaration are pure.

```rb
IO.puts("Hello world!") # !! Error as no module IO found here

module ConsoleLogger
  def log(output, io \\ IO)
    io.puts(output)
  end
end

ConsoleLogger.log("Hello world!")
# Hello world!
ConsoleLogger.log(output: "Hello world!", io: NullIO)

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
