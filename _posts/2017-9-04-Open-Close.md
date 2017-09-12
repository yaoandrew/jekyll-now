---
layout: post
title:
tags: solid
---
![Contra Boss Graphic](/images/contra-boss.png)

In my last [post](/Liskov) about SOLID, I went over the Liskov Substitution Principle (LSP). If you'll recall, Liskov stated that you should be able to use the derived class without breaking the business logic of the parent class. I briefly went over the typically used example of a rectangle vs. square and how the `setWidth` and `setLength` methods of `rectangle` wouldn't make sense for the subtype `square` since the assumption for `rectangle` is that both of those properties are independently settable.

We then discussed a scenario in the two player arcade game Contra where you could have a `Commando` class along with `PlayerOne` and `PlayerTwo` subclasses. Contra didn't have medics in the game. Instead, players were expected to navigate their way around numerous enemy mutants, soldiers, and aliens created by Red Falcon without getting hit. Assuming you didn't have the konami code at your disposal, having a medic to repair your health would have been helpful in the battles against the many enemy bosses.

We violated Liskov's LSP in our the last post by having the medic return an unexpected type (hash instead of string). This time, let's learn about the Open Closed Principle and see how it might apply to our Commandos.

The Open Closed Principle is credited to Bertrand Meyer and discussed in his 1988 book *Object Oriented Software Construction*. He states:

>A satisfactory modular decomposition technique must satisfy one more requirement: It should yield modules that are both open and closed.
  * A module will be said to be open if it is available for extension. For example, it should be possible to add fields to the data structures it contains, or new elements to the set of functions it performs.
  * A module will be said to be closed if it is available for use by other modules. This assumes that the module has been given a well-defined, stable description (the interface in the sense of information hiding). In the case of a programming language module, a closed module is one that may be compiled and stored in a library, for others to use. In the case of a design or specification module, closing a module simply means having it approved by management, adding it to the project's official repository of accepted software items (often called the project baseline), and publishing its interface for the benefit of other module designers.

  At first, it sounds quite confusing to be both open and closed since they seem like total opposites. Its important to understand the meaning of each in the context of software modules or objects. A module can be open for extension when you can add fields to it and have it still work. When Meyers is referring to a module being closed for modification, that's just want we are doing with our Contra Commandos. As long we don't change the interface of the parent Commando class, it remains closed for modification as we see in the PlayerOne and PlayerTwo subclasses.

  When we need to change the Commando base class which requires us to modify the subclasses that implement it, that is when the class ceases to be closed for modification. Alternatively, we can inherit from Commando and modify the behavior in the subclass. Commandos are open for extension since we can inherit their properties and behavior. We could add a medic class as a subclass of the Commandos. Instead of modifying Commandos to support medics, we'll add an additional class and encapsulate that behavior. A side effect is that we'll respect the Single Responsibility Principle with the new class.

Recall our Commando parent class:

{% highlight ruby %}
class Commando
  def talk
    ''
  end

  def shoot
    ''
  end
end
{% endhighlight %}

In order to create a new class of medics, we introduce a new subclass where we add more specific medic-like behavior to the base class. Commandos are open for extension and we can keep them closed for modification by not changing or getting rid of the talk or shoot methods.

{% highlight ruby %}
class Medic < Commando
  def talk
    'Doctor Thomas'
  end

  def shoot
    'Silent'
  end

  def give_health
    { health: 50, food: 50 }
  end
end
{% endhighlight %}

You can see how connected the SOLID principles are. In our example, we fixed a Liskov violation in our medic implementation and respected both the Open/Close Princinple and the Single Responsilbity Principle.
