# Blocking Queue

The Java BlockingQueue interface, java.util.concurrent.BlockingQueue, represents a queue which is thread safe to put elements into, and take elements out of from. In other words, multiple threads can be inserting and taking elements concurrently from a Java BlockingQueue, without any concurrency issues arising.

The term blocking queue comes from the fact that the Java BlockingQueue is capable of blocking the threads that try to insert or take elements from the queue. For instance, if a thread tries to take an element and there are none left in the queue, the thread can be blocked until there is an element to take.



**size()**
The BlockingQueue size() method returns the number of elements stored in BlockingQueue.

**remainingCapacity()**
The BlockingQueue remainingCapacity() method returns the remaining (unused) capacity of the BlockingQueue. The remaining capacity is calculated as full capacity minus the number of elements stored in the BlockingQueue.

**put()**
The BlockingQueue put() method inserts the element into the BlockingQueue if it has space for it internally. If the BlockingQueue does not have space for the new element, the put() method will block the thread calling the put() method until the BlockingQueue as space internally for the new element.

**take()**
The Java BlockingQueue take() method will remove the first element in the BlockingQueue. If the BlockingQueue does not contain any elements, the take() method will block the thread calling take() until an element is inserted into the BlockingQueue.


A BlockingQueue is typically used to have one thread produce objects, which another thread consumes.



# References :
https://www.youtube.com/watch?v=d3xb1Nj88pw&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4&index=17
