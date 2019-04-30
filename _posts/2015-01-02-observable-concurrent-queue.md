---
layout: post
title: 'Observable Concurrent Queue'
date: '2015-01-02 00:00:00'
comments: true
description: ObservableConcurrentQueue based on the classic .Net ConcurrentQueue (System.Collections.Concurrent.ConcurrentQueue) Allows to raise events when the queue content is changed with the same events as ObservableCollection...
categories: [Development]
tags: [Library, C#]
fullview: true
---

![ConcurrentQueue]({{ site.ImagesFolder }}/concurrentQueue.png)

I was working with the classic ConcurrentQueue in .Net, It's a good practice to schedule tasks execution asynchronously, 
however, getting notified when my ConcurrentQueue 
content is changed was the problem! How can i know if an element has been enqueued, peeked or dequeued? Also how can i be notified when the queue is empty after last element has been dequeued?

To solve the problem of notification, i've developed my custom ConcurrentQueue named ObservableConcurrentQueue inherit from System.Collections.Concurrent.ConcurrentQueue to raise events once the content is changed.

> If you are not familiar with the ConcurrentQueue, [Please read more about it on MSDN](http://msdn.microsoft.com/en-us/library/dd267265)

### Syntax & Example: 

{% highlight csharp %}
var observableConcurrentQueue = new ObservableConcurrentQueue<int>();
observableConcurrentQueue.ContentChanged += OnObservableConcurrentQueueContentChanged;
{% endhighlight %}

The handleMethod ContentChanged event looks as the follwoing:

{% highlight csharp %}

private static void OnObservableConcurrentQueueContentChanged(
            object sender, 
            NotifyConcurrentQueueChangedEventArgs<int> args)
        {
            if (args.Action == NotifyConcurrentQueueChangedAction.Enqueue)
            {
                Console.BackgroundColor = ConsoleColor.DarkGreen;
                Console.WriteLine("New Item added: {0}", args.ChangedItem);
            }

            if (args.Action == NotifyConcurrentQueueChangedAction.Dequeue)
            {
                Console.BackgroundColor = ConsoleColor.Red;
                Console.WriteLine("New Item deleted: {0}", args.ChangedItem);
            }

            if (args.Action == NotifyConcurrentQueueChangedAction.Peek)
            {
                Console.BackgroundColor = ConsoleColor.DarkBlue;
                Console.WriteLine("Item peeked: {0}", args.ChangedItem);
            }

            if (args.Action == NotifyConcurrentQueueChangedAction.Empty)
            {
                Console.BackgroundColor = ConsoleColor.White;
                Console.ForegroundColor = ConsoleColor.Blue;
                Console.WriteLine("Queue is empty");
            }

            Console.ResetColor();
        }

{% endhighlight %}

Then, Once the handler is defined, we can start adding, deleting or getting elements from the concurrentQueue, and after each operation an event will be raised and handled by the method above.

#### Event Args:

The EventArgs object sent by the event contains 2 properties:

#### NotifyConcurrentQueueChangedAction 

+ **Enqueue**: If a new item has been enqueued.
+ **Dequeue**: an item has been dequeued.
+ **Peek**: an item has been peeked.
+ **Empty**: The last element in the queue has been dequeued and the queue is empty.

#### T ChangedItem
The item which the changes applied on. can be null if the notification action is NotifyConcurrentQueueChangedAction.Empty.

### Download
+ Source: [Github Ripository][1]
+ Binary: [Nuget](https://www.nuget.org/packages/ObservableConcurrentQueue/) :

{% highlight bash %}

PM> Install-Package ObservableConcurrentQueue

{% endhighlight %} 
 
 [1]: https://github.com/BledSoft/ObservableConcurrentQueue





