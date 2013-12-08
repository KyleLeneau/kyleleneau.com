---
layout: post
title: "jMonthCalendar: Minor Release 1.2.0"
date: 2009-02-12 13:04
categories: Programming
---

Wow, let me first start by saying it has been too long since I posted any updates on jMonthCalendar.  I hope that the new release of jMonthCalendar 1.2.0 excites you as much as it does me.  1.2.0 sets the stage for some pretty cool stuff. Continue reading to see a short list of the new features and where this project is going next.

On the short list of new features there is:	

* Today Link (navigate back to today's date)
* Year navigation, jump to '10 or back to '08 in the active month
* Ability to click a day cell or day link and fire your own custom logic (i.e. add event on that day)
* JSON date parsing, parse what some from that event object if the calendar is un-aware.
* Fixed in-line sizing, configurable by options construct
* Deprecating Date property, replaced by StartDate
* Added EndDate property to event object

While not all of all of them seem flashy, the last three or four points make the calendar that much closer to having multi-day events and event overflow support.

I am happy to report that I am currently using the calendar on an ASP.Net MVC site on my development machine. I hope to have a new calendaring system ready soon. This should concern you only because when I find issues while developing and using it, I fix them and everyone benefits. In more detail my calendar does a JSON GetData call to a controller actions, which executes and returns JSON formatted events. I am using [James Newton-King's JSON.Net](http://james.newtonking.com/projects/json-net.aspx) library to map and serialize my C# objects. I use the attributes on my properties to rename or exclude them from serialization. Very nice library and commend James for the work.