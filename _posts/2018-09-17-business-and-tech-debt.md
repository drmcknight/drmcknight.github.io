---
layout: post
title: "Business and Tech Debt"
date:   2018-09-17 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/09/17/business-and-tech-debt
---

The platform that I work on has amassed quite a bit of tech debt over the decade of its existence. No one has ever really had a vision for what it should and shouldn't do so it does tons of things poorly and a few things well. 

A few years ago we forked a team to better align around the work we should be doing. One team owned a set of complex sites while the other team was intended to work on the platform. I was excited at the opportunity to repair the platform but it didn't immediately pan out. We would plan out quarters of work and do maybe 10% of it- the rest was whatever new work came in. One of our new managers  asked me, "Why does the Framework Team always seem available?". The business simply valued the new work more than tackling the tech debt.

I don't think our plans were being usurped because the business didn't value good engineering. We were just unsuccessful at reporting the specific tech debt we had and the cost we were incurring for having it around. 

In this post I'll try to list out a few things I wish I had known then.

### Be Specific
No one sits down at their computer and pays down tech debt. They do however refactor a class to be testable and then write unit tests.

### Classify to Prioritize
[Taxonomy of tech debt](https://engineering.riotgames.com/news/taxonomy-tech-debt)

### Measure Cost


