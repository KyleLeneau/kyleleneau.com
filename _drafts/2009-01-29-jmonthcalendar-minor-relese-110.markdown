---
layout: post
title: "jMonthCalendar: Minor Relese 1.1.0"
date: 2009-01-29 22:45
categories: Programming
---

I just finished posting a updated release for jMonthCalendar that can be found [here](/portfolio/jmonthcalendar). This release mostly consists of a few bug fixes and a new features that have been suggested by fellow supporters (people who post comments, issues and suggestions, and anyone else I've missed). To those and everyone else I say: Thank you.

Most of the bug fixes are internal but one notable thing I changed in my sample's is the Event object JSON string. I have also extended the Event object to accept a CssClass and Description properties. 

{% highlight csharp %}
//Before, (notice the lack of quotes to identify the property)
var events = [
    { EventID: 1, "Date": new Date(2009, 1, 1), "Title": "10:00 pm - EventTitle1", URL: "#" },
    { EventID: 2, "Date": new Date(2009, 1, 2), "Title": "9:30 pm - this is a much longer title", URL: "#" }
];

//After: new properties and quotes property strings (better JSON)
var events = [ 
    { "EventID": 1, "Date": new Date(2009, 1, 1), "Title": "10:00 pm - EventTitle1", "URL": "#", "Description": "This is a sample event description", "CssClass": "Birthday" },
    { "EventID": 2, "Date": new Date(2009, 1, 2), "Title": "9:30 pm - this is a much longer title", "URL": "#", "Description": "This is a sample event description", "CssClass": "Meeting" }
];
{% endhighlight %}

The new properties will allow for two things. One, the CssClass is placed onto the event block so that it can be styled with css easily. This could also be used like an event type or category. Second, the description allows for a more information, this is in conjunction with the feature below.

An exciting new feature for some is the ability execute custom code (extension point) when hovering over/out an event. This will provide the ability to do something with the hovered event, like display a ballon/pup-up. The new feature is part of the options construct so it should be define like the example below.

{% highlight javascript %}
var options = {
    onEventBlockOver: function(event) {
        //of course this is rude example but you could to anything here and pass property values to it.
        //Example, you could create UI ballon and display (set the scope higher) then destroy or close it on out.
        alert(event.Title + " - " + event.Description);
        return true;
    },
    onEventBlockOut: function(event) {
        return true;
    }
};
{% endhighlight %}

This was my solution to a comment that someone wanted balloon like pop-ups. I didn't want to have to mess with that since it deals with positioning and calculations that I am not comfortable with spending the time on it now.  My continued goal of this project is to avoid dependencies, with the exception of jQuery sponsored projects.

Please keep up the comments for suggestions, issues, requested features, and anything else you think I might like. Thanks for the support.