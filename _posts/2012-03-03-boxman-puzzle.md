---
layout: post
title: Boxman Puzzle
comments: true
description: Transport puzzle developed in Ocaml by Younes Cheikh, in witch the player pushed boxes around a maze, viewed from above, and tries to put them in designated location.
categories: [Development]
tags: [Game, Puzzle, Caml]
fullview: true
---

![Boxman Puzzle]({{ site.ImagesFolder }}/boxman/boxman1.png) 

Boxman (Also called Sokoban Pushbox) is a transport puzzle in witch the player pushed boxes around a maze, viewed from above, and tries to put them in designated location. Only one box may be pushed at a time, and boxes cannot be pulled.

![Boxman Puzzle]({{ site.ImagesFolder }}/boxman/boxman2.png)
![Boxman Puzzle]({{ site.ImagesFolder }}/boxman/boxman2.png)

To compile the source code you need to download <code>[CamlLight][1]</code> from [inria.fr][2] website.
Include the boxman.ml file, 
```file > include > browse_to_file_path``` The game will be executed automatically , if you want to execute it manually type in the caml interpeter:
{% highlight ocaml %}
jeu();; 
{% endhighlight %}
than press enter.

![Boxman Puzzle]({{ site.ImagesFolder }}/boxman/boxman4.png)
![Boxman Puzzle]({{ site.ImagesFolder }}/boxman/boxman5.png)

[1]: http://caml.inria.fr/pub/distrib/caml-light-0.74//cl74win.exe "camllight"
[2]: http://caml.inria.fr "Inria"
