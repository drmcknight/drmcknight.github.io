---
layout: post
title: "Business and Tech Debt"
date:   2018-08-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/business-and-tech-debt
---

I've noticed that engineers tend to feel at odds with product owners when it comes to tech debt. Product owners set priority and tech debt never seems to make it to the top. They just have some weird vendetta against good engineering, right? Maybe. The more likely issue is that engineers suck at speaking the business' language when it comes to tech debt.

I've made a decent amount of progress in this kind of communication so I'll try to list out a few lessons that I've learned over the years.

### Be Specific
No one sits down at their computer and pays down tech debt. They do however refactor a class to be testable and then write unit tests.

Take a piece of our tech debt as an example. 

>**Refactor CSS:**
>Our CSS is embarrassing. Needs to be cleaned up.

This is just begging to be ignored.

>**Resolve CSS Overspecificity:**
>Our platform CSS is overly specific, difficult to read, and even more difficult to maintain. Developers building on our platform have to write CSS that is even harder to read and maintain to beat platform specificity. This is a pretty big lift but will only get worse with time.

### Classify to Prioritize
[Taxonomy of tech debt](https://engineering.riotgames.com/news/taxonomy-tech-debt)
* Impact
* Fix Cost
* Contagion

### Measure Cost


