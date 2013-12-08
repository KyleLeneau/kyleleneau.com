---
layout: post
title: "Getting Started with jMonthCalendar"
date: 2009-06-12 11:46
categories: Programming
---

So you are interested in using jMonthCalendar and are unsure how to start using it...?  Well hopefully I can give the 5 minute startup that will help you along the way.  In this post I will show you how to install and place a calendar on the page as well as show you how to populate the calendar with some events. Easy enough right?  I hope so.

Getting started with jMonthCalendar is really quite easy, it is like any other Javascript library or jQuery plugin in that it requires a Javascript file and reference in the page.

### Step 1 - Download

Well you will first need a copy of jQuery if you don't already have one, I recomend jQuery 1.3.2 which can be found [here](http://docs.jquery.com/Downloading_jQuery#Current_Release), you either want the uncompressed version or the compressed version depending on your preferences.

You will will also need a copy of jMonthCalendar which can be downloaded [here](http://jmonthcalendar.googlecode.com/files/jMonthCalendar-1.3.1-beta.zip).  The download contains the Javascript files, a sample html page, and some default css (which can be changed to suit your needs).

### Step 2 - Include in Html

After the files are downloaded you will want to move them to a directory in your project/website that can be references either relativley or absolutly.  You'll want to include a reference to the jQuery file you downloaded as well as the jMonthCalendar plugin.  You can place these references in the head of the html or the body, with Javascript it is all the same. You'll want to put these two line in your html document:
       
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js" type="text/javascript"></script>
    <script src="js/jMonthCalendar.js" type="text/javascript"></script>
    
If you want to use the default styles now is the time to either copy the contents of the core.css (from the jMonthCalendar download) into your css file or include a reference in the head like so:
  
    <link href="css/core.css" type="text/css" rel="stylesheet"></link>	

### Step 3 - Create place holder in the Html body

In order to draw the calendar on to the page, the plugin needs to know where to put it.  Add and empty div tag someplace in the body of the html like so: (The ID of the div is VERY important, you can change the ID but you must tell the plugin what it should look for through the options.)
    
    <div id="jMonthCalendar"></div>	

### Step 4 - Initialize calendar on page load.

To draw the calendar after the page has loaded you will need to hook up that standard jQuery onLoad event.  This usually happens once on the page and is surrounded in a script block at either the top or the bottom of the page.  The safest place to do this is with another script block right after step 2.  This will create the calendar and draw it on the screen using the empty div you created in step 3.
    
    <script type="text/javascript">
        $().ready(function() {
    	$.jMonthCalendar.Initialize(null, null);
        });
    </script>

Thats it! That is all you need to do in order to display the calendar on te page. There are of course configurable options and events that you can tie into to perform advanced operations but I will save that for another post. The next topic I will cover is, "okay now what...", how to load events into the calendar.

**Update:** Added the first bits of documentation for the plugin [here](/2009/08/09/jmonthcalendar-options-events-methods-documentation/).