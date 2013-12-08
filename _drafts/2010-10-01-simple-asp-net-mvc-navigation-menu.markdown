---
layout: post
title: Simple Asp.Net MVC Navigation Menu
date: 2010-10-01 13:44
categories: Programming
---

Well it's October first, it has been a really long time since I have last written anything. Oh well.  Recently I have been working on applying some updates to an MVC site I maintain, as usual I updated the dependencies, ran some tests, and looked over the code.  It's been a while since I last opened the project since it has been in production.  Of course, I was not happy with a couple things in the application and was constantly fixing the same bugs in the navigation menu.

There are always the same questions with a navigation menu, how do you render the html, how do you know what item is selected, how to achieve 2 level menus, and how do you trim by security.  To give some history; I went from defining only a single level with no selection (action links in an un-ordered list).  Then I found a project on <a href="http://codeplex.com/">codeplex</a> called <a href="http://mvcsitemap.codeplex.com/">ASP.NET MVC SiteMap Provider</a>, this is great it has a ton of features, fits the provider model of ASP.Net, easy to define and use in simple cases.  Unfortunately, it is not as mature as I would like.  Plus it adds another dependency that is hard to work with and does not always work the way I would expect it to.  Needless to say it is buggy (my opinion and experience only, others may differ).

Which brings me to my subject line.  I wanted to create my own navigation system and have full control over the levels, rendering and selection of the items. Perfect, I needed a partial to render the menu and top level items in my own un-ordered list. I also needed some helpers to render those items in my partial, in this case the top level is a list of my controllers. 

{% highlight html %}
<ul id="navigation">
	<%= Html.NavItem("Home")%>
	<%= Html.NavItem("Calendar")%>
	<%= Html.NavItem("Media")%>
	<%= Html.NavItem("Messages", "Forum", "Index")%>
	<%= Html.NavItem("Goods", "Catalog", "Index")%>
	<%= Html.NavItem("Links", "Link", "Index")%>
	<%= Html.NavItem("Contact")%>
	<%= Html.LoginStatusNavItem() %>
</ul>

<div class="clearboth"></div>

<ul id="subnavigation">
	<%= Html.SubNavListItems() %>
	<%= Html.NavItem("Join Our Mailing List!", "Contact", "MailingList") %>
</ul>
{% endhighlight %}

I also added a helper to render the login/logout link in the navigation based on whether the request was authenticated.  The second level navigation was where the work came in. Essentially I wanted to render some of the actions from the current controller based on a attribute assigned to the action. The rending will then sort the list based on the sort order and perform security trimming.

{% highlight csharp %}
[NavigationItem("About Us", 0)]
public ActionResult Index()
{
	return View("Index", GetIndexModel());
}

[NavigationItem("Secured Page", 0), Authorize]
public ActionResult Admin()
{
	return View("Index", GetIndexModel());
}
{% endhighlight %}

In order to do that I created a custom Attribute to store the link text and the order it should be in.

{% highlight csharp %}
[AttributeUsage(AttributeTargets.Method, Inherited = false, AllowMultiple = false)]
internal sealed class NavigationItemAttribute : Attribute
{
	public NavigationItemAttribute(string text) : this(text, 0) { }

	public NavigationItemAttribute(string text, int order)
	{
		Text = text;
		SortOrder = order;
	}

	public string Text { get; private set; }
	public int SortOrder { get; set; }
}
{% endhighlight %}

After that I needed a way to cache all this information in order to look it up later from my helpers. Populating this cache involves doing some basic reflection and type checking of controller actions. Then storing the results in a dictionary based on controller name as the key and a list of actions with the NavigationItemAttribute (stored as a ControllerNavigationItem, which is a POCO object to store data).  Since I only wanted to do this reflection once, I created a singleton to do the work.

{% gist 606514 %}

Finally to render the second level navigation I look up the list based on the current controller and loop over the items, only rendering the secure and authenticated items or the public items in the order defined by the attribute.

In hindsight, there are some things I could have made better or more features I could support. Currently it just checks to see if your logged in and doesn't take into account any specific roles on the action.  Also it lacks support for MVC 2 Areas, but I don't have any yet so I will cross that bridge when I get to it. This solution was simply an exercise for me in creating a singleton, using reflection to find controllers and actions, and to fill a common need in an ASP.Net MVC application.  Hope you found this interesting or useful.

Download the code <a href="http://gist.github.com/gists/606514/download">here</a> or check out the <a href="http://gist.github.com/606514">Gist</a> on <a href="http://github.com">Github</a>