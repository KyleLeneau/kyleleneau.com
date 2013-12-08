---
layout: post
title: "My Octopress Workflow"
date: 2012-01-14 23:03
comments: true
published: false
categories: 
---

### The workflow to produce content

One thing that I am going to have to get used to is how to produce content on a timely basis. Octopress does not make it the easiest to do from anywhere in the world. Thankfully, I am usually not far from my computer or an internet connection so my workflow for publishing Octopress and keeping my blog under source control is as follows:

```
git pull origin site				# This will update my working source with the latest
rake new_post["Some New Title"]		# This will create a new post for me
```

After I have created the file I will use [TextMate](http://macromates.com/) on my Mac to find and open it up to edit the content