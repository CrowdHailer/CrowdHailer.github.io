---
---

Some event sourcing links to go through

genomu implementation in elixir

https://github.com/genomu/genomu

and talk
http://www.erlang-factory.com/conference/SFBay2013/speakers/YuriiRashkovskii
https://dl.dropboxusercontent.com/u/923732/genomu-efsf13/index.html#/


event sourcing on rails

http://codetunes.com/2014/event-sourcing-on-rails-with-rabbitmq/


Stream processing, Event sourcing, Reactive, CEP… and making sense of it all
http://blog.confluent.io/2015/01/29/making-sense-of-stream-processing/

Datomic vs Event Store
http://www.slideshare.net/jankronquist/java-zone-2013-immutable-data-stores

coffee script evvent store eventric
https://github.com/efacilitation/eventric

js - sourced
https://github.com/mateodelnorte/sourced

the CQRS diet
http://www.slideshare.net/cavalle/the-cqrs-diet?related=1

ruby example
https://github.com/cavalle/banksimplistic

clarified CQRS
http://www.udidahan.com/2009/12/09/clarified-cqrs/

mvc evolved
http://www.slideshare.net/jbsen/mvc-evolved

mixter example several languages
https://github.com/DevLyon/mixter

Lagom example https://github.com/dotta/activator-lagom-scala-chirper

Build a wage reporter similar to the goodlord referencing system. Applicant updates income history, reports are built from requirements

persistent actor game of life

erlang otp 
```erlang
handle_command(command, _from, state) ->
  {:ack, [event1, event2]},
handle_command(command, _from, state) ->
  {:error, [violation1, violation2]}.
  
apply_event(event, state) ->
  {:ok, new_state, timeout},
apply_event(event, state) ->
  {:error, reason}.
```
