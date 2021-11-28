# Blocking Queue

The Java BlockingQueue interface, java.util.concurrent.BlockingQueue, represents a queue which is thread safe to put elements into, and take elements out of from. In other words, multiple threads can be inserting and taking elements concurrently from a Java BlockingQueue, without any concurrency issues arising.

The term blocking queue comes from the fact that the Java BlockingQueue is capable of blocking the threads that try to insert or take elements from the queue. For instance, if a thread tries to take an element and there are none left in the queue, the thread can be blocked until there is an element to take.





# References :
https://www.youtube.com/watch?v=d3xb1Nj88pw&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4&index=17
