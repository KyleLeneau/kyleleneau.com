---
layout: post
title: "Frustrating IIS7 Configuration 500 Error"
date: 2008-09-22 15:13
categories: Programming
---

Recently I have been putting a lot of my evenings and weekends in to a re-architecting of a site I host and develop for some friends of mine [Pert' Near Sandstone.](http://www.pertnearsandstone.com) The Entire site is built using ASP.Net and features a standard (web forms) website front end (public facing) and an admin side also built using web forms. I liked this at the time, but it soon became very difficult to debug, maintain and add features to.

The biggest factor in deciding the re-architect the site at the time was the lack of interoperability in the Admin side/application. It worked as intended about 60% of the time (60% of the time it works every time). The web forms admin side required a lot of code that was spread out over numerous code behind files, making it difficult to maintain. Not to mention similar logic was being duplicated, violating the DRY principal (don't repeat yourself).

Around the same time I had just finished my exploration of the new ASP.Net MVC (model-view-controller) model and had fallen in love with web development all over again. I had been in the process of creating some sample applications with it. I even started testing how it deployed on various web hosting platforms. I discovered that the MVC pattern DID work on IIS6 and IIS7. The URL's on IIS6 required special mapping (either adding .aspx or .mvc to map to the aspnet framework), I didn't like that so I found a host that offered IIS7. The URL's are now clean and to my liking. MVC makes sense, it creates clean separation of UI, business logic and data models. and will be an architecture of choice on ASP.Net.

So to make my long story short and to the point. I ended up re-architecting the Admin (once web forms side) of my site/project into a new MVC project in my solution. I started bringing over functionality one peice at a time, while reworking the underlying business logic and data access logic into various providers and repositories. I had everything working perfectly for a phase one deployment to the web host. I had 2 projects to deploy, one public facing site (web forms) and one admin MVC site. I set up the web host to use a virtual directory for the the MVC site, configured my connection strings as:
    
{% highlight xml %}
<connectionstrings>
    <add name="PertNear.Data.Properties.Settings.PertNearSandstoneConnectionString"
         connectionstring="server=secureserver.net;uid=user;pwd=pass;database=db"
         providername="System.Data.SqlClient"></add>
    <add name="PertNear.Membership"
         connectionstring="server=secureserver.net;uid=user;pwd=pass;database=db" 
         providername="System.Data.SqlClient"></add>
</connectionstrings>
{% endhighlight %}

I uploaded everything to the virtual directory and tried to access the new applications.  The public facing side (web forms) worked cause it had a separate config file, the admin side through the generic IIS7 internal server error with no messages.  I looked everywhere to find a solution.  Many sources said to add a wrapping element around the parent web.config so that it's settings don't conflict with the virtual directories (inheritance in IIS7 config files). I spent a week plus on this issue until I ran the config file through an XML validator.  As you can see I had a rouge comment tag in the config.  Had I known that IIS7 was first validating my config file I might have gotten an error along the lines of "invalid xml" instead of generic 500 error.

Reader be warned, be sure the validate the web.config file before uploading.  And check the config file before you make any drastic changes like I did (I moved the MVC project into the public facing site to now have just one project to deploy, thinking that might solve the issue).  One point worth mentioning, I had edited my published web.config outside of VS2008 in a text editor, hopefully VS would have caught that error for me had I known.

Good luck, happy coding and avoid the frustration I had.