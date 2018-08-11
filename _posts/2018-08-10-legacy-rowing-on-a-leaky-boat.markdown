---
layout: post
title:  "Cobalt: Rowing a Leaky Boat, part 1"
date:   2018-08-10 23:48:47 -0500
categories: curse, cobalt
---

Cobalt is the name of the platform that many of your favorite Curse sites are built upon ([dndbeyond.com](https://www.dndbeyond.com), [strawpoll.me](https://www.strawpoll.me), and [wowdb.com](https://www.wowdb.com) to name a few). It offers robust multi-tenant forums, CMS, two achievements systems, and dozens of other things that I'm eager to remove. In this series I'm going to attempt to chronicle my adventures with Cobalt as it contains lots of lessons about software.

The abridged origin story is that it was a skunkworks project in response to the lackluster performance of existing 3rd party offerings Curse was using back in 2008. Here are the early specs:

* .NET 3.5
* ASP.NET MVC 1.1
    * There was never an ASP.NET MVC 1.1. Someone decompiled MVC's source, changed a few things, and recompiled it as MVC 1.1. I still don't know what was changed.
* Custom static content packager
* Custom deploy process
* SQL Server 2008
* An extended LINQ 2 SQL
* IIS Output Caching
* Cloudflare

[A bit about the first site or two built using cobalt]

The posts from here on out will be from my perspective when I started working with Cobalt in September of 2014.