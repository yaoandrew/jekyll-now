---
layout: post
title: The Interface Segregation Principle
tags: ["SOLID"]
---
![Cartoon about code image](/images/ISP.jpg)

The Interface Segregation Principle says the following:
>Clients should not be forced to depend on interfaces they do not use.

Let's think for a minute what an interface is. An interface is simply a way we interact with something. In the real world, it might be the control panel of a washing machine. This might have buttons to turn on the power, select the wash style, water temperature, and spin speed. Imagine that I'm building a matching dryer that needs a way to turn on the power and I use the same control panel. While my dryer can use the power button, the rest of the buttons on the interface are not really useful. One way we might achieve the same look and feel for the washer and the dryer by using the same control panel is to split it into two areas, one that controls things to do with the power and one that controls things that configure the washing cycle. Then, our dryer could use (implement) the power control panel (interface) and not have extraneous controls for the wash cycle that it doesn't need.

Now that you understand the concept, let's think about what this means when we are designing systems instead of household appliances. In software, an interface is still the way you interact with something, instead this time its a class, not a dryer. The interface lays out the blueprint for the class but doesn't have any implementation details. Each class that implements the interface must specify implementation details for the methods in the interface. When a class implements an interface, we know it will contain the methods in the interface.

The SOLID principles are meant to help your code deal with change. Imagine that several classes have implemented the same interface and you have to add a method to that interface to support some functionality that one of those classes needs. Now all classes need to have implementation details for the new method regardless if its needed or not. The change, causes a series of cascading changes. It would seem that the interface is doing too much and perhaps violates the Single Responsibility Principle. We can clean this up by splitting the interface across its responsibility lines and classes can then implement only the interfaces they need.

Let's say we want to add the ability to send email messages to our system. They should implement the `IMessage` interface as shown below.

{% highlight csharp %}
public interface IMessage
{
  IList<string> SendTo { get; set; }
  IList<string> CCTo { get; set; }
  IList<string> BCCTo { get; set; }
  string Subject { get; set; }
  string MessageText { get; set; }
  bool Send()
}

public class EmailMessage : IMessage
{
  IList<string> SendTo { get; set; }
  IList<string> CCTo { get; set; }
  IList<string> BCCTo { get; set; }
  string Subject { get; set; }
  string MessageText { get; set; }

  bool Send()
  {
    //Connect to email server and send message
  }

}
{% endhighlight %}

Now imagine that we'd like to add SMS messages to our system. Awesome, we can create a new class to handle this logic and leverage the existing `IMessage` interface. Uh oh, there's a bunch of stuff that isn't relevent to SMS messages in the interface like the Subject field.

This should inform us that perhaps the `IMessage` interface is too fat, violates the SRP, and we can extract some logic out. We could in fact split this into a few interfaces.

{% highlight csharp %}
public interface IMessage
{
  IList<string> SendTo { get; set; }
  string MessageText { get; set; }
  bool Send()
}

public interface IEmailMessage
{
  IList<string> CCTo { get; set; }
  IList<string> BCCTo { get; set; }
  string Subject { get; set; }
}

{% endhighlight %}

Now we can have the `EmailMessage` class implement both interfaces while the `SMSMessage` class only needs to implement the one that it needs to send SMS messages without being coupled to things it doesn't care about like the CC, BCC, and Subjects fields.

{% highlight csharp %}
public class SMSMessage : IMessage
{
  IList<string> SendTo { get; set; }
  string MessageText { get; set; }

  bool Send()
  {
    //Connect to SMS server and send message
  }
}

public class EmailMessage : IMessage, IEmailMessage
{
  IList<string> SendTo { get; set; }
  IList<string> CCTo { get; set; }
  IList<string> BCCTo { get; set; }
  string MessageText { get; set; }
  string Subject { get; set; }

  bool Send()
  {
    //Connect to email server and send message
  }

}

{% endhighlight %}

When thinking about the SOLID principles, you finally notice how interconnected they are and how they are applicable in many different areas in your code design. Hopefully, by sticking to the SRP and the ISP, your code will be easy to change. By extracting and refactoring our interface, we've made our code less rigid, fragile, and easier to maintain.
