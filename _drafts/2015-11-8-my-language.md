---
layout: post
title: The next technology bubble
description: Why the Internet everywhere is not the same as the Internet anywhere
date: 2015-11-8 06:56:05
tags: Language
author: Peter Saxton
---

### The temptation
As a developer I am excited to build new things.
The reality is that this is not always the best thing to do.
Certainly when developing systems for production using existing tools is preferable.
The lessons learned by many developers from many mistakes you don't want to make yourself are within these tools.

A complete programming language is something that I know I do not need to build

### My Values
These are the things that I currently value in a programming language.
- As human readable as possible
- Immutability by default
- Side effects must contained and be possible to substitute or fake
- Structural typing not classification typing
What is less important
- Functional programming vs Object Oriented Programming.

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
