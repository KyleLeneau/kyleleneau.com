---
layout: post
title: "jMonthCalendar: A jQuery Event Calendar"
date: 2009-01-18 12:46
categories: Programming
---

While working on a project conversion to MVC I realized I needed a full month calendar that supported events.  None existed so I spent a few evenings learning jQuery and developing my own.  I just recently posted new pages on the project and submitted the plugin to jQuery.

Recently I have been working on a re-architecture of [PertNearSandstone.com](http://www.pertnearsandstone.com).  I have been converting the project into a full MVC application (previously Webforms).  Part of the application features displaying upcoming events/shows on a calendar for visitors.  In the previous Webforms world this was easy, I could throw an Asp.Net Calendar on the page and tie into the instances events to display what I wanted on the calendar.  Well MVC does not like the runat tag and thus can not use the same control in the new app.

I searched the web for a replacement, I thought that someone would have made something to fulfill this requirement.  All I could find were Javascript pop-up calendar like the ones you see next to input fields.  Since I couldn't find one I thought I would start on my own adventure into learning jQuery (since I have heard good things about it) and creating my own.  That is where I cam up with [this](/portfolio/jmonthcalendar) full month calendar that can display events and provide some minor extension points for custom code.

Overall I am very pleased and excited about this.  This is close to my first sole open source project and is a major accomplishment for my JavaScript skills; not to mention that I was successfully able to learn jQuery and develop a plugin for it.  I am giving back to the jQeury community who helped me out, if you would like a copy of this please visit [jMonthCalendar jQuery Plugin page](http://plugins.jquery.com/project/jMonthCalendar).  To see code samples and demos of the plugin please visit my projects page [here](/portfolio/jmonthcalendar)