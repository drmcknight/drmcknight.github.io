---
layout: post
title: "Fixing Jekyll Auto-Watch While Serving Via Docker"
date: 2018-10-07 01:00:00 -0500
categories: [software]
description: 
image: 
permalink: archive/2018/10/07/fixing-jekyll-auto-watch-while-serving-via-docker
---

My team is rewriting [curse.com](https://www.curse.com) in Jekyll and decided to use Docker to avoid requiring everyone install Ruby stuff. This worked well enough except auto-watch wasn't working. Adding the `--force_polling` solves the problem.

{% highlight bash %}
docker run --rm --label=jekyll --volume=%CD%:/srv/jekyll -it -p 4000:4000 jekyll/builder jekyll serve --force_polling
{% endhighlight %}