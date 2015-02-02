---
layout: post
title: "jMonthCalendar: Minor Release 1.2.2"
date: 2009-05-01 09:02
categories: Programming
---

Well it has been awhile since I posted anything new so I thought that I would provide a rundown of the minor new features and fixes in jMonthCalendar 1.2.2

New Features:
	
  * Dragable Events support using jQuery UI (Optional usage).	
  * Add ability to enable or disable calendar links (today link, next year, and previous year).	
  * Default Next and Previous link text changed.	
  * Added onDayCellDblClick event that passes the date you are double clicking.	
  * Added onEventDropped event that passes the event object and the new date being dropped into.	
  * Removed my custom Date extensions and replaced it with [Datejs](http://www.datejs.com/), more on this below.	
  * Complete Build Process to build, pack and minify the source.

The drag and drop stuff is pretty cool and makes the calendar even slicker.  Have to provide props to the reader ([Mattias Jakobsson](http://mattias-jakobsson.net/Item/19/Extended%20jMonthCalendar%20with%20drag%20n%20drop)) who took it upon their own to add it in.  With the addition of the event when the event is dropped this would allow a developer to update an event using AJAX, allowing the user to easily reorganize events.  jQuery UI is not a dependency and this feature is totally optional.

As for the date extension stuff, it was not something I wanted to maintain, and didn't use that often.  I hope to add another option in the setup to allow for a date parsing options on the inbound JSON.

Another item I am proud of is a unified build process.  I wanted to make releases as easy as possible so I thought I would spend some time learning ANT and looking at other scripts (jQuery, Dojo, and other projects for JavaScript).  I managed to write a pretty neat ANT script that will produce all the artifacts for a release and zip it up.  I will save the details for another post.

The last point I will mention is now the ability to override the navigation links and turn them on or off depending on your usage.  This was asked for and was a simple addition to source.  If you have any suggestions, send them along I will add them in to the source if I feel they fit the project goal.  Below is an updated definition of all the options available for the plugin.

FYI: The next release will make a change in how the calendar is sized and will absolutely position events over the calendar for Multi Day Event capabilities.

{% highlight javascript %}    
var defaults = {
	height: 650,
	width: 980,
	navHeight: 25,
	labelHeight: 25,
	firstDayOfWeek: 0,
	calendarStartDate:new Date(),
	dragableEvents: false,
	activeDroppableClass: false,
	hoverDroppableClass: false,
	navLinks: {
		enableToday: true,
		enableNextYear: true,
		enablePrevYear: true,
		p:'‹ Prev', 
		n:'Next ›', 
		t:'Today'
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
	locale: {
		days: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
		daysShort: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
		daysMin: ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa", "Su"],
		months: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
		monthsShort: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
		weekMin: 'wk'
	}
};
{% endhighlight %}