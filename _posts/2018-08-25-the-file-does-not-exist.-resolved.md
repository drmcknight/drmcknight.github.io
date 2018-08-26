---
layout: post
title: "\"The file does not exist\" Error Resolved"
date:   2018-08-25 01:48:47 -0500
categories: software
description: Resolving the "The file does not exist" error for an ASP.NET MVC view
image: 
---

We started getting the `The file does not exist.` error intermittently after moving to AWS. When you run into this issue, check out the following:
* The file really doesn't exist at the path specified
* The master page cannot be found
* You are running out of memory

The first two are obvious but it was the last one was our problem. As best as we can tell, dynamic view compilation was failing due to not having enough resources causing view files to never get compiled. This was particularly tough to track down because it was happening intermittently on different views directing us to dig into several red herrings. We resolved the issue by just increasing the EC2 node size and haven't had an issue since.