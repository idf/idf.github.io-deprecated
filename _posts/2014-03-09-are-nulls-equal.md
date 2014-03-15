---
layout: post
title: "Are nulls equal?"
description: "It depends"
category: Computer Science
tags: []
---
{% include JB/setup %}

In Python:

{% highlight python %}
None==None # return True, invoking __eq__ method 
None is None # return True, identity test, for singleton
{% endhighlight %}
In Java: 

{% highlight java %}
null==null // return true
null.equals(null) // NullPointerException
{% endhighlight %}
In SQL:

{% highlight sql %}
null = null -- evaluate to False if set ansi_nulls off
null = null -- evaluate to True if set ansi_nulls on
null IS null -- evaluate to True
{% endhighlight %}
###Java
To be more pricise, there is a slight difference between null and 0 depending on compilers. Jimple/Java distinguishes between 0 and null, whereas Dalvik does not.
###SQL
For SQL, the reason of evaluating null = null to false is like considerting null as "unknown" in that case (or "does not exist"). In either of those cases, you cannot say that they are equal, because you don not know the value of either of them, according to [this](http://stackoverflow.com/questions/1843451/why-does-null-null-evaluate-to-false-in-sql-server). 
###C++
Macro NULL is 0. You know what will happen when comparing two integer. 
