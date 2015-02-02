---
layout: post
title: "ASP.Net MVC Areas/Modules"
date: 2008-12-03 13:40
categories: Programming
---

[In this post Phil Haack explains how Areas can be accomplished in the ASP.Net MVC framework.](http://haacked.com/archive/2008/11/04/areas-in-aspnetmvc.aspx)

I really like this idea of have Areas or Modules in ASP.Net MVC. I have been in the process of developing a Forum for a website and came across this after I was complete. I thought that "yes it would be nice to use this same logic in another application", and having an areas or module to move around would be quite nice.

One thing I would expand upon is the idea of creating a self contained binary (dll) that can be referenced into the main project. This would mean that all the views and resources would have to be statically defined in the binary, but could be easily re-styled with CSS. You'd probably also have to define a configuration element in your web.config that defines database connections and other information important/configurable to the Module/Area.

We'll see how time permits for a prototype. Not something I need now but is cool to think of. I wish the ASP.Net MVC guys/gals would include this functionality of segregated sections/areas/modules in a future release of ASP.Net MVC.
