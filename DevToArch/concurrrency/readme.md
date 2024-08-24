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

## Concurrency Concepts: Contention and Pessimistic Locking

## Contention

**Contention** in concurrency refers to the situation where multiple threads or processes compete for the same resources simultaneously. This competition can lead to various issues, including:

- **Resource Competition**: Multiple threads or processes trying to access shared resources (e.g., memory, CPU, data) at the same time.
- **Lock Contention**: Occurs when multiple threads attempt to acquire the same lock, causing threads to be blocked until the lock is released.
- **Performance Bottlenecks**: High contention can degrade system performance, reducing throughput and increasing latency.
- **Deadlocks**: Severe contention can lead to deadlocks, where threads wait indefinitely for resources held by each other.
- **High-Concurrency Environments**: Contention is more prevalent in environments with numerous simultaneous transactions or operations.

## Pessimistic Locking

**Pessimistic Locking** is a concurrency control mechanism used to prevent conflicts in high-contention environments by locking resources before accessing them. Key points include:

- **Preventing Conflicts**: Ensures that once a transaction locks a resource, no other transaction can access it until the lock is released, maintaining data integrity.
- **Consistency**: Guarantees that the data read by a transaction is consistent and not modified by other transactions.
- **Avoiding Deadlocks**: By managing locks carefully, pessimistic locking can help avoid deadlocks.
- **Simplicity**: Easier to implement and reason about compared to optimistic locking, especially in complex systems.
- **Critical Sections**: Ensures that critical sections of code are executed atomically without interference from other transactions.

Pessimistic locking is particularly useful in scenarios with high contention for resources, where data consistency and integrity are more important than performance.

![img.png](img.png)

## E-Commerce Application with Optimistic Locking

## Overview
Optimistic locking is a powerful technique for managing concurrency in high-performance applications. By detecting conflicts at commit time rather than locking resources upfront, it allows for greater scalability and efficiency, making it ideal for scenarios like e-commerce where multiple users interact with the same data simultaneousl

This project demonstrates the use of optimistic locking in a simple e-commerce application. Optimistic locking is a concurrency control mechanism that allows multiple transactions to proceed without locking resources upfront. Instead, it checks for conflicts before committing changes, making it suitable for high-concurrency environments where conflicts are rare.

## Key Concepts

- **Concurrency Control**: Optimistic locking helps manage access to shared resources in a multi-threaded environment, ensuring data integrity and consistency.
- **Conflict Detection**: Instead of locking resources, optimistic locking detects conflicts at the time of committing a transaction. If a conflict is detected (e.g., another transaction has modified the data), the transaction is rolled back and can be retried.
- **Versioning**: Typically, a version field is used in the database to track changes. Each time a transaction updates a record, it increments the version number. When committing, the transaction checks if the version number has changed, indicating a conflict.

## Benefits

- **Performance**: Optimistic locking allows for higher throughput as it doesn't lock resources upfront, reducing the chances of blocking other transactions.
- **Scalability**: Suitable for high-concurrency environments where conflicts are infrequent, making it ideal for applications with many simultaneous users.
- **Simplicity**: Easier to implement in scenarios where the likelihood of conflicts is low, avoiding the complexity of managing locks.

## Example Scenario

In an e-commerce application, multiple customers might try to purchase the same product simultaneously. Optimistic locking ensures that the inventory count remains accurate by checking for conflicts before updating the inventory. If a conflict is detected (e.g., another customer has already purchased the product), the transaction is rolled back, and the customer is informed that the product is out of stock.
![img_1.png](img_1.png)

## Compare and Swap (CAS) in Java with E-commerce Example

## Overview

**Compare and Swap (CAS)** is a low-level atomic operation used in concurrent programming to achieve synchronization without using locks. In Java, CAS is primarily implemented in classes like `AtomicInteger`, `AtomicLong`, `AtomicReference`, etc., provided by the `java.util.concurrent.atomic` package.

## How CAS Works

- **Compare:** It reads the current value from a variable.
- **Swap:** If the current value matches an expected value, it updates the variable with a new value.
- If the current value doesn't match the expected value, the operation is retried or aborted, ensuring that only one thread can successfully update the variable at a time without locks.

## CAS in E-commerce: Real-time Example

Let's consider an e-commerce platform where multiple users are trying to purchase the last item in stock. The system needs to update the inventory count atomically to ensure that the count doesn't go negative or multiple users don't purchase the same last item.

### Scenario: Inventory Management for a Product

**Problem:** Multiple users are trying to purchase the last item simultaneously. We need to decrement the stock count safely, ensuring no more than the available items are sold.

**Solution: Using CAS with `AtomicInteger`**

```java
import java.util.concurrent.atomic.AtomicInteger;

public class Inventory {
    private AtomicInteger stock;

    public Inventory(int initialStock) {
        this.stock = new AtomicInteger(initialStock);
    }

    public boolean purchaseItem() {
        while (true) {
            int currentStock = stock.get();
            if (currentStock == 0) {
                System.out.println("Out of stock");
                return false;  // No stock left
            }
            // Attempt to decrement the stock
            if (stock.compareAndSet(currentStock, currentStock - 1)) {
                System.out.println("Purchase successful! Remaining stock: " + (currentStock - 1));
                return true;  // Purchase successful
            }
            // If compareAndSet fails, another thread has modified the stock; retry
        }
    }

    public int getStock() {
        return stock.get();
    }

    public static void main(String[] args) {
        Inventory inventory = new Inventory(1); // Only 1 item in stock

        // Simulate multiple users trying to purchase the last item
        Thread user1 = new Thread(inventory::purchaseItem);
        Thread user2 = new Thread(inventory::purchaseItem);

        user1.start();
        user2.start();
    }
}
```
### Explanation

- **AtomicInteger:** The `stock` is represented using an `AtomicInteger`, allowing atomic operations on the stock count.
- **compareAndSet:** The `purchaseItem()` method uses `compareAndSet()` to ensure that only one thread can decrement the stock when the current stock is equal to the expected stock.
- **Thread Safety:** This approach ensures that if multiple users try to purchase the last item at the same time, only one of them succeeds, and the stock count is correctly updated without race conditions.

In this example, if two users try to buy the last item at the same time, one will succeed, and the other will receive an "Out of stock" message. This is achieved without using traditional locks, making the system more efficient in a high-concurrency environment like e-commerce.

## Is CAS a Good Idea When There Is High Contention?

### Advantages of CAS:
1. **Lock-Free:** CAS avoids the overhead of traditional locks, reducing the risk of thread contention and deadlocks.
2. **Performance:** In low to moderate contention, CAS can be very fast since it allows multiple threads to attempt the operation concurrently without blocking.

### Disadvantages of CAS in High Contention:
1. **Spinning/Retry Loop:** If many threads are contending to update the same variable, CAS may lead to frequent failures and retries, which can cause a performance degradation. The threads may end up in a spinning loop, repeatedly attempting the operation, which can consume significant CPU resources.
2. **Starvation:** In some cases, a thread may never succeed in updating the value if other threads continuously succeed before it, leading to potential starvation.
3. **Complexity:** The retry logic in CAS can make the code more complex, especially in scenarios where multiple variables need to be updated atomically, which might require additional techniques like using `AtomicReference` or `AtomicStampedReference`.

### Alternatives to CAS in High Contention:
1. **Locks:** In high contention scenarios, traditional locks (`synchronized`, `ReentrantLock`) might perform better as they can prevent excessive spinning and ensure that only one thread modifies the shared resource at a time.
2. **Optimistic Locking:** This technique involves attempting an operation and only locking if the operation fails due to contention. It can be seen as a hybrid approach, where CAS is used first, and if contention is detected, the system falls back to locking.
3. **Striped Locks:** Instead of using a single lock or CAS on one variable, use a set of locks on different segments of the data. This reduces contention by distributing the workload across multiple locks.
4. **Staged CAS (or Phased CAS):** This approach involves splitting the update operation into smaller stages, each using CAS, to reduce the likelihood of contention on any single CAS operation.

### When to Use CAS:
- **Low to Moderate Contention:** CAS works well when the probability of contention is low to moderate, as it offers better performance than locking in these cases.
- **Read-Mostly Scenarios:** CAS is effective when most operations are reads, and only a few operations are updates, as the contention is naturally low.
- **Fine-Grained Control:** If you can design your system to reduce contention (e.g., by sharding data or minimizing shared variables), CAS can still be viable even with multiple threads.



