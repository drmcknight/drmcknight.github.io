---
layout: post
title: "\"The file does not exist\" Error Resolved (ASP.NET MVC)"
date:   2018-08-25 01:48:47 -0500
categories: software
description: Resolving the "The file does not exist" error for an ASP.NET MVC view
image: 
---

We started getting an error stating `The file does not exist.` intermittently regarding random views. When you run into this issue, check that the following is true:
* The view really does exist at the path specified
* The master page that the view is referencing exists
* You are not running out of memory

The first two are obvious but it was the last one was our problem. As best as we can tell, dynamic view compilation was failing due to not having enough resources causing view files to never get compiled. This was particularly tough to track down because it was happening intermittently on different views directing us to dig into several red herrings. We resolved the issue by just increasing the EC2 node size and haven't had an issue since.