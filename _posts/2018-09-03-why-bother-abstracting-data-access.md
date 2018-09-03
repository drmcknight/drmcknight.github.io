---
layout: post
title: "Why Bother Abstracting Data Access?"
date:   2018-09-03 01:00:00 -0500
categories: [software]
description: Beware! When advocating for data access abstraction, database changeability is a red herring. The real discussion is whether or not we want a loosely coupled application.
image: 
permalink: archive/2018/09/03/why-bother-abstracting-data-access
---

Beware! When advocating for data access abstraction, database changeability is a red herring. Sharp teammates can argue that changing from MSSQL to Oracle is highly unlikely, and they'd most likely be right. The real discussion is whether or not we want a loosely coupled application. With a loosely coupled application, we can indeed easily change databases but that is not the end to our means. 

Below I'll try to cover what I think are the best reasons for abstracting data access. By the way, in the project I'm working on right now, we need to change both the database platform and ORM.

### Loose Coupling
With data access abstract, your application is no longer opinionated on how the data is being handled. We just need an implementation that fulfills a contract.

An example of when this would have been useful was on one project where we were running into database collisions under high traffic. Unfortunately the data access was intentionally ad hoc and all over the place. I needed to bypass the ORM and execute SQL commands directly to ensure proper SQL execution. Doing so removed any possibility of unit testing and coupled the class to yet another dependency. If this had all been behind an interface, my tests would have continued to pass and the rest of the application would have been none the wiser.

{% highlight csharp %}
[HttpPost]
public ActionResult LikeComment(int commentId)
{
    //This controller action doesn't care that I've changed how Like() works
    _commentRepository.Like(commentId, User);
    ...
}
{% endhighlight %}

_Note: it is implied that repositories are being injected in examples throughout_

### Unit Testing
Loose coupling allows for unit testing because interfaces can be mocked. You _can_ unit test ad hoc data access with an in memory database using EF Core but that locks you in to using whatever ORM supports in memory databases (EF Core). 

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

### Get Feedback Faster
{% highlight csharp %}
[HttpGet]
public ActionResult GetForumThreads(int forumId)
{
    var threads = _threadRepository.GetForumThreads(forumId, User);
    return View(new ForumViewModel(threads));
}
{% endhighlight %}

Given that you've created `IForumThreadRepository`, the controller action above is functional. There is a ton of complexity in getting the threads visible to a user that we don't have to deal with yet. I can inject a fake implementation of the ForumThreadRepository and return whatever I want from `GetFroumThreads(User)` allowing myself or other team members to begin working on consuming the endpoint and getting stakeholder feedback without being blocked by my tinkering on complex queries.

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

 Whenever I'm ready to work with an actual database, I just configure my application to inject the "real" class.

### It Fits In Your Head
Dan North talks a lot about writing [software that fits in your head](https://www.youtube.com/watch?v=4Y0tOi7QWqM). If you haven't watched his stuff, do it.

It becomes much harder to reason about your software when you have queries (or anything) scattered all over. The project I'm currently working on has data access in more places than it isn't. I think the last time I checked there are 130 queries in views.

Now consider our current initiative: We need to update our ORM so we can use a cheaper database platform. Accurately estimating this effort is impractical. Our choices are: commit to a long-term, herculean effort to find every query in the application and change it or find a solution that we can extend to match our current syntax.

If our data access was abstract, this would be much simpler to plan and execute piecemeal.

{% highlight csharp %}
public class CurseORMForumRepository : IForumThreadRepository
{
    public IEnumerable<ForumThread> GetAllForums()
    {
        return Forum.Query.GetAll();
    }

    public ForumThread GetById(int forumId)
    {
        return Forum.Query.GetById(forumId);
    }

    ...
}
{% endhighlight %}

Now just wrap the old class with a new one and override the methods we have time to tackle. 

{% highlight csharp %}
public class EFCoreForumRepository : CurseORMForumRepository
{
    public override IEnumerable<ForumThread> GetAllForums()
    {
        using(var ctx = new DataContext())
        {
            // not sure if this is the correct syntax but you get the idea.
            return ctx.Forums;
        }
    }
    ...
}
{% endhighlight %}

When we're done overriding all of the methods in this class, just inherit from `IForumThreadRepository` instead of `CurseORMForumRepository`, remove all of the `override` key words and call it good!