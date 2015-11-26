---
layout: post
title: Dreamcoding my ideal language.
description: Contriving four language features by wishful thinking.
date: 2015-11-8 06:56:05
tags:
- Functional Programming
- Immutability
- Design
author: Peter Saxton
---

**Dreamcoding is the process of writing down the code you wish to write, without considering implementaion.
This post is what happened when I tried to apply that concept to a whole language.**

I was first introduced to the concept of dreamcoding on the [nobackend.org](http://nobackend.org/) site.
Conceptually it is very similar to ['coding by wishful thinking'](https://www.youtube.com/watch?v=gULkBpl3e7c) that I have seen from Corey Haines.

### What I want

In my career I have worked with JavaScript, Ruby and Python, most recently I have been working with [Elixr](http://elixir-lang.org/).
In my free-time I have experimented with yet more.
These are all great languages yet there are certain features that might be useful that I have not found in any language.
These 'missing' features are what I present here.

**DISCLAIMER: These features might be harmful.**
I think all these features might be interesting but as I have not implemented them, so they could contain any problems.

All examples are highlighted as Ruby that's just because they look more interesting than un-highlighted and Ruby has a very free syntax.

#### 1. Named Curried Functions
My first feature is a function that is both curried and has named parameters.
Currying is the partial application of functions.
It allows for the very concise description of certain problems, for example mapping collections.
Named arguments in functions are expressive at communicating the intent of a function.
My hope is that named-curried functions could be both expressive and concise.

Such a combination might look like.

{% highlight rb %}
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
{% endhighlight %}

#### Immutable objects
Objects are a useful abstraction in many cases to model a domain.
In my experience, the most useful objects in domain modeling are small [value objects](http://insights.workshop14.io/2015/07/15/value-objects-in-ruby.html).
Immutable structures are cited to help improve the predictability of code, which I think is the case.

Most languages that are immutable are functional languages.
The pass data around and do not have a way to attach domain information to custom objects.
In the Ruby community there has been some discussion around immutability.
However because it is not immutable by default it is slow as certain optimisations cannot be made.

Simple immutable objects can just be modeled as partially applied modules.
Thought like this it would also be possible to have modules applied to different degrees, for example.

{% highlight rb %}
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
{% endhighlight %}

If logic is needed to instantiate objects this can be added as a function on the module.
For example if we wanted to create a user from a CSV row.

{% highlight rb %}
module User
  def from_csv_archive(archive_string)
    id, first_name, last_name = archive_string.split(' ')
    User(first_name: first_name, last_name: last_name)
  end
end
{% endhighlight %}

#### Side Effects always Dependencies
A well structured way of handling side effects is important when writing modular code.
I would like to see controlled access IO through an `IO` module that is not in the global namespace.
This IO module would be passed as in a function argument list, this would mean that two things.
First a fake implementation can always be passed in for the purpose of testing.
Second the language would be able to track its use and make optimisations of the code that did not call upon external IO.
Making IO always an explicit dependency might have advantages that the computer can assume functions without this declaration are pure.

{% highlight rb %}
IO.puts("Hello world!") # !! Error as no module IO found here

module ConsoleLogger
  def log(output, io=IO)
    io.puts(output)
  end
end

ConsoleLogger.log("Hello world!")
# Hello world!

// NullIO is a dummy object that has the same interface as the IO object.
ConsoleLogger.log(output: "Hello world!", io: NullIO)
{% endhighlight %}

#### Limited public interfaces
Controlling the public interface of a module is a good way to preserve modularity.
In some languages it is very easy to write code that relies on implementation details.
One way to control this would be to make all modules declare implementation of specific interfaces.

To go even further a function name can only be used once across all interfaces
For example, if a value has a `to_string` method then it is certain that the value implements the printable interface.
For this reason I want to experiment with structural typing where each function name is only able to refer to a single function signature within a certain context.
By default every function is private and they are only exposed through interfaces.

{% highlight rb %}
# Define a to_string interface that takes no arguments and returns a string
interface Printable
  to_string :: Any -> String
end

# Trying to create another interface with the string function is an error
interface Other
  to_string :: Any -> String
end
# !! raise SignatureAlreadyDefined

module User
  # Simply defining this function marks this module as printable
  def to_string(user)
    "user"
  end

  # By default this will be private as it is not in any defined interface.
  def private_method
    :some_constant
  end
end

User.implements(Printable)
# => true
{% endhighlight %}

### Conclusion
As a developer I am excited to build new things.
I'm sure I would enjoy the challenge of implementing my own language.
The reality is that this would be [yak shaving](http://www.hanselman.com/blog/YakShavingDefinedIllGetThatDoneAsSoonAsIShaveThisYak.aspx) of epic proportions.
So, for the moment, I have decided on dreamcoding only.

These four features interest me, and I will continue my search for them.
The next languages I want to investigate are Haskell, Scala and Typescript.

Do you see an obvious flaw in these features? Please do convince me.
Is one of these features already in existence? That is excellent I would love to know where and see some examples
