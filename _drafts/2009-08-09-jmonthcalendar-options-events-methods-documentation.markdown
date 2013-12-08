---
layout: post
title: "jMonthCalendar Options, Events, & Methods Documentation"
date: 2009-08-09 15:09
categories: Programming
---

In this post I am going to cover all the custom event/options as well as methods that can be configured and used in jMonthCalendar.  All of these are options that can be supplied at initialization in order to manipulate the calendar further or be able to tie into some additional logic or rules.  As well as methods that are exposed for manipulating the calendar after initialization.  This is my first attempt at formal documentation, so bare with me.

## Options

### containerId - default: #jMonthCalendar

Use this to configure where your calendar should be placed in the page. You must have a matching DOM element with the ID
    
    $.jMonthCalendar.Initialize({ containerId: '#MyContainerId' }, null);

### headerHeight - default: 50

This sets the height of the navigation header.
    
    $.jMonthCalendar.Initialize({ headerHeight: 50 }, null);

### firstDayOfWeek - default: 0

This determines which day of the week weeks should start on (default 0 refers to sunday). Monday is 1, Tuesday is 2, etc.
    
    $.jMonthCalendar.Initialize({ firstDayOfWeek: 1 }, null);

### calendarStartDate - default: new Date()

This determines which month to display when the calendar is first loaded. The default is to start in the current month (today).
    
    $.jMonthCalendar.Initialize({ calendarStartDate: new Date(2009, 1, 1) }, null);

### dragableEvents - default: true

This determines weather or not you want event blocks to be dragable. Note this depends on jquery.ui.dragable.
    
    $.jMonthCalendar.Initialize({ dragableEvents: false }, null);
    
### dragHoverClass - default: 'DateBoxOver'

This is the css class that is added when an element is being hovered over an acceptable date cell.
    
    $.jMonthCalendar.Initialize({ dragHoverClass: 'SomeCssClass' }, null);
    
### navLinks (object of values)

These are the label text and switches to determine the header navigation.
    
    $.jMonthCalendar.Initialize({ 	
    	navLinks: {
    		enableToday: true,
    		enableNextYear: true,
    		enablePrevYear: true,
    		p:'‹ Prev', 
    		n:'Next ›', 
    		t:'Today',
    		showMore: 'Show More'
    	}
    }, null);

## Events

### onMonthChanging

This event is triggered upon changing the calendar's month. If the callback function returns false, the change will be prevented. Note: this would be an excelent point to do an AJAX call for the next months events.
    
    // supply this callback as an option with the collowing signature
    $.jMonthCalendar.Initialize({
        onMonthChanging(newDate) { ... }
    }, null);
    
    // AJAX call sample for more events
    $.jMonthCalendar.Initialize({
        onMonthChanging(newDate) { 
            
        }
    }, null);

### onMonthChanged

This event is triggered after calendar's month has been changed.
    
    $.jMonthCalendar.Initialize({
        onMonthChanged(event, newDate) { ... }
    }, null);

### onEventLinkClick

This event is triggered when the anchor tag of the event is clicked. Note: good place to link out to another page.
    
    $.jMonthCalendar.Initialize({
        onEventLinkClick(event) { 
            alert(event.data.Event);
        }
    }, null);

### onEventBlockClick

This event is triggered when the div container of the event is clicked. Note: this our the link click would be a good place to show tooltips.
    
    $.jMonthCalendar.Initialize({
        onEventBlockClick(event) { 
            alert(event.data.Event);
        }
    }, null);

### onEventBlockOver

This event is triggered when your mouse is over the event div container.
    
    $.jMonthCalendar.Initialize({
        onEventBlockOver(event) { 
            alert(event.data.Event);
        }
    }, null);

### onEventBlockOut

This event is triggered when you mouse moves off the event div container.
    
    $.jMonthCalendar.Initialize({
        onEventBlockOut(event) { 
            alert(event.data.Event);
        }
    }, null);

### onDayLinkClick

This event is triggered when the user clicks on the label of the day (number in upper right corner)
    
    $.jMonthCalendar.Initialize({
        onDayLinkClick(event) { 
            alert(event.data.Date);
        }
    }, null);

### onDayCellClick

This event is triggered when the user clicks on the cell that contains the event div containers.
    
    $.jMonthCalendar.Initialize({
        onDayCellClick(event) { 
            alert(event.data.Event);
        }
    }, null);

### onDayCellDblClick

This event is triggered wehn the user double clicks ont eh cell that contains the event div containers.
    
    $.jMonthCalendar.Initialize({
        onDayCellDblClick(event) { 
            alert(event.data.Event);
        }
    }, null);

### onEventDropped

This event is fired after a user drags and drops and event onto a new day.
    
    $.jMonthCalendar.Initialize({
        onEventDropped(event, calEvent, newDate) { 
            alert(calEvent);
            alert(newDate);
        }
    }, null);

### onShowMoreClick

This event is triggered when the user wishes to "see more" events than what can be displayed in the cell. Note: this would be a good place to use a tooltip or dialog as well.
    
    $.jMonthCalendar.Initialize({
        onShowMoreClick(dayEvents) { 
            // dayEvents is an array of events 
            alert(dayEvents.length);
        }
    }, null);

## Methods

### Initialize(options, eventArray)

This is the main method needed to be called to get a calendar on the page. You can initialize it with the options and event callbacks mentioned above to get a more custom plugin.    
    
    $.jMonthCalendar.Initialize({ containerId: '#MyContainerId' }, []);

### ChangeMonth(newDate)

This method will change the current selected month of the calendar. This method will fire the callback onMonthChanging and onMonthChanged.
    
    $.jMonthCalendar.ChangeMonth(new Date(2009, 1, 1));

### ReplaceEventCollection(eventArray)

This will replace all events in the plugin with the new event array passed in. This will clear all existing events being displayed and redraw all the events after the replacement.
    
    $.jMonthCalendar.ReplaceEventCollection([]);

### AddEvents(eventArray)

This method will add a single event to the plugin or an array of events by merging into the existing array of events. After which the method will clear all visible event on the calendar and draw the events in the updated array.
    
    $.jMonthCalendar.AddEvents([]);

### ClearEventsOnCalendar()

This method will remove all the events in the plugin and and remove any being displayed.
    
    $.jMonthCalendar.ClearEventsOnCalendar();
