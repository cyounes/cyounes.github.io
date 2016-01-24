---
layout: post
title: Termcolor Library
comments: true
description: "C/C++ library used for ANSII Color formatting for Linux/Mac terminal output."
---


TermColor Is a C library used for ANSII Color formatting for Linux/Mac terminal output.


* [Installation](#installation)
* [Termcolor users documentation](#termcolor-users-documentation) &larr; &hearts;
* [Termcolor developers documentation](#termcolor-developers-documentation)

![Termcolor Library]({{ site.ImagesFolder }}/termcolor/example_termcolor.png) 

<h2><a name="installation">Installation:</a></h2>
There are two ways to install <code class="option">termcolor.h</code> library:

<h3> 1. Install into gcc includes folder : </h3>
&rarr; <code>need root permissions</code>
{% highlight bash %}
curl https://raw.github.com/cyounes/termcolor/master/quickinstall.sh | sh 
{% endhighlight %}
include it in your code:
{% highlight c %}
#include <termcolor.h>
{% endhighlight %}
<h3> 2. download termcolor.h in your project folder:  </h3>
get `termcolor.h` file:
{% highlight bash %}
curl -O https://raw.github.com/cyounes/termcolor/master/termcolor.h 
{% endhighlight %}
include it in your code then start use the libray :)
{% highlight bash %}
#include "termcolor.h"
{% endhighlight %}	

<h2><a name="termcolor-users-documentation">Termcolor users documentation: </a></h2>

<code class="flag">cprint()</code> function facilitates the use of the <b>termcolor</b> library, the programer needs to know just some tags to get a good results. So to get a good results you must be <b>OK</b> to use <code class="flag">cprint()</code> instead of <code class="flag">printf()</code> :P

* Example 1: 

{% highlight c %}
cprint("${bd}Hello world!${/bd}\n");
{% endhighlight %}	

In this example, the <code>${bd}</code> tag tells the program to <b>START</b> showing text in bold and the <b>${/bd}</b> tag tells the program to <b>STOP</b> showing text in bold.

* Example 2:

{% highlight c %}
cprint("${ul}Hello world!${/ul}\n");
{% endhighlight %}	

In the second example, the <code class="yel">${ul}</code> tag tells the program to <code>START</code> underlining text and the <code class="yel">${/ul}</code> tag tells the program to <code>STOP</code> underlining the text.

<h3> Easy to use? </h3>
<p>
The principle of using this function is roughly the principle of html tag, every time you open a tag you must close it after inserting a code.
Except it is not quite the same, as you will see in the following examples…
</p>
### Tags:

<h4> Text decoration </h4>
<table> 
<thead>
    <tr>
        <th>Tag Name:</th>
		<th>What it does:</th>
	</tr>
</thead>
<tbody>
<tr><td><p><code class="option">${bd}</code></p></td><td><p>Start Bold</p></td></tr>
<tr><td><p><code class="option">${/bd}</code></p></td><td><p>Stop Bold</p></td></tr>
<tr><td><p><code class="option">${ul}</code></p></td><td><p>Start Underline</p></td></tr>
<tr><td><p><code class="option">{/ul}</code></p></td><td><p>Stop underline</p></td></tr>
<tr><td><p><code class="option">${bl}</code></p></td><td><p>Start blink</p></td></tr>
<tr><td><p><code class="option">${/bl}</code></p></td><td><p>Stop blink</p></td></tr>
</tbody>
</table>
		
<h4> Colors: </h4>
<h5> Effects: </h5>
<table>
<thead><tr><th>Tag name:</th><th>What it does:</th></tr></thead>
<tbody>
<tr><td><p><code class="option">${rv}</code></p></td><td><p>reverse colors</p></td></tr>

<tr><td><p><code class="option">${/rv}</code></p></td><td><p>stop reversing colors</p></td></tr>

<tr><td><p><code class="option">${bi}</code></p></td><td><p>use high intensity for background color</p></td></tr>
<tr><td><p><code class="option">${/bi}</code></p></td><td><p>stop using high intensity for background color</p></td></tr>
<tr><td><p><code class="option">${fi}</code></p></td><td><p>use high intensity for foreground color</p></td></tr>
<tr><td><p><code class="option">${/fi}</code></p></td><td><p>stop using high intensity for foreground color</p></td></tr>
</tbody>
</table>

##### Foreground and Background colors:

###### Background color tags: 
<table>
<thead>
<tr><th>Tag name:</th><th>What it does:</th></tr>
</thead>
<tbody>
<tr><td><p><code class="option">${bb}</code></p></td><td><p>Black background</p></td></tr>
<tr><td><p><code class="option">${rb}</code></p></td><td><p>Red background</p></td></tr>
<tr><td><p><code class="option">${gb}</code></p></td><td><p>Green background</p></td></tr>
<tr><td><p><code class="option">${yb}</code></p></td><td><p>Yellow background</p></td></tr>
<tr><td><p><code class="option">${ub}</code></p></td><td><p>Blue background</p></td></tr>
<tr><td><p><code class="option">${mb}</code></p></td><td><p>Magenta background</p></td></tr>
<tr><td><p><code class="option">${cb}</code></p></td><td><p>Cyan background</p></td></tr>
<tr><td><p><code class="option">${wb}</code></p></td><td><p>White background</p></td></tr>
<tr><td><p><code class="option">${/bg}</code></p></td><td><p>Stop using background</p></td></tr>
</tbody>
</table>

###### Foreground color tags:
<table>
<thead>
<tr><th>Tag name:</th><th>What it does:</th></tr>
</thead>
<tbody>
<tr><td><p><code class="option">${bf}</code></p></td><td><p>Black foreground</p></td></tr>
<tr><td><p><code class="option">${rf}</code></p></td><td><p>Red foreground</p></td></tr>
<tr><td><p><code class="option">${gf}</code></p></td><td><p>Green foreground</p></td></tr>
<tr><td><p><code class="option">${yf}</code></p></td><td><p>Yellow foreground</p></td></tr>
<tr><td><p><code class="option">${uf}</code></p></td><td><p>Blue foreground</p></td></tr>
<tr><td><p><code class="option">${mf}</code></p></td><td><p>Magenta foreground</p></td></tr>
<tr><td><p><code class="option">${cf}</code></p></td><td><p>Cyan foreground</p></td></tr>
<tr><td><p><code class="option">${wf}</code></p></td><td><p>White foreground</p></td></tr>
<tr><td><p><code class="option">${/fg}</code></p></td><td><p>Stop using foreground</p></td></tr>
</tbody>
</table>

### autoResetStyle(): 
This function has one `BOOLEAN` argument, when it take the `TRUE` variable, you need to restart all effects and decoration you did in the previous `cprint()`.
Otherwise, if you forget to close the tags in the previous `cprint()` , the next one continue applying all the effects and decorations that you have forgot to close.

* Example:

* _auto reset_ :
	
{% highlight c %}
autoResetStyle(TRUE);
cprint("${bd}Hello ");
cprint("world\n");
{% endhighlight %}
this will display **Hello** in bold and world in normal weight.

* _don't auto reset_ :
	
{% highlight c %}
autoResetStyle(FALSE);
cprint("${bd}Hello ");
cprint("world\n");
{% endhighlight %}
this will display both **Hello** and **world** in bold
	
### cprint() and variables:

Currently, <code class="yel">cprint()</code> ~~must exactly take one arguments (char *)~~ takes more than one argument, 
however it takes only the `int %d` , `char %c` and strings `char * %s` , it may prints anything wrong
if you give a long or float argument.
in the next versions may be developed to take all the data types possible which is the case of `printf()` .

So to print a variable of another data type using effects,
you must disable `auto reset` by doing : `autoResetStyle(FALSE);`
then put the printf(args) between tow cprint()s.
#### Example: 

{% highlight c %}
long a=10, b=10;
autoResetStyle(FALSE);
cprint("a = ${bd} }
printf("%ld",a);
cprint("${/bd} b= ${bd}");
printf("%ld, b);
cprint("${/bd}\n");
{% endhighlight %}

<h2><a name="termcolor-developers-documentation">Termcolor developers documentation:</a></h2>
### Available Colors:
 `BLACK` `RED` `GREEN` `YELLOW` `BLUE` `MAGENTA` `CYAN` `WHITE`


### BOOLEAN ?
By including **termcolor** library in your code, you don't need to include the ~~**stdbool**~~ library. However you need to write the boolean keywords in uppercase characters:  ***TRUE***  and ***FALSE*** 

### Functions:

#### Colors: 

+ `bgColor(COLOR)` : set the background color using the available colors.

+ `fgColor(COLOR)` : set the foreground color using the available colors.

for `bgColor(COLOR)` and `fgColor(COLOR)` functions use the variable `DEFAULT`as parameter to reset the default color:
{% highlight c %}
bgColor(DEFAULT);
fgColor(DEFAULT);
{% endhighlight %}
#### Text decorations:

+ `textBold(BOOLEAN)` : enable or disable text bolding for the next output:
{% highlight c %} 
textBold(TRUE); 
textBold(FALSE);
{% endhighlight %}

+ `textBlink(BOOLEAN)` : enable or disable text blinking for the next output:
{% highlight c %} 
textBlink(TRUE); 
textBlink(FALSE);
{% endhighlight %}

+ `colorReverse(BOOLEAN)`: enable or disable colors reversing for the next output:

{% highlight c %} 
colorReverse(TRUE); 
colorReverse(FALSE);
{% endhighlight %}

+ `textUnderline(BOOLEAN)`: underline text

+ `highFgIntensity(BOOLEAN)` : Use High Intensity for foreground colors.

+ `highBgIntensity(BOOLEAN)` : Use High Intensity for background colors.

+ `setStyle()` : Usually the programer don't need to invoke this function, it will be invoked automatically by the other functions each time you change the style.

+ `resetStyle()` : Reset all colors and decorations by default!, i suggest to invoke this function at the end of your main to restore all as default.

### Examples:
##### Red Background:

{% highlight c %}
bgColor(RED);
printf("text with RED Background");
{% endhighlight %}
######Result:
![termcolor red background](https://raw.github.com/cyounes/termcolor/master/examples/red_background.png) 
-
##### Default background + Red foreground:

{% highlight c %}
bgColor(DEFAULT);
fgColor(RED);
printf("text with RED Foreground");
{% endhighlight %}
######Result:
![termcolor red foreground](https://raw.github.com/cyounes/termcolor/master/examples/red_foreground.png)
-
##### Yellow text on red background:

{% highlight c %}
bgColor(RED);
fgColor(YELLOW);
printf("YELLOW text in RED Background");
{% endhighlight %}
######Result:
![Yellow text on red background](https://raw.github.com/cyounes/termcolor/master/examples/yellow_in_red.png)
-
##### Yellow Bold text on red background:

{% highlight c %}
bgColor(RED);
fgColor(YELLOW);
textBold(TRUE);
printf("YELLOW and BOLD text in RED Background");
{% endhighlight %}
######Result:
![termcolor Yellow Bold text on red background](https://raw.github.com/cyounes/termcolor/master/examples/bold_yellow_in_red.png)
-
##### Yellow, Bold and underlined text on red background:

{% highlight c %}
bgColor(RED);
fgColor(YELLOW);
textBold(TRUE);
textUnderline(TRUE);
printf("YELLOW and BOLD text in RED Background");
{% endhighlight %}
######Result:
![termcolor Yellow, Bold and underlined text on red background](https://raw.github.com/cyounes/termcolor/master/examples/bold_yellow_underline.png)
-

##### High Intensity: Yellow Bold text on red background:

{% highlight c %}
bgColor(RED);
fgColor(YELLOW);
textBold(TRUE);
highFgIntensity(TRUE);
highBgIntensity(TRUE);
printf("YELLOW and BOLD text in RED Background");
{% endhighlight %}
######Result:
![termcolor High Intensity: Yellow Bold text on red background](https://raw.github.com/cyounes/termcolor/master/examples/high_intens.png)
-

##### Reversed colors:

{% highlight c %}
bgColor(DEFAULT);
fgColor(DEFAULT);
textBold(TRUE);
textUnderline(TRUE);
printf("REVERSED test with default foreground and default background :)");
{% endhighlight %}
######Result:
![termcolor Reversed colors](https://raw.github.com/cyounes/termcolor/master/examples/reversed_colors.png)
-

##### Main Example:

{% highlight c %}
#include <stdio.h>
#include "termcolor.h"

int main() {

	printf("Hi, Thanks for trying termcolor library :) \n" );
	printf("Using this library allow the developer to decorate \
the output of its console application.\n\n");
	printf("Some Examples: \n\n");
	
	bgColor(RED); // Background RED and not "RED" !
	printf("text with RED Background\n\n");
	bgColor(DEFAULT); // Default Background Color
	fgColor(RED); // RED Foreground color 
	printf("text with RED Foreground\n\n");
	bgColor(RED);
	fgColor(YELLOW);
	printf("YELLOW text in RED Background\n\n");
	textBold(TRUE); // Bold Text
	printf("YELLOW and BOLD text in RED Background\n\n");
	textUnderline(TRUE); // Underlined text 
	bgColor(DEFAULT);
	printf("YELLOW and BOLD and Underlined text\n\n");
	fgColor(DEFAULT);
	colorReverse(TRUE);
	printf("REVERSED test with default foreground and default background :)\n\n");
	colorReverse(FALSE);
	textBlink(TRUE);
	printf("BLINKING text with default foreground and default background\n\n");
	
	resetStyle(); // Reset all as default 
	printf("Now Examples using High Intensity\n\n");
	highFgIntensity(TRUE);
	highBgIntensity(TRUE);
	bgColor(RED);
	printf("text with RED Background\n\n");
	bgColor(DEFAULT);
	fgColor(RED);
	printf("text with RED Foreground\n\n");
	bgColor(RED);
	fgColor(YELLOW);
	printf("YELLOW text in RED Background\n\n");
	textBold(TRUE);
	printf("YELLOW and BOLD text in RED Background\n\n");
	
	resetStyle();
	printf("Simple Text :D \n\n");
	
    return 0;
}

{% endhighlight %}
######Result:
![termcolor Reversed colors](https://raw.github.com/cyounes/termcolor/master/examples/example_termcolor.png)
-

## TODO:
* insert horizontal line with specified color.
* Text align : [Left ; Center ; Right ].
* Text Border.
* add availability to `cprint()` to take more than one argument.

### Fork me on GitHub:

I'll be very happy to take pull requests from others, Go ahead and fork me.


[1]: http://github.com/cyounes/        "c.Younes on github"
[2]: http://twitter/cyounes  "@cyounes"
[3]: http://cyounes.com/    "personal website"