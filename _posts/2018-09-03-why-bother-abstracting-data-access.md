---
layout: post
title: "Why Bother Abstracting Data Access?"
date:   2018-09-03 01:00:00 -0500
categories: [software]
description: Why Bother Abstracting Data Access? I'll try to cover the reasons here. 
image: 
permalink: archive/2018/09/03/why-bother-abstracting-data-access
---

Early in my career I had trouble articulating why one should abstract an application's data access. I couldn't make it past the "in case we need to switch databases" argument. The point I was trying to make is a decent reason to follow the pattern but isn't alone very convincing. However, there are many, much more convincing reasons why you should abstract your data access. I'll try to cover them here. 

By the way, in the project I'm working on right now, we need to change both the database and ORM.

### Loose Coupling
With data access abstract, your application is no longer opinionated on how the data is being handled. We just need an implementation that fulfills a contract.

On one project we were running into database collisions under high traffic. Unfortunately the data access was intentionally ad hoc and all over the place, views and all. I needed to bypass the ORM and execute SQL commands directly to ensure proper SQL execution. Doing so removed any possibility of unit testing and coupled the class to yet another dependency. If this change had been behind an interface, my tests would have continued to pass (if they had even existed in the first place) and the rest of the application would have been none the wiser.

### Unit Testing
Loose coupling allows for unit tests because interfaces can be mocked. You _can_ unit test ad hoc data access with an in memory database using EF Core but that locks you in to using whatever ORM supports in memory databases. 

When I say "ad hoc" I mean using some kind of ORM to interact with data storage anywhere within the application. Like the following:
{% highlight csharp %}
[HttpGet]
public ActionResult Index()
{
    using(var context = new SomeDataContext())
    {
        var threads = context.ForumThreads.Take(10);
        return View(new IndexViewModel(threads));
    }
    
    // Or in our current case
    return View(new IndexViewModel(ForumThread.Query.Take(10)));
}
{% endhighlight %}

### It's just faster
{% highlight csharp %}
[HttpGet]
public ActionResult GetForumThreads(int forumId)
{
    var threads = _threadRepository.GetForumThreads(forumId, User);
    if(!threads.Any())
    {
        // error or something
    }

    return View(new ForumViewModel(threads));
}
{% endhighlight %}

Given that you've created the ForumThreadRepository interface and ignoring the fake error, the controller action above is finished. There is a ton of hidden complexity in getting the threads visible to a user. The best part about this, I can inject a fake implementation of the ForumThreadRepository and return whatever I want from `GetFroumThreads(User)` allowing other team members to begin working on consuming the endpoint without being blocked by my tinkering on complex queries. Whenever I'm ready to work with an actual database, I just configure my application to inject another class.

{% highlight csharp %}
public class FakeForumThreadRepository : IForumThreadRepository
{
    public IEnumerable<ForumThread> GetFroumThreads(User user)
    {
        return new[]
        {
            new ForumThread { Id = 1, Title = "A title" ...},
            ...
        }
    }
}
{% endhighlight %}
