# A top-level event-loop in Gambit-in-JavaScript

This is code that can be run in the Gambit Scheme REPL at [try.gambitscheme.org](https://try.gambitscheme.org).
Its purpose is to implement a
[First Come First Served (FCFS)](https://www.geeksforgeeks.org/difference-between-first-come-first-served-fcfs-and-round-robin-rr-scheduling-algorithm/)
scheduling algorithm to handle a global queue of JavaScript events.

One Gambit thread puts 'keydown' events into the queue.
Another Gambit thread puts 'mousemove' events into the queue.
Each of these threads are [blocked](https://www.math.purdue.edu/~lucier/615-2016/gambit.html#Thread-objects)
until it is made runnable by its corresponding event, 'keydown' or 'mousemove'.
After enqueing its corresponding event, the thread is again blocked.
Each subsequent 'keydown' or 'mousemove' event is handled the same way.

The queue can accomodate multiple 'keydown' and 'mousemove' events.
A top-level loop dequeues events and prints them to the web browser's JavaScript console.
After dequeuing some events, the loop is blocked.
A global Gambit constant holds the number of events the loop dequeus before being blocked.
After blocking, the loop is made runnable again by a JavaScript interval timer.
