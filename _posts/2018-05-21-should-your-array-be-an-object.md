---
layout: post
title: "Should Your Array Be an Object?"
date: 2018-05-21 23:48:47 -0500
categories: clean code
description: I stumbled on this terrible code.
---

If each index of your array represents a property of a conceptual model, do a solid for those who will come after you and make a class. I stumbled on this a few years ago while trying fix a bug. My best guess is that this represents the attack/defense/resist/weakness matrix of a set of pokemon. Which pokemon? Which stats?

{% highlight csharp %}
private static readonly double[][] AtkDefResistWeaknessMatrix =
{
  new[] {1, 1, 1, 1, 1, .5, 1, 0, .5, 1, 1, 1, 1, 1, 1, 1, 1,0},
  new[] {2, 1, .5, .5, 1, 2, .5, 0, 2, 1, 1, 1, 1, .5, 2, 1, 2,0 },
  new [] {1, 2, 1, 1, 1, .5, 2, 1, .5, 1, 1, 2, .5, 1, 1, 1, 1,0 },
  new [] {1, 1, 1, .5, .5, .5, 1, .5, 0, 1, 1, 2, 1, 1, 1, 1, 1,0 },
  new [] {1, 1, 0, 2, 1, 2, .5, 1, 2, 2, 1, .5, 2, 1, 1, 1, 1,0 },
  new [] {1, .5, 2, 1, .5, 1, 2, 1, .5, 2, 1, 1, 1, 1, 2, 1, 1,0 },
  new [] {1, .5, .5, .5, 1, 1, 1, .5, .5, .5, 1, 2, 1, 2, 1, 1, 2,0 },
  new [] {0, 1, 1, 1, 1, 1, 1, 2, .5, 1, 1, 1, 1, 2, 1, 1, .5,0 },
  new [] {1, 1, 1, 1, 1, 2, 1, 1, .5, .5, .5, 1, .5, 1, 2, 1, 1,0 },
  new [] {1, 1, 1, 1, 1, .5, 2, 1, 2, .5, .5, 2, 1, 1, 2, .5, 1,0 },
  new [] {1, 1, 1, 1, 2, 2, 1, 1, 1, 2, .5, .5, 1, 1, 1, .5, 1,0 },
  new [] {1, 1, .5, .5, 2, 2, .5, 1, .5, .5, 2, .5, 1, 1, 1, .5, 1,0 },
  new [] {1, 1, 2, 1, 0, 1, 1, 1, 1, 1, 2, .5, .5, 1, 1, .5, 1,0 },
  new [] {1, 2, 1, 2, 1, 1, 1, 1, .5, 1, 1, 1, 1, .5, 1, 1, 0,0 },
  new [] {1, 1, 2, 1, 2, 1, 1, 1, .5, .5, .5, 2, 1, 1, .5, 2, 1,0 },
  new [] {1, 1, 1, 1, 1, 1, 1, 1, .5, 1, 1, 1, 1, 1, 1, 2, 1,0 },
  new [] {1, .5, 1, 1, 1, 1, 1, 2, .5, 1, 1, 1, 1, 2, 1, 1, .5,0 },
  new [] {1, .5, 1, 1, 1, 1, 1, 2, .5, 1, 1, 1, 1, 2, 1, 1, .5,0 }};
{% endhighlight %}

A much cleaner implementation could could have been to create an object...

{% highlight csharp %}
public class Pokemon
{
  public string Name { get; set; }
  public double Attack { get; set; }
  public double Defence { get; set; }
  ...
}
{% endhighlight %}