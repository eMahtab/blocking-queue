# Blocking Queue

The Java BlockingQueue interface, java.util.concurrent.BlockingQueue, represents a queue which is **thread safe** to put elements into, and take elements out of from. In other words, multiple threads can be inserting and taking elements concurrently from a Java BlockingQueue, without any concurrency issues arising.

**What is meant by thread safe :**

`ArrayBlockingQueue` uses internal locks to control access to the queue's elements. When one thread is accessing or modifying the queue (e.g., by calling take() to remove an element), other threads attempting to access the queue must wait until the current operation is completed and the lock is released.

**The term blocking queue comes from the fact that the Java BlockingQueue is capable of blocking the threads that try to insert or take elements from the queue. For instance, if a thread tries to take an element and there are none left in the queue, the thread can be blocked until there is an element to take.**

**size()**
The BlockingQueue size() method returns the number of elements stored in BlockingQueue.

**remainingCapacity()**
The BlockingQueue remainingCapacity() method returns the remaining (unused) capacity of the BlockingQueue. The remaining capacity is calculated as full capacity minus the number of elements stored in the BlockingQueue.

**put()**
The BlockingQueue put() method inserts the element into the BlockingQueue if it has space for it internally. If the BlockingQueue does not have space for the new element, the put() method will block the thread calling the put() method until the BlockingQueue as space internally for the new element.

**take()**
The Java BlockingQueue take() method will remove the first element in the BlockingQueue. If the BlockingQueue does not contain any elements, the take() method will block the thread calling take() until an element is inserted into the BlockingQueue.


A BlockingQueue is typically used to have one thread produce objects, which another thread consumes.

![Blocking Queue](blocking-queue.png?raw=true)

The producing thread will keep producing new objects and insert them into the BlockingQueue, until the queue reaches some upper bound on what it can contain. It's limit, in other words. If the blocking queue reaches its upper limit, the producing thread is blocked while trying to insert the new object. It remains blocked until a consuming thread takes an object out of the queue.

The consuming thread keeps taking objects out of the BlockingQueue to processes them. If the consuming thread tries to take an object out of an empty queue, the consuming thread is blocked until a producing thread puts an object into the queue.

```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

class Producer implements Runnable {
    BlockingQueue<String> blockingQueue = null;
    public Producer(BlockingQueue<String> queue) {
        this.blockingQueue = queue;
    }

    @Override
    public void run() {
        while (true) {
            long timeMillis = System.currentTimeMillis();
            try {
                this.blockingQueue.put("" + timeMillis);
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println("Producer was interrupted");
            }
        }
    }
}

class Consumer implements Runnable {
    BlockingQueue<String> blockingQueue = null;
    public Consumer(BlockingQueue<String> queue) {
        this.blockingQueue = queue;
    }

    @Override
    public void run() {
        while(true){
            try {
                String element = this.blockingQueue.take();
                String text = Thread.currentThread().getName() +
                        " consumed " + element;
                System.out.println(text);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BlockingQueue<String> blockingQueue = new ArrayBlockingQueue<>(3);

        Producer producer = new Producer(blockingQueue);
        Consumer consumer1 = new Consumer(blockingQueue);
        Consumer consumer2 = new Consumer(blockingQueue);

        Thread producerThread = new Thread(producer);
        Thread consumerThread1 = new Thread(consumer1);
        Thread consumerThread2 = new Thread(consumer2);
        producerThread.start();
        consumerThread1.start();
        consumerThread2.start();
    }
}
```

### Execution Output :
```
Thread-1 consumed 1730482058227
Thread-2 consumed 1730482059228
Thread-1 consumed 1730482060228
Thread-2 consumed 1730482061228
Thread-1 consumed 1730482062228
Thread-2 consumed 1730482063228
Thread-1 consumed 1730482064229
Thread-2 consumed 1730482065229
Thread-1 consumed 1730482066229
Thread-2 consumed 1730482067229
Thread-1 consumed 1730482068229
Thread-2 consumed 1730482069229
Thread-1 consumed 1730482070230
Thread-2 consumed 1730482071230
Thread-1 consumed 1730482072230
Thread-2 consumed 1730482073231
Thread-1 consumed 1730482074231
Thread-2 consumed 1730482075231
Thread-1 consumed 1730482076232
Thread-2 consumed 1730482077233
Thread-1 consumed 1730482078233
Thread-2 consumed 1730482079233
Thread-1 consumed 1730482080233
Thread-2 consumed 1730482081233
Thread-1 consumed 1730482082233
Thread-2 consumed 1730482083233
Thread-1 consumed 1730482084234
Thread-2 consumed 1730482085234
........
```

# References :
1. https://www.youtube.com/watch?v=d3xb1Nj88pw&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4&index=17

2. http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html

3. https://github.com/eMahtab/producer-consumer-pattern
