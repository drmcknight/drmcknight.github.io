---
layout: post
title: "C# var Keyword Versus Explicit Type"
date: 2018-09-24 01:00:00 -0500
categories: [csharp, holy war]
description: 
image: 
permalink: archive/2018/09/24/csharp-var-versus-explicit-type
---

I've stumbled upon this holy war a few times throughout my career. One side says var is easier to use, the other side says explicit typing is more readable. I think they're both right. I tend to use var liberally but if I had to agree upon a set of rules with someone who hated var, here's what they'd be:

* If there's any ambiguity on the right side of the equal sign, use explicit typing. `var thread = _threadRepository.GetById(id);` is a little vague. Although I'd improve the variable and method names before using the type explicitly.
* Use var when the type is obvious. `IndexViewModel indexViewModel = new IndexViewModel();` doesn't help anyone.

Using var puts the burden on variable names and initialization for clarity which is good enough for most cases. I think these rules are a decent compromise. If one side of the holy war isn't happy, I'll just start writing the most explicit code imaginable by using full namespaces on everything.

{% highlight csharp %}
public static void DoAThing()
{
    System.Collections.Generic.List list = new System.Collections.Generic.List();
    System.Console.WriteLine("Now no one is happy.");
    ...
}
{% endhighlight %}


