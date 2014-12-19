ThreadLooperSample
==================

This is intended to serve as an example on how to use Threads along with the pipeline pattern. 

So what can you do with Loopers and Handlers? Basically, they implement a common concurrency pattern that I call the Pipeline Thread. Here’s how it works:

The Pipeline Thread holds a queue of tasks which are just some units of work that can be executed or processed.
Other threads can safely push new tasks into the Pipeline Thread’s queue at any time.
The Pipeline Thread processes the queued tasks one after another. If there are no tasks queued, it blocks until a task appears in the queue.
Sometimes tasks can called messages and other names.
This architecture has some valuable traits and is widely used in frameworks and applications on different platforms.

In this post, we are going to build a simple app that emulates a queue of background downloads while showing its status in the UI. It will be based on a Pipeline Thread that we will build using Looper and Handler. As usual, the complete source is available at the bottom of the article.


But before we start, let’s discuss the Pipeline Thread for some more time and see how Looper and Handler implement it.

Usages of the Pipeline Thread

The most prominent usage of Pipeline Thread is found within almost any UI framework, including Swing (remember the event-dispatching thread?), SWT, Adobe Flex and, of course, Android Activities. The Pipeline Thread pattern is used to process UI events (such as button clicks, mouse movement, orientation changes, screen redraw and so on). This allows you to change a button caption without having to worry that the user will click the button at the same moment.

On the other hand, this forces you to only do quick operations in the UI thread – any developer knows what happens if you try to download a file right there in a button onClick handler. In our app we will overcome that by adding another Pipeline Thread and pushing long-lasting operations (in our case, the downloads) to it so that the UI thread can run free.

Other common usages of the Pipeline Thread pattern:

Executing requests to a remote service (usually you want to do them one by one and sequentially)
Uploading images to an HTTP service
Resizing and processing images (I once developed a picture uploader :) )
Downloading stuff, just like we’re going to do in this app.


For more information: 
http://mindtherobot.com/blog/159/android-guts-intro-to-loopers-and-handlers/ 
http://developer.android.com/reference/android/os/Looper.html
