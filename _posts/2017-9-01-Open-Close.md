---
layout: post
title:
tags: solid
---
![Contra Boss Graphic](/images/contra-boss.png)

In my last [post](/Liskov) about SOLID, I went over the Liskov Substitution Principle (LSP). If you'll recall, Liskov stated that you should be able to use the derived class without breaking the business logic of the parent class. I briefly went over the typically used example of a rectangle vs. square and how the `setWidth` and `setLength` methods of `rectangle` wouldn't make sense for the subtype `square` since the assumption for `rectangle` is that both of those properties are independently settable.

We then discussed a scenario in the two player arcade game Contra where you could have a `Commando` class along with `PlayerOne` and `PlayerTwo` subclasses. Contra didn't have medics in the game. Instead, players were expected to navigate their way around numerous enemy mutants, soldiers, and aliens created by Red Falcon without getting hit. Assuming you didn't have the konami code at your disposal, having a medic to repair your health would have been helpful in the battles against the many enemy bosses.

We violated Liskov's LSP in our the last post by having the medic return an unexpected type (hash instead of string). This time, let's learn about the Open Closed Principle and how it might be applied to our Commandos.

The Open Closed Principle is credited to Bertrand Meyer and discussed in his 1988 book *Object Oriented Software Construction*. He states:

>A satisfactory modular decomposition technique must satisfy one more requirement: It should yield modules that are both open and closed.
  * A module will be said to be open if it is available for extension. For example, it should be possible to add fields to the data structures it contains, or new elements to the set of functions it performs.
  * A module will be said to be closed if it is available for use by other modules. This assumes that the module has been given a well-defined, stable description (the interface in the sense of information hiding). In the case of a programming language module, a closed module is one that may be compiled and stored in a library, for others to use. In the case of a design or specification module, closing a module simply means having it approved by management, adding it to the project's official repository of accepted software items (often called the project baseline), and publishing its interface for the benefit of other module designers.

  At first, it sounds quite confusing to be both open and closed since they seem like total opposites. Its important to understand the meaning each in the context of software modules or objects. An object can be open for modification when you can add fields to it and have it still work. When Meyers is referring to a module being closed for modification, that's just want we are doing with our Contra Commandos. As long we don't change the interface of the parent Commando class, it remains closed for modification as we see in the PlayerOne and PlayerTwo subclasses. When we need to change the Commando base class to implement more functionality is when that class ceases to be closed for modification. Alternatively we can inherit from Commando and modify the behavior in the subclass.
