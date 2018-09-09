---
layout: post
title: "Prioritizing Tech Debt"
date:   2018-09-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/prioritizing-tech-debt
---

I've been working on how to best advocate prioritizing tech debt in quarterly planning. These are a few things that I've found handy.

## Be Specific
When creating the artifacts (JIRA stories, note cards, etc.) that will be discussed in planning meetings, paint a clear and simple picture of what the tech debt is and why it's debt. Be wary of including too much information. Your non-technical teammates may skim over the details and you'll wind up [bikeshedding](https://en.wiktionary.org/wiki/bikeshedding).

**Bad:**
Our CSS is difficult to work with. It needs to be cleaned up.

**Better:**
Our platform CSS is overly specific, difficult to read, and even more difficult to maintain. Developers building on our platform have to write CSS that is even harder to read and maintain to beat platform specificity. This causes regressions often and severely impacts developer effectiveness. In order to fix this we will need to refactor our style sheets and markup.

## Measure
Once we've described the tech debt we'll need a way to compare it to other things competing for priority. One great approach was published by Riot in a [blog post](https://engineering.riotgames.com/news/taxonomy-tech-debt) explaining how they measure their tech debt by impact, fix cost, and contagion. I don't see much value in the actual numbering system that they use but the axes help drive discussions.

### Impact
>This takes the form of player-facing issues (bugs, missing features, unexpected behavior), and developer-facing issues (slower implementation, workflow issues, random useless shit to remember).

Does this impact developers, customers, or both?

### Fix Cost
>The second axis has to do with the cost to fix the tech debt. If we decide to fix an issue in our code or data, it will require someone’s measurable time to fix.

You may find value spending the time coming up with specific dollar values here. I'm really just looking for something simple: expensive, reasonable, cheap

### Contagion
>If this tech debt is allowed to continue to exist, how much will it spread?

Does this tech debt create more tech debt?

## The Price of Ignoring
How much will it cost us to not fix it? This is hard to measure but it exists and needs to be discussed. The price could be a dollar amount, risky deploys, difficultly recruiting, or anything really. I'll probably write a whole post about this soon.

----

<br />
With the information that we've aggregated, we're in a much better position to advocate prioritizing paying down our tech debt. We may still end up prioritizing other projects but at least the decision will be far more informed.