# Trade-Offs

## CAP

### 📜 The CAP Theorem
The CAP theorem outlines an inherent trade-off in the design of distributed systems.

### 📜 Initial statement of the CAP theorem
It is impossible for a distributed data store to provide more than two of the following properties simultaneously: **consistency**, **availability**, and **partition tolerance**.

### 📜 Partition Tolerance
In a distributed system, there is always the risk of a network partition. If this happens, the system needs to decide either to continue operating and compromise **data consistency**, or stop operating and compromise **availability**.

### 📜 Final statement of the CAP theorem
A distributed system can be either **consistent** or **available** in the presence of a network partition.

### 📜 Proof
The system has two options during a network partition: fail one of the operations and break the **availability** property, or process both operations and break the **consistency** property.

### 📜 Importance of the CAP theorem
The CAP theorem forces designers of distributed systems to make explicit trade-offs between **availability** and **consistency**.

### 📜 Categorization of distributed systems based on the CAP theorem
Systems are usually classified into two basic categories: **CP** (Consistency and Partition tolerance) and **AP** (Availability and Partition tolerance). This classification depends on which property the system violates during a network partition.

### 📜 Trade-off between latency and consistency
When no network partition is present, there’s a trade-off between **latency** and **consistency**. To guarantee data consistency, the system will have to delay write operations until the data has been propagated across the system successfully, thus taking a latency hit.

## PACELC theorem

### 📜 PACELC theorem
The PACELC theorem states that in the case of a network partition (P), the system has to choose between **availability** (A) and **consistency** (C), but else (E), when the system operates normally, it has to choose between **latency** (L) and **consistency** (C).

### 📜 Categorization of distributed systems based on PACELC theorem
Each branch of the PACELC theorem creates two sub-categories of systems: **AP/EL** (Availability during partition, Latency during normal operation) and **CP/EC** (Consistency during partition, Consistency during normal operation). Most systems fall into the AP/EL or CP/EC categories.

Here are some **trade-offs** mentioned in the current page regarding **distributed messaging queues**:

### **⚖️ Trade-offs in Distributed Messaging Queues**
1. **Strict Ordering vs. Throughput**
    - Ensuring **strict message order** requires additional mechanisms like **timestamp-based sorting** and **serialization**.
    - These techniques **introduce processing delays**, reducing the system’s ability to handle large volumes of messages efficiently.
    - Some systems **sacrifice strict ordering** to achieve **higher throughput**, allowing messages to be processed in parallel.

2. **Latency vs. Message Ordering**
    - **Online sorting** ensures messages are processed in the correct sequence but **introduces delays** before messages are ready for extraction.
    - To **reduce latency**, some systems use a **time-window approach**, where messages are **batched and sorted together** instead of sorting each message individually.

3. **Scalability vs. Reliability**
    - A **single-server messaging queue** has **low scalability** but **high reliability** since all messages are processed in one place.
    - A **distributed messaging queue** improves **scalability** but requires **replication and synchronization**, which can introduce **consistency challenges**.

4. **Decoupling vs. Complexity**
    - Messaging queues **decouple dependencies** among different entities, making systems more flexible.
    - However, this **adds complexity**, requiring additional mechanisms for **message tracking, retries, and failure handling**.

Here are some **trade-offs** mentioned in the current page regarding **distributed messaging queues**:

### **⚖️ Trade-offs in Distributed Messaging Queues**
1. **Single-Server vs. Distributed Messaging Queue**
    - A **single-server queue** is simpler but suffers from **low scalability, availability, and durability**.
    - A **distributed messaging queue** improves scalability but introduces **complexity in replication and partitioning**.

2. **Strict Ordering vs. Performance**
    - Enforcing **strict message order** requires **timestamp-based sorting** and **serialization**, which **reduces throughput**.
    - Some systems **sacrifice strict ordering** to achieve **higher performance**, allowing messages to be processed in parallel.

3. **Metadata Storage: Small vs. Large Approach**
    - **Small metadata approach** replicates metadata across all servers, ensuring **fast access** but **higher storage costs**.
    - **Large metadata approach** uses **sharding**, reducing storage costs but **introducing lookup overhead**.

4. **Load Balancing vs. Latency**
    - Using **multiple load balancers** improves **availability** but may introduce **latency** due to request redirection.
    - A **single load balancer** reduces latency but creates a **single point of failure**.

5. **Sharding vs. Replication**
    - **Sharding** distributes data across multiple hosts, improving **scalability** but making **data retrieval more complex**.
    - **Replication** ensures **high availability** but increases **storage and synchronization overhead**.

Here are some **trade-offs** mentioned in the current page regarding **distributed messaging queues**:

### **⚖️ Trade-offs in Distributed Messaging Queues**
1. **Primary-Secondary Model vs. Cluster of Independent Hosts**
    - The **Primary-Secondary Model** ensures **strong consistency** by designating a primary host for each queue, but it **introduces delays** due to replication and primary host election.
    - The **Cluster of Independent Hosts** improves **availability** by distributing queues across multiple hosts, but it **requires additional mapping mechanisms** to track queue locations.

2. **Synchronous vs. Asynchronous Replication**
    - **Synchronous replication** ensures **message consistency** across all replicas but **increases latency** due to waiting for acknowledgments.
    - **Asynchronous replication** improves **performance** by acknowledging the client immediately, but it **introduces replication lag** and potential consistency issues.

3. **Internal vs. External Cluster Managers**
    - **Internal cluster managers** provide **fine-grained control** over individual nodes but **increase complexity** in managing host failures and queue partitioning.
    - **External cluster managers** simplify **cluster-wide management** but **lack detailed visibility** into individual hosts.

4. **Queue Partitioning vs. Load Distribution**
    - **Partitioning queues** across multiple hosts improves **scalability**, but it **requires additional mechanisms** to ensure proper message ordering.
    - **Load distribution** balances requests across clusters, but it **may lead to uneven queue utilization**.


Here are some **trade-offs** mentioned in the current page regarding **distributed messaging queues**:

### **⚖️ Trade-offs in Distributed Messaging Queues**
1. **Strict Ordering vs. Throughput**
    - Enforcing **strict message ordering** requires additional mechanisms like **timestamp-based sorting** and **serialization**, which **reduces throughput**.
    - Relaxed ordering improves **throughput and latency**, but messages may not always be processed in the exact order they were sent.

2. **Message Extraction Order vs. Achievable Latency**
    - If messages are extracted in **strict order**, the system must perform **extra work** to enforce **wall-clock or causality-based ordering**, increasing latency.
    - Allowing **best-effort ordering** reduces latency but may lead to slight reordering.

3. **Replication and Partitioning vs. Scalability**
    - **Replication** ensures **high availability** and **durability**, but it **increases storage and synchronization overhead**.
    - **Partitioning** helps scale data across multiple nodes but **introduces complexity** in maintaining consistency.

4. **Consumer-Tracked Deletion vs. Visibility Timeout**
    - **Consumer-tracked deletion** allows multiple processes to consume a message but requires **tracking mechanisms** to ensure proper deletion.
    - **Visibility timeout** prevents immediate deletion, ensuring **at-least-once delivery**, but may lead to **duplicate processing** if the timeout expires before the consumer finishes processing.


Here are some **trade-offs** mentioned in the current page regarding **distributed caching**:

### **⚖️ Trade-offs in Distributed Caching**
1. **Write-through vs. Write-back vs. Write-around Cache**
    - **Write-through cache** ensures **strong consistency** between cache and database but **increases write latency**.
    - **Write-back cache** improves **write performance** but introduces **potential inconsistency** when stale data is read from the database.
    - **Write-around cache** avoids unnecessary cache writes but **leads to cache misses** when recently updated data is accessed.

2. **Eviction Strategies: LRU vs. LFU vs. FIFO**
    - **Least Recently Used (LRU)** removes the **oldest accessed data**, ensuring frequently used data remains in cache.
    - **Least Frequently Used (LFU)** prioritizes **high-access data**, but requires **tracking access counts**, increasing overhead.
    - **First-In, First-Out (FIFO)** is simple but **does not consider access frequency**, potentially evicting useful data.

3. **Active vs. Passive Cache Expiration**
    - **Active expiration** proactively removes expired cache entries but **requires additional processing**.
    - **Passive expiration** removes expired entries **only when accessed**, reducing overhead but **allowing stale data to persist**.

4. **Dedicated Cache Servers vs. Co-located Cache**
    - **Dedicated cache servers** allow **independent scaling** of cache and application layers but **increase infrastructure costs**.
    - **Co-located cache** reduces hardware costs but **introduces failure risks**, as both cache and application logic reside on the same machine.

5. **Consistent Hashing vs. Simple Hashing**
    - **Consistent hashing** ensures **better load distribution** and **handles scaling gracefully**, but **adds complexity**.
    - **Simple hashing** is easier to implement but **fails when cache servers are added or removed**, leading to **data redistribution issues**.

Here are some **trade-offs** mentioned in the current page regarding **distributed caching**:

### **⚖️ Trade-offs in Distributed Caching**
1. **Specialized Hardware vs. Commodity Hardware**
    - **Specialized hardware** offers **better performance and storage capacity** but comes at a **higher cost**.
    - **Commodity hardware** is more **affordable** but may require **more servers** to achieve similar performance.

2. **Persistence vs. Performance**
    - **Storing cache data on secondary storage** ensures **data availability after a reboot**, but **slows down retrieval** compared to RAM-based caching.
    - **RAM-based caching** provides **fast access** but requires **rebuilding the cache** after failures.

3. **Consistency vs. Scalability**
    - **Ensuring consistency** across cache servers means **synchronizing data**, which **reduces scalability** due to increased coordination overhead.
    - **Relaxed consistency** improves **scalability** but may lead to **stale data** being served.

4. **Eviction Policy Selection**
    - **Least Recently Used (LRU)** ensures **frequently accessed data remains in cache**, but **requires tracking access history**, increasing overhead.
    - **First-In, First-Out (FIFO)** is **simpler** but may **evict useful data** prematurely.

5. **Cache Client Location**
    - **Embedding the cache client within the application server** reduces **network latency** but **limits flexibility** for external users.
    - **Using a dedicated cache client** allows **external access** but introduces **additional communication overhead**.

Here are some **trade-offs** mentioned in the current page regarding **distributed caching**:

### **⚖️ Trade-offs in Distributed Caching**
1. **Configuration Management: Manual vs. Automated**
    - **Manual configuration files** require **human intervention** for updates, making them **prone to errors** and **deployment delays**.
    - **Automated configuration services** eliminate manual updates but **increase operational costs** and **complexity**.

2. **Cache Availability: Primary-Secondary Model vs. No Replication**
    - **Primary-secondary model** improves **availability** but introduces **replication overhead** and **potential consistency issues**.
    - **No replication** simplifies design but **increases the risk of cache unavailability** during failures.

3. **Replication Strategy: Synchronous vs. Asynchronous**
    - **Synchronous replication** ensures **strong consistency** but **increases latency** due to waiting for acknowledgments.
    - **Asynchronous replication** improves **performance** but may lead to **temporary inconsistencies** between replicas.

4. **Eviction Policy: Local vs. API-Based Deletion**
    - **Local eviction** (through TTL and algorithms like LRU) ensures **automatic cleanup** but **does not allow explicit deletions**.
    - **API-based deletion** enables **manual removal** of cache entries but **adds complexity** to cache management.

5. **Consistent Hashing vs. Load Balancing**
    - **Consistent hashing** distributes cache entries **efficiently** but may result in **uneven data distribution** across servers.
    - **Load balancing** helps **redistribute load** but requires **additional monitoring and adjustments**.

Here are some **trade-offs** mentioned in the current page regarding **Memcached vs. Redis**:

### **⚖️ Trade-offs in Distributed Caching**
1. **Simplicity vs. Automation**
    - **Memcached** is simpler but requires **manual cluster management**, giving developers finer control.
    - **Redis** automates **scalability and data division**, reducing manual effort but adding complexity.

2. **Persistence vs. Volatility**
    - **Redis** provides **persistence** using **Append-Only File (AOF) and Redis Database (RDB) snapshots**, ensuring data durability.
    - **Memcached** lacks built-in persistence, requiring **third-party tools** for data recovery.

3. **Data Structure Support vs. Performance**
    - **Redis** supports **multiple data structures** (sorted sets, hash maps, bitmaps, etc.), making it more versatile.
    - **Memcached** only supports **key-value pairs**, but this simplicity allows **faster query speeds**.

4. **Multithreading vs. Single-Threaded Processing**
    - **Memcached** supports **multithreading**, efficiently utilizing **multi-core systems**.
    - **Redis** runs as a **single-threaded process**, reducing complexity but limiting concurrency.

5. **Replication vs. Third-Party Solutions**
    - **Redis** has **built-in replication**, enabling **automatic failover** and **high availability**.
    - **Memcached** requires **third-party tools** for replication, making setup more complex.

6. **Horizontal Scalability vs. Cluster Complexity**
    - **Memcached** scales **horizontally** due to its **shared-nothing architecture**, making it easier to distribute across multiple servers.
    - **Redis** provides **scalability through clustering**, but this approach is **more complex** to configure.

