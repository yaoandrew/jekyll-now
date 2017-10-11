---
layout: post
title: Know Your Command Line Tools
tags: ["tools"]
---
![Command Line Screen image](/images/commandline.png)

In the O'Reilly book _97 Things Every Programmer Should Know_, there's an entry that caught my attention by Carroll Robinson. His 'thing' that we should know is how to use command line tools. My own history in technology has set me up well for this. In the late 90s, while at my first job, we ran Solaris/UNIX machines on the desktop. It was the first time I was exposed to the command line and I had a boss that loved to write shell scripts and use UNIX commands for basic tasks that Windows users had GUI based applications for. One example that comes to mind is our contact database which was simply a flat file that we would grep to search for a contact.

There were times when I needed to find out the number of users at a particular client and I could simply chain together a few commands:

{% highlight ruby %}
grep clientname | wc -l
{% endhighlight %}

I worked with one person who's job was to extract some reporting from our systems and he seemed to do his entire job with shell scripts, `sed`, and `awk`.

In Robinson's post, his point is related to another 'thing' programmers should know or do by Alan Griffiths called Don't Rely on "Magic Happens Here". The common themes across both articles are to understand what is going on under the hood and not think anything happens automagically. Robinson talks about it in the context of an IDE and refers to Visual Studio or Eclipse while suggesting that programmers understand what happens when you click a button in the IDE and the tool magically creates an executable file in your project folder. In more modern development tools like VS Code, there's even a terminal window to run terminal commands.

Robinson's point is, get your head out of the IDE and learn some command line tools. He suggests that the IDE is just a graphical interface to the command line for developement and there's a lot of power and experience to be gained from using the command line.

I happen to use vim for most of my development. A key part to working efficiently in vim is understanding how to find all references of a class across files on the file system. I could certainly use a refresher on all the command line arguments available for `grep` and `find`. I agree with Robinson on learning the command line and have seen patterns from UNIX help me understand other concepts in programming. While I don't need to control my soundcloud playlist from the command line like the image in this post suggests, there are a lot of fun, retro things you can do with it.

I'll leave you with the following example command to play with on you command line:

{% highlight ruby %}

curl wttr.in/~newyork
curl wttr.in/santa-monica

{% endhighlight %}
