---
layout: post
title: Basicmenu Library
comments: true
description: An open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs.
categories: [Development]
tags: [Library, C]
fullview: true
---


[Basicmenu](http://cyounes.com/projects/basicmenu) is a an open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs.


<h4> Screenshoot example: </h4>
![BasicMenu Library]({{ site.ImagesFolder }}/basicmenu.png)


<h4>Installation: </h4>
<p>
There is no installation required, you need just to download the basicmenu.h file, include it in your code then start use the libray :)
</p>
{% highlight c %}
#include "basicmenu.h"
{% endhighlight %}

<h4>Essential functions:</h4>
<p>
To use this library , you have just to learn about some basic functions
</p>
<h5>1. Start the basic menu library :</h5>
<p>
First you need to tell the program that uses the library 
to do this, invoke <code>startBasicMenu()</code> function in the beginning of the main.
</p>
 
<h5> 2. Create and initialize a new menu:</h5>
<p>
To create a new menu you need to declare it with its type:</p> 
{% highlight c %}
custom_Menu* mymenu; 
{% endhighlight %}
<p>To initialize it with the <code>init_new_menu()</code> function:</p> 
{% highlight c %}
init_new_menu (&mymenu);
{% endhighlight %}

<h5>3. Add a new item to the menu:</h5>
<p>
Any menu, needs to have at least tow items, to add a new item to the menu use the <code>addNewItem()</code> function:</p> 
{% highlight c %}
addNewItem (&mymenu , "Choice number one!");
addNewItem (&mymenu , "Choice number tow!");
{% endhighlight %}
<p>You can add unlimited number of items, but be careful to don't exceed the console size :)</p> 
<code> see the TODO list.</code>

<h5> 4. Put and display a menu into the program:</h5>
<p>
To display the menu you need to invoke the <code>put_menu()</code> function.
example: <a href="/Content/Docs/basicmenu/example1_8c-example.html">Link</a>
</p>
<h4> TODO:</h4>
<ul>
<li>
Allow the programmer to add unlimited items to the menu.
</li>
<li>
Add a scroll menu option.
</li>
<li>
Add the maximum of items to shown on the menu.
</li>
</ul>

for more functions and examples please visit <a href="/Content/Docs/basicmenu/examples.html">the documentation</a>


<div class="note info">
	<h5>Are you a developer? Fork me on GitHub</h5>
	<p>I'll be very happy to take pull requests from others, Go ahead and fork me.</p>
</div>


### Documentation: 

for code documentation please visit  <a href="/Content/Docs/basicmenu/examples.html" >Documentation page</a>
