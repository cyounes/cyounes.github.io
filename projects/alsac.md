---
layout: projects
title: alsac
prev_section: boxman-puzzle
next_section: 
permalink: /projects/alsac/
project: alsac
comments: true
description: "Simple command line tool to control alsa devices sound on linux."
---


![alsac](https://raw.github.com/cyounes/alsac/master/alsac.png) 
Simple command line tool to control sound on linux for alsa devices

## Installation:

```
curl https://raw.github.com/cyounes/alsac/master/quickinstall.sh | sh 
```

## Usage: 
```
$ alsac [-|+] [value]
```
```
$ alsac [value] 
```
```
$ alsac [mute | unmute]
```

## Examples:
Examples: 

+ `alsac - 10`  : decrease sound of 10% 

+ `alsac + 18 ` : increase sound of 18% 

+ `alsac 45`    : set sound to 45% 

+ `alsac mute`  : mute sound 

+ `alsac unmute`: unmute sound

## License: 
See [license.txt](https://raw.github.com/cyounes/alsac/master/license.txt)

<a rel="license"
href="http://creativecommons.org/licenses/by-nc-sa/3.0/fr/deed.us"><img
alt="Creative Commons License" style="border-width:0"
src="http://i.creativecommons.org/l/by-nc-sa/3.0/fr/88x31.png" /></a>
