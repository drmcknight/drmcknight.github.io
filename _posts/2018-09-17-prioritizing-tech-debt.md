---
layout: post
title: "Prioritizing Tech Debt"
date:   2018-09-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/prioritizing-tech-debt
---

When setting priority, tech debt seems to want to crawl to the bottom of the list. The business wants to deliver valuable feature x and developers want to fix developer-nagging issue y. We need to improve how we advocate for resolving tech debt. I've been working on improving at this so I'll list out a few things that I've found handy.

## Be Specific
When creating the artifacts that will be discussed in planning meetings (JIRA stories or note cards), paint a clear and simple picture of what the tech debt is and why it's debt. Be wary of including too much information. Your non-technical people may skim over the details and you'll wind up [bikeshedding](https://en.wiktionary.org/wiki/bikeshedding).

**Bad:**
Our CSS is difficult to work with. It needs to be cleaned up.

**Better:**
Our platform CSS is overly specific, difficult to read, and even more difficult to maintain. Developers building on our platform have to write CSS that is even harder to read and maintain to beat platform specificity. This causes regressions often and severely impacts developer effectiveness. In order to fix this we will need to refactor our style sheets and markup.

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
We now know generally what it will cost to fix the tech debt but how much have we already paid? It will be much easier to justify prioritizing tech debt when we know how much the business has been paying for it. If you're in our position and don't have sufficient time reporting at this granularity, estimate.

**Bad:**
I waste _so_ much time fighting CSS

**Better:**
I spend 20% more time writing CSS due to overspecificity and the resulting CSS is so difficult to understand that I'm the only developer who can maintain it. 

## Put it All Together
My team uses JIRA so we would make an epic and list the appropriate fields and discuss during quarterly planning. Now we're in a much better position to advocate for paying down tech debt.