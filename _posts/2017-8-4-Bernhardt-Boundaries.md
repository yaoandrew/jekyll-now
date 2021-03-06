---
layout: post
title: Gary Bernhardt on Boundaries
---
![Bernhardt Presentation Cover](/images/boundaries.png)


In Bernhardt’s [video on Boundaries](https://www.destroyallsoftware.com/talks/boundaries), Gary begins by discussing test doubles. Specifically, he’s talking about stubs and mocks. I later read that test doubles can also include fake objects and spies. This was also covered a bit in Justin Searle’s [video on Testing](http://blog.testdouble.com/posts/2015-11-16-how-to-stop-hating-your-tests). He goes over certain benefits of using test doubles but brings up the fact that what’s tested in dev may not match the implementation in production.

There are multiple ways to address this. One could write even more tests to make sure the boundaries are correct, use a tools approach with something like rspec-fire which makes sure all the methods on the real object match the methods on the mock. You could create a mock which is a subclass of the real object and rremove all the logic in the methods or you could do an integration test, which isn’t ideal since the path count grows exponentially making the test suite runtime extra long.

He then asks the question about values and how we could test something in isolation. What would it take to be able to test something that takes a value and returns a value (like a pure function)? Bernhardt goes over how data and code are combined or separated across 3 primary programming paradigms (procedural, OO, and functional) and introduces us to his own called FauxO which combine elements of both OO and functional.

He begins to introduce the concept of [functional core, imperative shell](https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell) where all of the decisions/logic are contained in the functional core. Isolated bits of data, like collections of pure functions. They can be simply tested and isolated unit testing is good for this. Surrounded by the imperative shell which has lots of dependencies but few differing paths. Integration testing is good for this. It can test the communication between all the pieces. He briefly touches on how this type of design makes concurrency easier. I’ve been playing around with Elixir so I recognize the actor model a bit although, I’m not that deep into OTP and the [Erlang-y parts](http://theerlangelist.blogspot.com/2013/01/actors-in-erlangelixir.html) yet.
