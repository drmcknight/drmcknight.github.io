---
layout: post
title: "Prioritizing Tech Debt"
date:   2018-09-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/prioritizing-tech-debt
---

Engineers tend to feel at odds with product owners when it comes to tech debt. Product owners set priority and tech debt never seems to make it to the top. They just have some weird vendetta against good engineering, right? Probably  not. The more likely issue is that engineers suck at communicating the value of paying down tech debt.

I've been working on improving at this so I'll try to list out a few things that I've found handy.

## Be Specific
No one sits down at their computer and pays down tech debt. They do however refactor a class to be testable and then write unit tests.

**Bad:**
Our CSS is difficult to work with. It needs to be cleaned up.

**Better:**
Our platform CSS is overly specific, difficult to read, and even more difficult to maintain. Developers building on our platform have to write CSS that is even harder to read and maintain to beat platform specificity. This causes regressions often and severely impacts developer sentiment. In order to fix this we will need to refactor our style sheets and markup.

## Measure
 Riot shared how they measure tech debt by impact, fix cost, and contagion in [Taxonomy of tech debt](https://engineering.riotgames.com/news/taxonomy-tech-debt). I don't see much value in the actual numbering system that they use but the axes help drive discussions.

### Impact
>This takes the form of player-facing issues (bugs, missing features, unexpected behavior), and developer-facing issues (slower implementation, workflow issues, random useless shit to remember).

Does this impact developers, customers, or both?

### Fix Cost
>The second axis has to do with the cost to fix the tech debt. If we decide to fix an issue in our code or data, it will require someone’s measurable time to fix.

You may find value spending the time coming up with specific dollar values here. I'm really just looking for something simple: expensive, reasonable, cheap

### Contagion
>If this tech debt is allowed to continue to exist, how much will it spread?

Does this tech debt create more tech debt?
## Interest Cost
We now know generally what it will take to fix the tech debt how much has it already cost? It will be much easier to justify prioritizing tech debt when we know how much the business has been paying for it. If you're in our position and don't have sufficient time reporting at this granularity, estimate.

**Bad:**
I waste _so_ much time fighting CSS

**Better:**
I spend 20% more time writing CSS due to overspecificity and the resulting CSS is so difficult to understand that I'm the only developer who can maintain it. 

## Put it All Together
My team uses JIRA so we would make an epic and list the appropriate fields and discuss during quarterly planning. Now we're in a much better position to advocate for paying down tech debt.