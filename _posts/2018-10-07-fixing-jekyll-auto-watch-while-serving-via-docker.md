---
layout: post
title: "Fixing Jekyll Auto-Watch While Serving Via Docker"
date: 2018-10-07 01:00:00 -0500
categories: [software]
description: Fix auto-watch when running jekyll through docker.
image: 
---

My team is rewriting [curse.com](https://www.curse.com) in Jekyll and decided to use Docker to avoid requiring everyone install Ruby stuff. This worked well enough except auto-watch didn't immediately work using the `jekyll serve` command. We had to add the `--force_polling` flag to solve the problem.

{% highlight bash %}
docker run --rm --label=jekyll --volume=%CD%:/srv/jekyll -it -p 4000:4000 jekyll/builder jekyll serve --force_polling
{% endhighlight %}