---
layout: post
title: "Business and Tech Debt"
date:   2018-09-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/business-and-tech-debt
---

I've noticed that engineers tend to feel at odds with product owners when it comes to tech debt. Product owners set priority and tech debt never seems to make it to the top. They just have some weird vendetta against good engineering, right? Probably  not. The more likely issue is that engineers suck at speaking the business' language when it comes to tech debt.

I've made a decent amount of progress in this kind of communication so I'll try to list out a few lessons that I've learned over the years.

### Be Specific
No one sits down at their computer and pays down tech debt. They do however refactor a class to be testable and then write unit tests.

Take a piece of our tech debt as an example. 

>**Refactor CSS:**
>Our CSS is difficult to work with. Needs to be cleaned up.

This is just begging to be ignored.

>**Resolve CSS Overspecificity:**
>Our platform CSS is overly specific, difficult to read, and even more difficult to maintain. Developers building on our platform have to write CSS that is even harder to read and maintain to beat platform specificity. This is a pretty big lift but will only get worse with time.

### Classify to Prioritize
 Riot shared how they reason about their tech debt in [Taxonomy of tech debt](https://engineering.riotgames.com/news/taxonomy-tech-debt). We haven't found much value in the actual numbering system that they use but the axes help us drive discussions and set priority.

#### Impact
>This takes the form of player-facing issues (bugs, missing features, unexpected behavior), and developer-facing issues (slower implementation, workflow issues, random useless shit to remember).

#### Fix Cost
>The second axis has to do with the cost to fix the tech debt. If we decide to fix an issue in our code or data, it will require someone’s measurable time to fix. If it’s a deeply rooted assumption that affects every line of code in the game, it may take weeks or months of engineering time. If it’s a dumb error in a single function, it may be fixable in a matter of minutes. Regardless of the time to implement a fix, though, we also must consider the risk of actually deploying that fix. Even a system I consider “wrong” can still be used as a tool to make a great game


#### Contagion
>The third axis is something I’ve become obsessed with: contagion. If this tech debt is allowed to continue to exist, how much will it spread?


### Measure Cost


