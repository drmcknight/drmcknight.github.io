---
layout: post
title:  "Cobalt: Rowing a Leaky Boat, part 1"
date:   2018-08-10 23:48:47 -0500
categories: curse, cobalt
---

I once heard a developer on another team describe his work as "rowing a leaky boat". In the analogy you are in a sinking boat and you have to either bail or row. If you choose to bail, you're drifting back out to sea. If you choose to row, you sink. The analogy felt familiar except we've even gone as far as trying to invent more choices. "Sure we can totally do this intense redesign and also meet the aggressive new project deadline. We'll just do them together!". Not suprisingly we found ourselves still sinking, drifting out to sea and totally off course. You can't row and bail at the same time and I think we've been trying to bail and row Cobalt for some time.

Cobalt is a platform that many of your favorite Curse sites are built upon ([dndbeyond.com](https://www.dndbeyond.com), [strawpoll.me](https://www.strawpoll.me), and [wowdb.com](https://www.wowdb.com) to name a few). It's a multi-tenent application that offers robust forums, CMS, UAC, two achievements systems, great performance, a few productivity tools, and dozens of other things that I'm eager to remove. 

Its abridged origin story is that it was a skunkworks project designed to outperform the lackluster 3rd party offerings Curse was using back in 2008. Unfortunately, the great performance usually came at the expense of maintainability. This wasn't an issue early on but as the platform matured, decay crept in. Branched codebases and databases diverged, code sprawled, deploys were risky as regressions were far too common. We've been paying down this debt little-by-little over the past few years but we've kicked this effort into overdrive! Throughout this series I'm going to chronicle my adventures as we pay down this tech debt in this "legacy rescue". 

To give a little peek into where we started I've added the details below:

* .NET 3.5
* ASP.NET MVC 1.1
    * There was never an ASP.NET MVC 1.1. Someone decompiled MVC's source, changed a few things, and recompiled it as MVC 1.1. I still don't know what was changed.
* Custom static content packager
* Custom deploy process executed on developer machines
* SQL Server 2008
* An extended LINQ 2 SQL
* Test coverage < 1%
* 1 repository with hundreds of branches
    * Some branches contained a totally different set of applications. Merges were fun.
* Little documentation