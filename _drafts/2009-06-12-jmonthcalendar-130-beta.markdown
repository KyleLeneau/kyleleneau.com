---
layout: post
title: "jMonthCalendar 1.3.0 Beta"
date: 2009-06-12 11:45
categories: Programming
---

**jMonthCalendar has reached a new milestone!** It now supports multi-day events (events that span multiple days).  Plus it retains all the same features as before including drag and drop and event stacking. This release is a huge change from the previous version and is thus labeled as Beta.  Most significant to the change is how events are rendered onto the calendar. In this post I am going to go over the new features and how they will affect existing users. I will also try to cover some of the new functionality and how it might be used.

**Change Log**

* Events that span multiple days with continuation over days, weeks, months, years.
* jQuery 1.3.2 Support
* Events are now pre-sorted for multi day events on top.
* "Show More Events" setting/hoot that passes the days worth of event object as an array.
* Start of jQuery UI theme support, arrows for spanning events.
* Removed initialize for static height and width, now all set on the main calendar using CSS (everything else is dynamic).
* Note: you must specify an EventID in the event objects, they are required now.

The biggest change to this release is the fact that multi-day events are being drawn now. In order to add this I had to make a huge amount of changes under the hood and thus I am adding a Beta to the release to warn people. At the same time I want to see how it behalves for people and fix any issues people might have.

In the last release events were being appended into the table cell tag of the specified day. This created huge problems as you can't do a column span on the event easily, plus how are you supposed to handle overflow and events that wrap over weeks or months. So I chose to rewrite how the events were drawn and make them absolutely positioned. I also added an object for each day on the calendar and set some properties, that made it a lot easier to reference the object from an array and grab the days worth of events.

Some people may look into this and think that I have missed how to display "More Events" (events that overflow the day). I have left this out and added a hook instead. I was unable to settle on an implementation and with so many other good balloon pop ups, I thought I would leave it up to you. There is a new hook called onShowMoreClick that passes an array of events to it. The array of events is a representation to all the events for that day, including the non-visible ones. I hope to provide a series of usage posts on how this might be done using my favorite plugins.

One last piece of information is regrading drag and drop events. They are supported with multi-day events even. They will fire the same hooks as in the past: onEventDropped (passing the event and the new date).

Please let me know what you think in the comments, I am very proud of where this plugin has come so far and hope to keep pushing it's feature set. If you experience any issues please feel free to leave a comment, email, or better yet; file an issue over at the Google Code Home page.

[Download From Google Code](http://jmonthcalendar.googlecode.com/files/jMonthCalendar-1.3.0-beta.zip)**
**