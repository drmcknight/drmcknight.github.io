---
layout: post
title: "Protip: Resilient SQL Scripts"
date:   2018-08-31 01:00:00 -0500
categories: [sql, protips]
description: Colleagues of mine recently suggested we make our SQL scripts idempotent due to a few problems we'd been having
image: 
permalink: archive/2018/09/01/resilient-sql-scripts
---

Colleagues of mine recently suggested we make our SQL scripts idempotent due to a few problems we'd been having. I've known what an idempotent script is. I like running idempotent scripts. I have no idea why this hadn't already occurred to me. I extracted the template below from their recommendations and examples.

{% highlight sql %}
SET XACT_ABORT ON
-- A detailed description of what I'm intending to do with this script
BEGIN TRANSACTION
    IF NOT EXISTS (Condition)
        BEGIN
            -- Some risky business
            PRINT 'I just finished doing some risky business!';
        END
    ELSE
        BEGIN
            PRINT 'I did not have to do any risky business.';
        END
COMMIT TRANSACTION
{% endhighlight %}

_[SET XACT_ABORT ON](https://docs.microsoft.com/en-us/sql/t-sql/statements/set-xact-abort-transact-sql?view=sql-server-2017) Is the critical bit. It specifies whether SQL Server automatically rolls back the current transaction when a Transact-SQL statement raises a run-time error._

Now developers executing my scripts can execute them as many times as necessary and will always get a successful result. They are idempotent.
 