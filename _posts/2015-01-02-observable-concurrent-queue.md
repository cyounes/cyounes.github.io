---
layout: post
title: 'Observable Concurrent Queue'
date: '2015-01-02 00:00:00'
comments: true
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

### Event Args:

The EventArgs object sent by the event contains 2 properties:

### NotifyConcurrentQueueChangedAction 

+ **Enqueue**: If a new item has been enqueued.
+ **Dequeue**: an item has been dequeued.
+ **Peek**: an item has been peeked.
+ **Empty**: The last element in the queue has been dequeued and the queue is empty.

### T ChangedItem
The item which the changes applied on. can be null if the notification action is NotifyConcurrentQueueChangedAction.Empty.

## Download
+ Source: [Github Ripository][1]
+ Binary: [Nuget](https://www.nuget.org/packages/ObservableConcurrentQueue/) :

{% highlight bash %}

PM> Install-Package ObservableConcurrentQueue

{% endhighlight %} 

<a href="https://github.com/cyounes/ObservableConcurrentQueue"><img style="position: fixed; top: 0; right: 0; border: 0; z-index: 999; display: block;" src="https://camo.githubusercontent.com/652c5b9acfaddf3a9c326fa6bde407b87f7be0f4/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f6f72616e67655f6666373630302e706e67" alt="Fork me on GitHub"></a>
 
 [1]: https://github.com/BledSoft/ObservableConcurrentQueue





