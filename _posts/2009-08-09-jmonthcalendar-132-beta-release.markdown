---
layout: post
title: "jMonthCalendar-1.3.2-beta Release"
date: 2009-08-09 00:21
categories: Programming
---

I have released a new version of jMonthCalendar (1.3.2-beta).  Below I will provide a sample of the use of event callback as options.  Well this release is pretty straight forward for the most part.  It includes changes to how the custom events are fired mostly and addresses various bug fixes.  As well as includes some reduction in file size. **UPDATE** Beta2 is released to fix some minor bug issues.

Download location: [jMonthCalendar-1.3.2-Beta](http://jmonthcalendar.googlecode.com/files/jMonthCalendar-1.3.2-beta.zip)

The biggest change in this release is how events are handled.  Before I was not passing the DOM event back to you for control, I was simply just calling the methods you configured as options and passing parameters.  Now, the original DOM event is bubbled up to the custom event in most cases.  Along with the original DOM event I am also stuffing in the custom data for the callback into the [jQuery event object](http://docs.jquery.com/Events/jQuery.Event).

jQuery provides a nice way of encapsulating the original DOM event into a [jQuery event object](http://docs.jquery.com/Events/jQuery.Event).  A property on that object is 'data' (which can be waht ever I want).  So now, all custom events are mostly passed one single parameter (with the exception of onMonthChanging and onShowMoreClick); the jquery typed event.  Inside that event object I have put the data I want to send back, like the date or event object clicked on.  Don't worry I will get to a sample of what I am talking about.

First I will start off by showing you the old way of doing it prior to this release.

### OLD Way
    
    $().ready(function() {
        var options = {
            onMonthChanging: function(dateIn) {
                // this could be an Ajax call to the backend to get this months events
                alert("on month changing");
                // $.jMonthCalendar.ReplaceEventCollection(events);
            },
            onEventLinkClick: function(calEvent) { 
                // calEvent will be the calendar event you clicked on
                alert("event link click");
                return true; 
            },
            onDayLinkClick: function(dateIn) { 
                // date might be wrong here, held reference from last item
                alert(dateIn.toLocaleDateString());
            }
        };
        
        $.jMonthCalendar.Initialize(options, []);
    });

Okay, so the obvious problem with that is that there is no way to get to the original DOM event.

### NEW recommended Way
    
    $().ready(function() {
        var options = {
            onMonthChanging: function(dateIn) {
                // this could be an Ajax call to the backend to get this months events
                alert("on month changing");
                // $.jMonthCalendar.ReplaceEventCollection(events);
            },
            onEventLinkClick: function(event) { 
                // event is the jQuery event passed
                alert("event link click");
                // can get to the actual calendar event now through the Data property
                alert(event.data.Event);
                // want to prevent event bubbling use:
                event.stopPropagation();
            },
            onDayLinkClick: function(event) { 
                alert(event.data.Date.toLocaleDateString());
            }
        };
        
        $.jMonthCalendar.Initialize(options, []);
    });
