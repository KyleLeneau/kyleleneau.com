---
layout: post
title: "ASP.Net MVC Route Table Ordering"
date: '2008-10-27 17:20:34'
categories: Programming
---

Over the past few weeks I have been working on an MVC forum component for a website I maintain/develop ([http://pertnearsandstone.com](http://pertnearsandstone.com)). As I was working through the various screens I would set up the intended routes to the route table in my global.ascx.cs file only to learn that route ordering is very important. The order of the routes affects the flow and logic of your application.

To start off I had something like this working. I could get to all my views and actions as expected. Could get to the post/reply system as well and the index of topics and thread pages.

{% highlight csharp %}
routes.MapRoute("Forum-Index", "Forum",
    new { controller = "Forum", action = "Index" });

routes.MapRoute("Forum-CreatePost", "Forum/Create",
    new { controller = "Forum", action = "Create" });

routes.MapRoute("Forum-NewPost", "Forum/Post/{ParentThreadID}/{ParentPostID}",
    new { controller = "Forum", action = "New", ParentThreadID = 0, ParentPostID = 0 });

routes.MapRoute("Forum-Thread", "Forum/Thread/{threadId}",
    new { controller = "Forum", action = "Thread", threadId = 0 });
{% endhighlight %}

Then I wanted to add paging to the index (topics) page so I implemented the logic in my controllers and added the helper to the view.  I also updated my routes to accept the new page as seen below:

{% highlight csharp %}
routes.MapRoute("Forum-Index", "Forum/{page}",
    new { controller = "Forum", action = "Index", page = 0 });

routes.MapRoute("Forum-CreatePost", "Forum/Create",
    new { controller = "Forum", action = "Create" });

routes.MapRoute("Forum-NewPost", "Forum/Post/{ParentThreadID}/{ParentPostID}",
    new { controller = "Forum", action = "New", ParentThreadID = 0, ParentPostID = 0 });

routes.MapRoute("Forum-Thread", "Forum/Thread/{threadId}",
    new { controller = "Forum", action = "Thread", threadId = 0 });
{% endhighlight %}

I tested everything out and found that the paging was working correctly but everything else had broken, except the thread page.  I spent entirely too much time on this issue to find out thanks to [Scott Guthrie](http://weblogs.asp.net/scottgu/default.aspx) and his [URL Routing Post](http://weblogs.asp.net/scottgu/archive/2007/12/03/asp-net-mvc-framework-part-2-url-routing.aspx) that I had an issue with how my routes were ordered. In his post I re-learned that routes must be in order from most specific to least specific. Obviously my new paging parameter was catching my Create route and my Post route when no data was being sent additionally (/Forum/Post/0/0 works, /Forum/Post did not). I changed the order of my routes like below and everything worked as expected.

{% highlight csharp %}
routes.MapRoute("Forum-CreatePost", "Forum/Create",
    new { controller = "Forum", action = "Create" });

routes.MapRoute("Forum-NewPost", "Forum/Post/{ParentThreadID}/{ParentPostID}",
    new { controller = "Forum", action = "New", ParentThreadID = 0, ParentPostID = 0 });

routes.MapRoute("Forum-Thread", "Forum/Thread/{threadId}",
    new { controller = "Forum", action = "Thread", threadId = 0 });

routes.MapRoute("Forum-Index", "Forum/{page}",
    new { controller = "Forum", action = "Index", page = 0 });
{% endhighlight %}

If you are reading this entry and know of a way to a) either check to see if the parameter can be parsed as an int (as in page index) and match the route, similar to a constraint or b) an easy way to test the routes.  I would greatly appreciate any feedback, comments, or sample code of your solutions.
