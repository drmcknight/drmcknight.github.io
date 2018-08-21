---
layout: post
title:  "Cobalt: Curse's ASP.NET MVC Platform"
date:   2018-08-10 23:48:47 -0500
categories: [curse, cobalt, software]
description: Cobalt is an APS.NET MVC platform that many of your favorite sites are built upon. I'm going to chronicle my adventures as we pay down its tech debt.
---

Cobalt is a platform that many of your favorite Curse sites are built upon ([dndbeyond.com](https://www.dndbeyond.com), [strawpoll.me](https://www.strawpoll.me), and [wowdb.com](https://www.wowdb.com) to name a few). It's a multi-tenant application that offers robust forums, CMS, UAC, two achievements systems, great performance, a few productivity tools, and dozens of other things that I'm eager to remove. Its abridged origin story is that it was a skunkworks project designed to outperform the lackluster 3rd party offerings Curse was using back in 2008. Unfortunately, the great performance usually came at the expense of maintainability. This wasn't an issue early on but as the platform matured and the original authors moved on to other things, decay crept in. Branched codebases and databases diverged, code sprawled, and deploys were risky as regressions were far too common. To give a little peek into the earlier application I've added the details below:

* ASP.NET MVC 1.1
    * There was never an ASP.NET MVC 1.1. Someone decompiled MVC's source, changed a few things, and recompiled it as MVC 1.1. I still don't know what was changed.
* Custom static content packager
* Custom deploy process executed on developer machines
* MSSQL
* LINQ 2 SQL with custom extensions
* Test coverage < 1%
* 1 repository with hundreds of branches
    * Some branches contained a totally different set of applications. Merges were fun.
* Little documentation

We've been paying down the glaring tech debt little-by-little over the past few years but we've recently kicked this effort into overdrive! From time-to-time I will chronicle our adventures as we pay down tech debt in this "legacy rescue"!

