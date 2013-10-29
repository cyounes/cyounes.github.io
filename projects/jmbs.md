---
layout: projects
title: jMBS 
next_section: walletix-java-api
prev_section: tisseo-api.net
permalink: /projects/jmbs/
project: jmbs
comments: true
description: "Java Micro Blogging System, free and open source software, Currently allows to create a mini platform for a local social network."
---

Java Micro Blogging System
		
**`jMBS`** is free and open source software, Currently allows to create a mini platform for a local social network.  
##### How it works?
Users can register using the Client GUI, each user can writes messages, and follows other users, participate to one or more projects.  


![jMBS](../../img/projects/jmbs/jmbs_login_client.png)

## Get Code Source:
You can get a copy of the repository using the public git
{% highlight bash %}
$ git clone git://github.com/cyounes/jmbs.git
{% endhighlight %}

## Compile jMBS

First, you need to create a new **PostgreSQL** database, use the latest version of SQL script included in the `Server/SQL/` directory.

Next you need to configure jMBS to connect to Database. to do this you could edit the `db.connect` file.

###Compile Server:

1. You need to compile the RMI project innorder to compile the server project.
{% highlight bash %}
$ cd /PATH/TO/JMBS/DIRECTORY/RMI/
$ mvn clean compile install
{% endhighlight %}

2. Compile the server maven project
{% highlight bash %}
$ cd /PATH/TO/JMBS/DIRECTORY/Server/
$ mvn clean assembly:assembly
{% endhighlight %}


###Compile Client:
{% highlight bash %}
$ cd /PATH/TO/JMBS/DIRECTORY/Client/
$ mvn clean assembly:assembly -Dmaven.test.skip=true
{% endhighlight %}	

## Start jMBS

### Server:
![jMBS Start Server](../../img/projects/jmbs/jmbs_start_server.png)
{% highlight bash %}
$ java -jar \
-Djava.rmi.server.codebase=file:../RMI/target/RMI-0.0.1-SNAPSHOT.jar \
target/Server-jar-with-dependencies.jar
{% endhighlight %}

### Client:
![jMBS Start Client](../../img/projects/jmbs/jmbs_loading_client.png)

{% highlight bash %}
$ java -jar -Djava.rmi.server.codebase=file:../RMI/target/RMI-0.0.1-SNAPSHOT.jar -Djava.security.policy=target/classes/security.policy target/Client-jar-with-dependencies.jar
{% endhighlight %}


## Contributors:
+ [Younes Cheikh](http://cyounes.com)
+ [Benjamin Babic](https://github.com/Ornro)  

## TODO:
- add some lines to this file to explain how to use jMBS
- add JavaDoc link

