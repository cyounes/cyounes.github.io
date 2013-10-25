---
layout: projects
title: Basicmenu Library
prev_section: termcolor
next_section: cryptarithms-solver
permalink: /projects/basicmenu/
project: basicmenu
comments: true
description: "An open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs."
---


[Basicmenu](http://cyounes.com/projects/basicmenu) is a an open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs.


<h4> Screenshoot example: </h4>
![BasicMenu Library](../../img/projects/basicmenu/1.png)


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
example: <a href="doc/example1_8c-example.html">Link</a>
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

<h4> Useful functions:</h4>

<ul>
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#af25248c9cb3d0736be1409117da84682" />
		item_border_ON()
		</a>
	</li>
	
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#a1c21c2b1ab331a2c67ef05a9284218da" />
		item_border_OFF()
		</a>
	</li>
	
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#a704a37ae8f690f7a54186ee146309cb6" />
		menu_border_ON()
		</a>
	</li>
	
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#a0d9a10f8ced566cb797395039f35fb9d" />
		menu_border_OFF()
		</a>
	</li>
	
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#ad089e1df4782b887c8eefe307bd42fd4" />
		BG_COLOR_ON()
		</a>
	</li>
	
	<li>
		<a target="_blank" href="doc/basicmenu_8h.html#a538de9d0a829e45b7fe3d7930bc81a03" />
		BG_COLOR_OFF()
		</a>
	</li>
</ul>


for more functions and examples please visit <a href="doc/examples.html">the documentation</a>


<div class="note info">
	<h5>Are you a developer? Fork me on GitHub</h5>
	<p>I'll be very happy to take pull requests from others, Go ahead and fork me.</p>
</div>


### Documentation: 

for code documentation please visit  <http://cyounes.com/basicmenu/doc/index.html>

<a href="https://github.com/you"><img style="position: absolute; top: 0; left: 0; border: 0;" src="https://s3.amazonaws.com/github/ribbons/forkme_left_white_ffffff.png" alt="Fork me on GitHub"></a>