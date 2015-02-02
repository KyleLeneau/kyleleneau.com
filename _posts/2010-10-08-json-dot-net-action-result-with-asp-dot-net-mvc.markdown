---
layout: post
title: Json.Net Action Result with Asp.Net MVC
date: 2010-10-08 08:00
categories: Programming
---

Well this has probably been done 100 times before but so what, the world could always use more code. When working with ASP.Net MVC I started and fell in love with [James Newton-King's Json.Net library](http://james.newtonking.com/pages/json-net.aspx).  It is simple awesome and does an amazing job in different parts of my app.  The control over the serialzation and deserialization is very good and thought it would be well suited for my MVC application.

You might be thinking, why not just use the one that comes with .Net. It's in the box and is just as good. Well my preference was control, I wanted to control my model better and I wanted to output Json differently in different situations. So I created a new ActionResult that does just that but with the [Json.Net library](http://james.newtonking.com/pages/json-net.aspx).  Enjoy!

Example usage in any controller action:

{% highlight csharp %}
public ActionResult List(int Year, int Month)
{
    if (Year == 0)
        Year = DateTime.Now.Year;

    if (Month == 0)
        Month = DateTime.Now.Month;

    var calendarMonth = _calendarService.GetCalendarMonth(Year, Month, !this.IsAdmin());

    return new JsonNetResult(calendarMonth);
}
{% endhighlight %}

{% gist 606739 %}