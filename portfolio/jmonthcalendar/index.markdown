---
layout: default
title: "jMonthCalendar"
date: 2009-01-08 09:37
comments: false
sharing: true
footer: true
---

jMonthCalendar is a full month calendar that supports events. You simply initialize the calendar with options and an events array and it can handle the rest. The plugin does have extension points that allow the developer to interact with the calendar when the display is about to change months, after the display has changed months and when the event bubbles are clicked on. jMonthCalendar now supports hover extension points, hover over an event and trigger an event like an alert(); By default the events would each have a URL supplied that would link to a details page.

**UPDATE**:  Please be sure to read my latest [post](/2009/08/09/jmonthcalendar-132-beta-release/) to see some of the new changes and to find out why it is in beta.

**NOW ACCEPTING DONATIONS!** - jMonthCalendar needs some better documentation and and demos. This site, my blog, can not fully provide that, and nor can Google Code. I want to expand my demos to showing examples of AJAX solutions and provide more source code examples. However, hosting doesn't come cheap and if you are using this plugin (and like it) and feel generous I could very much appreciate the help. Any dollar amount is appreciated. **Note: ** PayPal take a 3.4% commision on all donations. Please bare this in mind when donating.

![](https://www.paypal.com/en_US/i/scr/pixel.gif)

**Links**
[Google Code Home (Source/Wiki)](http://code.google.com/p/jmonthcalendar/)
[Downloads](http://code.google.com/p/jmonthcalendar/downloads/list)
[jQuery Project Home Page](http://plugins.jquery.com/project/jMonthCalendar)
[Documentation and Samples](/2009/08/09/jmonthcalendar-options-events-methods-documentation/)

### Features
  * jQuery 1.3.2 Compatible
  * Ability to Load events

### Change Log

  * Release 1.3.2-beta
    * Better event callback support
    * Various bug fixes related to callback
  * 6/17/2009 Release 1.3.0-beta
    * Events that span multiple days with continuation over days, weeks, months, years.
    * jQuery 1.3.2 Support
    * Events are now pre-sorted for multi day events on top.
    * Show More Events setting/hoot that passes the days worth of event object as an array.
    * Start of jQuery UI theme support, arrows for spanning events.
    * Removed initialize for static height and width, now all set on the main calendar using CSS (everything else is dynamic).
    * Note: you must specify an EventID in the event objects, they are required now.
  * Release 1.2.2
    * Drag and Drop Events
    * Dragable Events support using jQuery UI (Optional usage).
    * Add ability to enable or disable calendar links (today link, next year, and previous year).
    * Default Next and Previous link text changed.
    * Added onDayCellDblClick event that passes the date you are double clicking.
    * Added onEventDropped event that passes the event object and the new date being dropped into.
    * Removed my custom Date extensions and replaced it with [Datejs](http://www.datejs.com/), more on this below.
    * Complete Build Process to build, pack and minify the source.
  * 3/24/2009 Release 1.2.1
    * New Project Home: [http://code.google.com/p/jmonthcalendar/](http://code.google.com/p/jmonthcalendar/)
    * Bug fixes for UTC Date Parsing
    * Stop Event Propogation
    * ANT Build Process
    * Fix Day Cell click and Day click
  * 2/12/2009 Release 1.2.0
    * New extension points for working with the day cells or links
    * Changed navigation header layout
    * Added year navigation, works the same as month navigation
    * Added a today link to return to today's date
    * Date formatting the parsing JSON improvements
    * Updated sample for AJAX call, should happen onMonthChanging
  * 2/12/2009 Minor Release 1.1.1
    * Events are drawn immediately after month is drawn.
    * Fixed configurable height and width in options
    * Fixed configurable height of headers in options
    * JSON Date formatting/parsing (ISO, new Date literal, UTC)
    * EndDate property added to event object
    * Date is now deprecated, replace by StartDate
    * Event in calendar has new ID of 'Event_' + EventID, allow styling of specific events
  * 1/29/2009 Minor Release 1.1.0
    * Event onHover Extension Point added.
    * Extend event object to include description and escape JSON.
    * Extend the event object to accept "class" css class.
    * Minor bug fixes to placement of events.
  * 1/20/2009 Patch Release 1.0.1
    * Event loading (isArray is not a function)
    * Month Name not displayed in IE
    * Configurable first day of week (0 for Sunday, 1 for Monday, etc)	
  * 1/18/2009 Initial Release

### Uses & Code Examples

The simplest way to use the plugin use this html some place in your page:

And use this Javascript:
    
    $().ready(function() {
        var options = { };
        var events = [ ];
        $.jMonthCalendar.Initialize(options, events);
    });

If you want to get more advance an tie into some of the configurable options you can use this as your options variable.  You can see how you can set the extension handles here to fire custom code at points.  You can also see that the month names can be localized easily. Notice the new onEventBlockOver and onEventBlockOut; this would allow you to signal an alert or a type of balloon pop-up.

    var options = {
        containerId: "#jMonthCalendar",
        headerHeight: 50,
        firstDayOfWeek: 0,
        calendarStartDate:new Date(),
        dragableEvents: true,
        activeDroppableClass: false,
        hoverDroppableClass: false,
        navLinks: {
    	enableToday: true,
    	enableNextYear: true,
    	enablePrevYear: true,
    	p:'Ã¢â‚¬Â¹ Prev',
    	n:'Next Ã¢â‚¬Âº',
    	t:'Today',
    	showMore: 'Show More'
        },
        onMonthChanging: function(dateIn) { return true; },
        onMonthChanged: function(dateIn) { return true; },
        onEventLinkClick: function(event) { return true; },
        onEventBlockClick: function(event) { return true; },
        onEventBlockOver: function(event) { return true; },
        onEventBlockOut: function(event) { return true; },
        onDayLinkClick: function(date) { return true; },
        onDayCellClick: function(date) { return true; },
        onDayCellDblClick: function(dateIn) { return true; },
        onEventDropped: function(event, newDate) { return true; },
        onShowMoreClick: function(eventArray) { return true; },
        locale: {
    	days: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    	daysShort: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
    	daysMin: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa", "Su"],
    	months: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
    	monthsShort: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
    	weekMin: 'wk'
        }
    };

As for the events, this is how I have set them up to be handled, if you need something different you can modify the source of the plugin or easily map to these object/array.  I plan on using this plugin in an MVC application and will just serialize my event object to JSON for this plugin.
    
    var events = [
        { "EventID": 1, "StartDateTime": new Date(2009, 5, 12), "Title": "10:00 pm - EventTitle1", "URL": "#", "Description": "This is a sample event description", "CssClass": "Birthday" },
        { "EventID": 2, "StartDateTime": "2009-05-28T00:00:00.0000000", "Title": "9:30 pm - this is a much longer title", "URL": "#", "Description": "This is a sample event description", "CssClass": "Meeting" },
    ];

You are not limited to just loading the events the first time the calendar is initialized.  You can do an AJAX call and retrieve more events from your server based on the date that the calendar is changing to.  You can also add events to the calendar through an exposed method. _Note: the method to use an AJAX call should be onMonthChanging. This event fires before the calendar and events are drawn_
    
    //Set a function to get more events, this could be an AJAX call to the server as well.
    var options = {
        onMonthChanging: function(dateIn) {
            //this could be an Ajax call to the backend to get this months events
            var events = [
                { "EventID": 1, "StartDateTime": new Date(2009, 6, 1), "Title": "10:00 pm - EventTitle1", "URL": "#", "Description": "", "CssClass": "Birthday" },
                { "EventID": 2, "StartDateTime": new Date(2009, 6, 2), "Title": "9:30 pm - this is a much longer title", "URL": "#", "Description": "", "CssClass": "Meeting" }
            ];
            $.jMonthCalendar.ReplaceEventCollection(events);
            return true;
        }
    };
    
    //on a button click, add more the the calendar.
    $("#Button").click(function() {
        //extraEvents could be a call to the server or anything else that can produce a JSON array
        $.jMonthCalendar.AddEvents(extraEvents);
    });
    
    //you could also set/change the month from an external source
    $("#ChangeMonth").click(function() {
        $.jMonthCalendar.ChangeMonth(new Date(2009, 5, 7));
    });

### Demo

Should you have any issues with the plugin you can either leave a comment here with the details of your browser (name and version), post an issue at the Google Code home page [here](http://code.google.com/p/jmonthcalendar/issues/list) (login to create an issues), or worst case email me at [kyle.leneau@gmail.com](mailto:kyle.leneau@gmail.com).  Please provide as much detail as you can, such as browser name/version, along with the version of jQuery your using.  I will try to get to issues as quick as possible, but if you know or have the solution that will help even better.  Thanks, Kyle.