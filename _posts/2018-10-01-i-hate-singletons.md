---
layout: post
title: "I Hate Singletons"
date:   2018-10-01 01:00:00 -0500
categories: [software]
description: I'm only being a little dramatic. It's not that I hate only having one instance of something, that can be useful. It's that it's such an easy trap for developers to tightly couple everything together.
image: 
permalink: archive/2018/10/01/i-hate-singletons
---

I'm only being a little dramatic. It's not that I hate only having one instance of something, that can be useful. It's that it's such an easy trap for developers to tightly couple everything together.

Take my new class `Foo` for example. It only has the default constructor. Whoever calls `new Foo()` has no idea that they've just coupled their class to 4 other systems.

{% highlight csharp %}
public class Foo
{
    Foo()
    {
        BillingSystem.Instance.GetAThing();
        SessionSystem.Instance.GetAnotherThing();
        EmailSystem.Instance.GetYetAnotherThing();
        NotificationSystem.Instance.GetTheLastThing();
    }
}
{% endhighlight %}

Only use singletons when whatever you're doing _requires_ there to only one instance of a class. And if singletons are required, rely on your IOC Container and inject them.