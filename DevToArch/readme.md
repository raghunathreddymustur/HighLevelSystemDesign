# Dev To Arch

# Latency in Software Systems

## 1. Latency in Serial Processes

### 1.1. Serial Request Latency

#### 1.1.1. Network Latency

- **Protocols are decided based on intra or internet clients.**
    - **Connection Latency** - Connections are costly
        - **Intranet**: Reuse the connections by using a connection pool.
        - **Internet**: Latest protocols come with persistent connection (e.g., HTTP/1.2).
    - **Data Transfer Latency**
        - Use Caching.
        - Use better data encoding format if interoperability is not an issue.
        - Compress the data.

#### 1.1.2. Memory Latency

- **Avoid memory bloats** - Minimize the code base size.
- **Garbage Collection**
    - Avoid using too much heap space, as it will slow down the garbage collection algorithm.
    - Encourage the usage of weak or soft references.
    - Wisely choose the Garbage Collection algorithm based on requirements.
- **Finite Buffer Memory**
    - Use normalization to reduce duplication so that the data stored in memory is decreased.
    - Prefer compute over storage - don't store the data that is computable.

#### 1.1.3. Disk Latency

- **Logging**
    - Log in batches instead of single logs.
    - Encourage Async logging if the order of logs is not important.
    - Delegate logging to a different thread.
- **Web Content**
    - Cache static content - Store static content in reverse proxy.
- **Database**
    - Write efficient queries.
    - Use appropriate schema normalization or denormalization.
    - Utilize indexing effectively.
    - Write better queries.
    - Consider using better hardware.

#### 1.1.4. CPU Latency

- Write efficient algorithms.
- Avoid context switching due to I/O bounds.
- Batch commits for I/O.
- Use Async processing.
- Use a single-thread model, delegate I/O to a different thread.
- Mindfully create thread pool size to avoid context switching.

## 2. Latency in Concurrent Processes

### 2.1. Concurrency of the application depends upon the percentage of serial processing in between.

### 2.2. Decrease Queuing and Coherence

#### 2.2.1. Contention/Queuing: Due to serial code

- **Coherence:** Due to the refreshment of common code between the thread or process.

#### 2.2.2. Places Where Contention Happens - Where Finite Resources are Possible

1. Creating connections—Connection Pool.
2. Thread pool.
3. Web server request  listen and accept queue.
4. Disk, memory, network.
5. Locks.

#### 2.2.3. Overcoming Contention

- **Choose the right size for listen, accept queue, connection pool, and thread pool.**
    - Decide thread pool size based on:
        - Wait time.
        - CPU time.
- **Vertical Scaling** - Increase system resources for disk, CPU, network resources.

#### 2.2.4. Overcoming Locks Contention
- Keep the minimum possible code inside synchronization.
- Use lock splitting and lock striping techniques
- Use read-write locks.
- Use atomic operations where possible.

## Lock Splitting and Lock Striping Examples in Java

This project demonstrates the concepts of lock splitting and lock striping in Java to reduce lock contention and improve concurrency. Both techniques involve using multiple locks to protect different parts of a data structure, allowing multiple threads to access different parts concurrently.

## Overview

- **Lock Splitting**: Divides a single lock that protects multiple resources into multiple locks, each protecting a smaller subset of resources.
- **Lock Striping**: Divides a single lock that protects a data structure into multiple locks, each responsible for a subset of the data.

## Lock Splitting Example

The following Java code demonstrates lock splitting with separate locks for different resources:

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class LockSplittingExample {
    private final Lock lock1 = new ReentrantLock();
    private final Lock lock2 = new ReentrantLock();

    private int resource1;
    private int resource2;

    public void incrementResource1() {
        lock1.lock();
        try {
            resource1++;
        } finally {
            lock1.unlock();
        }
    }

    public void incrementResource2() {
        lock2.lock();
        try {
            resource2++;
        } finally {
            lock2.unlock();
        }
    }

    public int getResource1() {
        lock1.lock();
        try {
            return resource1;
        } finally {
            lock1.unlock();
        }
    }

    public int getResource2() {
        lock2.lock();
        try {
            return resource2;
        } finally {
            lock2.unlock();
        }
    }

    public static void main(String[] args) {
        LockSplittingExample example = new LockSplittingExample();
        // Example usage
        example.incrementResource1();
        example.incrementResource2();
        System.out.println("Resource1: " + example.getResource1());
        System.out.println("Resource2: " + example.getResource2());
    }
}
```

## Lock Striping Example in Java

This project demonstrates the concept of lock striping in Java to reduce lock contention and improve concurrency. Lock striping involves using multiple locks to protect different parts of a data structure, allowing multiple threads to access different parts concurrently.

## Overview

Lock striping is a technique used to divide a single lock that protects a data structure into multiple locks, each responsible for a subset of the data. This reduces contention and improves performance in multi-threaded environments.

## Example Code

The following Java code demonstrates lock striping with an array of locks protecting an array of resources:

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class LockStripingExample {
    private final Lock[] locks;
    private final int[] resources;

    public LockStripingExample(int numStripes) {
        locks = new ReentrantLock[numStripes];
        resources = new int[numStripes];
        for (int i = 0; i < numStripes; i++) {
            locks[i] = new ReentrantLock();
        }
    }

    public void incrementResource(int index) {
        int stripe = index % locks.length;
        locks[stripe].lock();
        try {
            resources[index]++;
        } finally {
            locks[stripe].unlock();
        }
    }

    public int getResource(int index) {
        int stripe = index % locks.length;
        locks[stripe].lock();
        try {
            return resources[index];
        } finally {
            locks[stripe].unlock();
        }
    }

    public static void main(String[] args) {
        LockStripingExample example = new LockStripingExample(4);
        // Example usage
        example.incrementResource(0);
        example.incrementResource(1);
        System.out.println("Resource 0: " + example.getResource(0));
        System.out.println("Resource 1: " + example.getResource(1));
    }
}
```

## Benefits and Overheads

### Lock Splitting

**Benefits**:
- **Reduced Contention**: By using separate locks for different resources, contention is reduced as threads are less likely to block each other.
- **Increased Concurrency**: Multiple threads can access different resources simultaneously, improving overall throughput.

**Overhead**:
- **Complexity**: Managing multiple locks can increase the complexity of the code.
- **Memory Usage**: Each lock consumes additional memory, which can be significant if there are many locks.

### Lock Striping

**Benefits**:
- **Increased Concurrency**: Multiple threads can work on different parts of the data structure simultaneously, reducing contention.
- **Improved Performance**: With less contention, the overall performance of the application can improve, especially under high concurrency.

**Overhead**:
- **Complexity**: Managing an array of locks and ensuring the correct lock is used for each operation can be more complex than using a single lock.
- **Memory Overhead**: More locks mean more memory usage, which can be significant if the number of stripes is large.

