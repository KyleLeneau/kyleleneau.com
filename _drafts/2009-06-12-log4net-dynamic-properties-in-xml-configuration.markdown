---
layout: post
title: "log4net Dynamic Properties in XML Configuration"
date: 2009-06-12 11:34
categories: Programming
---

I just learned about a new feature today of log4net that would have saved me a few hours of time had I known or been able to find this earlier. I learned that you can have dynamic properties stored into log4net's global context from code and then access them from the XML configuration file. This is useful in the case where dynamic configuration of log4net is needed.

**My Case:** I have been building console application that will run nightly to sync some integration records and I wanted to setup logging in order to see that status of the job and gather some reporting information (counts, time run, etc). There was a catch though this process would run multiple times in a night but each time for a different customer. This would make it difficult to read the logs for a particular customer as all I would have to go on is the file date and time.

I needed a way to break my log files into different customers yet retain the rolling file appender features of log4net. My first pass at with was to configure log4net using the basic configurator all in code and create the appender, with a dynamic file name, and set the level of the logger programmatically. This was not my preferred way but was my only hope to getting the application out of development. Then I found how to set properties into log4net's global context and access them through the configuration file. I did run into a small problem that my app.config file was not being read in so I had to add these two variable to my assembly.    
    
    [assembly: log4net.Config.XmlConfigurator(Watch = true)]
    [assembly: log4net.Config.Repository]

My goal was to make the file name dynamic based on the CustomerID passed into the application. Please not the file tag as it is the ticket to my case.
    
    <log4net>
        <root>
            <level value="INFO"></level>
            <appender-ref ref="RollingLogFileAppender"></appender-ref>
        </root>
    
        
        <appender type="log4net.Appender.RollingFileAppender" name="RollingLogFileAppender">
            <file type="log4net.Util.PatternString" value="logs\logFile_%property{BrokerID}.txt"></file> 
            <appendtofile value="false"></appendtofile>
            <rollingstyle value="Size"></rollingstyle>
            <maxsizerollbackups value="-1"></maxsizerollbackups>
            <maximumfilesize value="50GB"></maximumfilesize>
            <layout type="log4net.Layout.PatternLayout">
                <conversionpattern value="%date [%thread] %-5level %logger - %message%newline"></conversionpattern>
            </layout>
        </appender>
    </log4net>

Here is a sample of my log4net configuration section.  Please note the file tag and type attribute to be log4net.Util.PatternString. The pattern of the value is important to, it must be %property{property_name} to get the right replacement. This is the ticket to dynamic values.
    
    private static void InitLogger()
    {
        //This is freaking awesome, put a property into the log4net context and using the 
        //  log4net.Util.PatternString type you can dynamically set values for the logging context from code.
        log4net.GlobalContext.Properties["CustomerID"] = (CustomerID!= 0) ? CustomerID.ToString() : "Error";
    }

Here is an example of my small InitLogger.  This method is the very first item to be called when the main routine starts up. All that needs to be done now is get a logger and start logging.  A file will be created based on the CustomerID which in this case is retrieved from the command line arguments before InitLogger is called. If no CustomerID is passed in than the file will be to logFile_Error.txt
    
    private static ILog Logger;
    
    static void Main(string[] args)
    {
        if (args.Length > 0)
            CustomerID= Util.GetInt(args[0]);
    
        InitLogger();
        Logger = LogManager.GetLogger("Process");
    }

Pretty cool I think, I hope this saves people some headaches.  I wish I would have found this a few days ago.  Oh well it is to my benefit to learn.  Happy coding.