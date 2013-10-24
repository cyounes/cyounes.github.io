---
layout: news_item
title: "alsac Command Line Sound Controller"
date: "2012-12-03 00:00:00"
description: Linux tool to control sound using command line
categories: [Linux]
version: 1.0.0
author: Younes Cheikh
comments: true
---


When i've installed ubuntu with openbox window manager, there were no task bars and no menus. that was a problem for me to control the sound using command line.

![alsac](/img/content/alsac.png) To solve this i wrote some lines quickly to create a simple and easy command line tool allows me to control sound volume.

`alsac` works only with **alsa** devices and tested only on Ubuntu 12.10, based on
`alsa` command and its parmeters.

## Installation:

{% highlight bash %}
curl https://raw.github.com/cyounes/alsac/master/quickinstall.sh | sh 
{% endhighlight %}

## Usage: 
{% highlight bash %}
$ alsac [-|+] [value]
{% endhighlight %}

{% highlight bash %}
$ alsac [value] 
{% endhighlight %}

{% highlight bash %}
$ alsac [mute | unmute]
{% endhighlight %}

## Examples:

Examples: 

+ `alsac - 10`  : decrease sound of 10% 

+ `alsac + 18 ` : increase sound of 18% 

+ `alsac 45`    : set sound to 45% 

+ `alsac mute`  : mute sound 

+ `alsac unmute`: unmute sound

## Github page:
https://github.com/cyounes/alsac

