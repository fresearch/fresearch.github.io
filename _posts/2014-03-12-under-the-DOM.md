---
layout: post-no-feature
title: Under The DOM
description: "A gentle primer into the not-so-murky waters of JavaScript BY Dennis Kigen"
categories: articles
date: 2014-04-04
tags: [firstpost, programming, javascript]
---

The DOM or Document Object Model is basically a model of how the various HTML elements in a page (paragraphs, images and so on) are related to each other and to the topmost structure: the document itself. To make better sense of this concept, visualize your HTML page as being the 'document'. This document is made up of several 'objects' (HTML elements, text and attributes) and these come together in a particular order, referred to as the 'model'. 

The DOM is made up of items called nodes. Nodes representing HTML elements are referred to as *element nodes*. Those representing text are called *text nodes* whereas *attribute nodes* represent attributes.

**Working with the Element Node**

There are several ways of accessing elements in the element node.

* Targeting elements by ID

Since an element's ID is unique to a document, this method represents the most efficient method of access. It is also the fastest approach in terms of performance.

Consider the code snippet below.

{% highlight html %}
<section id="top">
	<p id="introtext">Accessing element by ID</p>	
</section>
{% endhighlight %}

The JavaScript code required to access the elements referenced by the two IDs above is:

{% highlight js %}
document.getElementById("top");
document.getElementById("introtext");
{% endhighlight %}

* Targeting elements by Tag Name

The previous approach, <code>getElementById</code>, would only return a single element at a time as IDs are unique to each document. Targeting elements by tag name will return a nodelist (a collection of nodes that maintain their source order) of all the elements that correspond to that particular tag name.

Example HTML code:

{% highlight html %}
<div>
	<p>This is a paragraph</p>
	<p>This is another paragraph</p>
	<p>This is yet another paragraph</p>
</div>
{% endhighlight %}

JavaScript code for accessing elements by tag name: 

{% highlight js %}
document.getElementsByTagName("p");
{% endhighlight %}

This code will return a nodelist of all the paragraphs in the document.

Since the nodelist is an object, several JavaScript methods can be used on it.
{% highlight js %}
document.getElementsByTagName("p").length; //returns 3 i.e. the number of paragraphs
document.getElementsByTagName("p").item[0]; //returns the first paragraph (item method)
document.getElementsByTagName("p")[0]; //returns the first paragraph (array syntax)
{% endhighlight %}

> Notice that the word 'elements' is pluralized. 

* Targeting elements by Class 

Example HTML code:

{% highlight html %}
<!doctype html>
<html>
   <head>
	<meta charset="utf-8 ">
	<title>Targeting elements by Class</title>	
   </head>
   <body>
	 <h1>Using getElementsByClassName</h1>
	 <p class="loud intro">This is a paragraph</p>
	 <p class="loud" id="self">This is <span class="intro">another paragraph</span></p>
     <p class="loud">This is yet another paragraph</p>
   </body>
</html>
{% endhighlight %}

JavaScript code for accessing elements by Class:
{% highlight js %}
document.getElementsByClassName("loud"); //returns all elements that have the class "loud" 
document.getElementsByClassName("loud intro"); //returns all elements that have the class "loud intro"
document.getElementById("self").document.getElementsByClassName("intro"); /* returns all elements that have the class "intro" contained in the elements with the ID "self". */
{% endhighlight %}

> With this being a relatively recent JavaScript feature, browser support for it may not be 100% across the board. Use of a JavaScript library or framework should help smooth out any support quirks on older browsers.

* Targeting elements using CSS Selectors

Involves the use of CSS selectors to target elements in JavaScript. Two methods are used here: <code>querySelector()</code> and <code>querySelectorAll()</code>. 

The difference between these is that <code>querySelectorAll()</code> returns a nodelist of all the elements pertaining to a particular selector whereas <code>querySelector()</code> returns only the first element pertaining to that selector. 

Example HTML code:

{% highlight html %}
	<body>
	<div id="header">
		<h1>Using querySelector</h1>
	</div>
		<p class="dropcap huge">Content paragraph</p>
		<p class="dropcap">Content <span class="huge">paragraph</span></p>
		<p class="dropcap">Content paragraph</p>
	</body>
{% endhighlight %}	

JavaScript code for accessing elements using CSS selectors:

{% highlight js %}
document.querySelector("#header"); //returns the header ID element; div in this case.
document.querySelectorAll(".dropcap"); //returns a nodelist of all the elements of the class "dropcap".
document.querySelector(".dropcap, .huge"); //returns all the elements of class "dropcap" OR class "huge".
document.querySelectorAll(p[class]); //returns a nodelist of all the paragraphs that have a class
{% endhighlight %}

> As with accessing elements by class, this approach also errs on the risky side as regards browser support. As before, use of a JavaScript library/framework is encouraged to avert any support quirks on older browsers.

**Working with the Attribute Node**

Four methods are used when accessing the attribute node:

* getAttribute()
* setAttribute()
* removeAttribute()
* hasAttribute()

Snippet of code showing example usage of the <code>getAttribute()</code>.
{% highlight html %} 
<p id="lead" class="show">  
{% endhighlight %}

{% highlight js %}
if document.getElementById("lead").hasAttribute("class")); //check whether the attribute exists
  document.getElementById("lead").getAttribute("class")); 
{% endhighlight %}

Adding a class to the paragraph using <code>setAttribute()</code>.
{% highlight js %}
document.getElementById("lead").setAttribute("title", "Set this picture as my avatar");
{% endhighlight %}

>This adds a class of "title" to the paragraph.

**Working with the Text Node**

Working with the text node basically entails changing content.

Example code snippet:
{% highlight html %}
<div id="header-text">
  <p>I'm a paragraph</p>
</div>
{% endhighlight %} 

JavaScript code for accessing the text node and changing it's content using <code>innerHTML</code>.
{% highlight js %}
document.getElementById("header-text").innerHTML = "<p>I'm a new paragraph</p>"; 
{% endhighlight %} 

>This code changes the content of the paragraph to the new string. 

