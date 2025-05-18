# Distributed Cache

## 📜 System Design: The Distributed Cache

Learn the basics of a **distributed cache**, its importance, and how to design it effectively.

---

## 🔍 Problem Statement

A typical system consists of the following components:
- A **client** that requests the service.
- One or more **service hosts** that handle client requests.
- A **database** used by the service for data storage.

Under normal circumstances, this setup works fine. However, as the **number of users increases**, database queries also increase, leading to **performance degradation**.  
To address this, a **cache** is introduced to store frequently accessed data, reducing the load on the database.

---

## 🚀 What is a Distributed Cache?

A **distributed cache** is a caching system where **multiple cache servers** coordinate to store frequently accessed data.  
It is needed when a **single cache server** is insufficient to store all the data.

### **Benefits of Distributed Caches**
- **Minimizes latency** by storing precomputed results.
- **Reduces database load** by caching expensive queries.
- **Stores user session data** temporarily.
- **Ensures availability** even if the database is temporarily down.
- **Reduces network costs** by serving data from local resources.

---

## 🔄 Why Use a Distributed Cache?

When the **size of cached data increases**, storing everything in a **single system** becomes impractical due to:
1. **Single Point of Failure (SPOF)** – A single cache server failure can disrupt the system.
2. **Layered System Design** – Each layer should have its own caching mechanism to ensure **data decoupling**.
3. **Latency Reduction** – Caching at different layers improves **response time**.

### **Caching at Different Layers**
| **System Layer** | **Technology Used** | **Usage** |
|-----------------|--------------------|-----------|
| **Web Layer** | HTTP cache headers, CDNs, key-value stores | Accelerates retrieval of static web content |
| **Application Layer** | Local cache, key-value store | Speeds up application-level computations |
| **Database Layer** | Database cache, buffers | Reduces database I/O load |

Apart from these layers, caching is also performed at **DNS and client-side technologies** like browsers.

---

## 🏗️ How to Design a Distributed Cache?

The design process is divided into **five lessons**:

### **📖 Background of Distributed Cache**
- Covers **fundamental concepts** necessary for designing distributed caches.

### **🛠️ High-Level Design**
- Builds a **scalable and efficient** distributed cache architecture.

### **🔍 Detailed Design**
- Identifies **limitations** of the high-level design and improves **performance**.

### **📊 Evaluation**
- Assesses the design based on **scalability, consistency, and availability**.

### **⚖️ Memcached vs. Redis**
- Compares **two industry-standard caching solutions** to understand their use cases.

---

## 🔚 Conclusion

A **distributed cache** enhances **performance, reliability, and scalability**.  
It is widely used in **web acceleration, session management, database optimization**, and more.

## 📜 Background of Distributed Cache

Learn the fundamentals for designing a **distributed cache**.

---

## 🔍 Motivation

The main goal of this chapter is to **design a distributed cache**.  
To achieve this, we need substantial background knowledge on **reading and writing techniques**.  
This lesson builds that foundation.

---

## ✍️ Writing Policies

Data is written to **cache and databases**.  
The order in which data writing happens has **performance implications**.

### **Types of Writing Policies**
- **Write-through cache** – Writes to both cache and database **simultaneously**, ensuring **strong consistency** but **higher latency**.
- **Write-back cache** – Writes to cache first, then asynchronously to the database, reducing **write latency** but **introducing inconsistency**.
- **Write-around cache** – Writes directly to the database, updating cache **only on read**, which is **inefficient for frequently updated data**.

---

## 🗑️ Eviction Policies

Since cache storage is **limited**, we need **eviction mechanisms** to remove **less frequently accessed data**.

### **Common Eviction Strategies**
- **Least Recently Used (LRU)** – Removes the **oldest accessed data**.
- **Most Recently Used (MRU)** – Removes the **most recently accessed data**.
- **Least Frequently Used (LFU)** – Removes **data accessed the least**.
- **Most Frequently Used (MFU)** – Removes **data accessed the most**.
- **First-In, First-Out (FIFO)** – Removes **oldest inserted data**.

### **Data Temperature Classification**
- **Hot Data** – Frequently accessed.
- **Warm Data** – Moderately accessed.
- **Cold Data** – Rarely accessed (often evicted).

---

## 🔄 Cache Invalidation

Apart from **eviction**, some cached data may become **stale or outdated**.

### **Cache Invalidation Methods**
- **Active Expiration** – A daemon process **actively checks TTL** and removes expired entries.
- **Passive Expiration** – TTL is checked **only when accessed**, removing expired items **on discovery**.

---

## 🗄️ Storage Mechanism

A **distributed cache** consists of **multiple cache servers**.  
Key design questions:
1. **Which cache server should store which data?**
2. **What data structure should be used for storage?**

### **Storage Techniques**
- **Hash Function** – Used to **identify cache servers** and **locate cache entries**.
- **Linked List** – **Doubly linked lists** allow **constant-time operations** for eviction and relocation.
- **Bloom Filters** – Quickly determine if a cache entry **does not exist**, reducing unnecessary lookups.

---

## 🔀 Sharding in Cache Clusters

To avoid **single points of failure (SPOF)** and **high load**, we introduce **sharding**.

### **Sharding Methods**
1. **Dedicated Cache Servers**
    - Separates **application servers** from **cache servers**.
    - Allows **independent scaling** of cache and application layers.
    - Enables **Cache as a Service** for multiple microservices.

2. **Co-located Cache**
    - Embeds cache **within the same host** as the application.
    - **Reduces hardware costs** but **increases failure risks**.

---

## 🖥️ Cache Client

A **cache client** is responsible for **hash calculations** to store and retrieve data.

### **Characteristics of Cache Clients**
- **Knows all cache servers**.
- **Uses TCP or UDP** for communication.
- **Handles cache misses** when a cache server is **unavailable**.

---

## 🔚 Conclusion

In this lesson, we explored:
- **Writing policies** for cache consistency.
- **Eviction strategies** for efficient storage.
- **Cache invalidation** to remove stale data.
- **Storage mechanisms** for optimal performance.
- **Sharding techniques** to improve scalability.
- **Cache clients** for efficient data retrieval.

Here’s a structured **README.md** file with extracted paragraphs, meaningful icons before headings, and highlighted important sections:


## 📜 High-Level Design of a Distributed Cache

Learn how to develop a **high-level design** for a distributed cache, covering **requirements, API design, storage considerations, and eviction policies**.

---

## 🎯 Requirements

### **🔹 Functional Requirements**
A **distributed cache system** must support the following operations:
- **Insert Data** – Users should be able to add entries to the cache.
- **Retrieve Data** – Users should be able to fetch data using a specific key.

These operations are commonly referred to as **Put** and **Get**.

### **⚙️ Non-Functional Requirements**
A distributed cache must meet several **performance and reliability** criteria:
- **High Performance** – Ensures **fast retrieval** of cached data.
- **Scalability** – Must scale **horizontally** without bottlenecks.
- **High Availability** – Prevents **database overload** during peak traffic.
- **Consistency** – Ensures **data uniformity** across cache servers.
- **Affordability** – Should be built using **commodity hardware** rather than expensive components.

---

## 🛠️ API Design

### **📥 Insertion API**
```python
insert(key, value)
```
- **key** – A unique identifier.
- **value** – Data stored against the key.
- **Returns** – Acknowledgment or error message.

### **📤 Retrieval API**
```python
retrieve(key)
```
- **key** – Identifier for stored data.
- **Returns** – Cached data object.

### **❓ Point to Ponder**
**How does a distributed cache differ from a key-value store?**
- **Key-value stores** ensure **durability**, while caches prioritize **speed**.
- **Caches** store data in **RAM**, whereas key-value stores use **non-volatile storage**.
- **Caches** can be **rebuilt after failure**, while key-value stores must **persist data**.

---

## 🏗️ Design Considerations

### **💾 Storage Hardware**
- **Sharding** may be required for **large datasets**.
- **Commodity hardware** is cost-effective but **specialized hardware** offers better performance.
- **Secondary storage** can be used for **persistence** during reboots.

### **📂 Data Structures**
- **Hash Tables** – Enable **constant-time retrieval**.
- **Linked Lists** – Support **efficient eviction algorithms**.
- **Flexible Storage** – Caches can store **hash maps, arrays, sets**, etc.

### **🖥️ Cache Client**
- **Handles insert and retrieve requests**.
- **Can be embedded within application servers** or **provided as a service**.

---

## ✍️ Writing Policy

The **writing strategy** affects **consistency** between cache and database.

### **🔄 Common Writing Policies**
- **Write-Through** – Writes to **cache and database simultaneously** (ensures consistency but increases latency).
- **Write-Back** – Writes to **cache first**, then asynchronously to the database (reduces latency but risks inconsistency).
- **Write-Around** – Writes **directly to the database**, updating cache **only on read** (inefficient for frequently updated data).

---

## 🗑️ Eviction Policy

Since **cache storage is limited**, an **eviction mechanism** is needed.

### **🚀 Common Eviction Strategies**
- **Least Recently Used (LRU)** – Removes **oldest accessed data**.
- **Most Recently Used (MRU)** – Removes **most recently accessed data**.
- **Least Frequently Used (LFU)** – Removes **least accessed data**.
- **First-In, First-Out (FIFO)** – Removes **oldest inserted data**.

### **⏳ Optimizing Time-to-Live (TTL)**
- **TTL settings** help **reduce cache misses**.
- **Short TTL** ensures **fresh data**, while **long TTL** improves **performance**.

---

## 🏗️ High-Level Design

### **🔀 Components of a Distributed Cache**
1. **Cache Client** – Manages **cache server selection** using **hashing algorithms**.
2. **Cache Servers** – Store cached data and **communicate with databases**.
3. **Load Balancer** – Distributes requests **efficiently** across cache servers.
4. **Persistence Layer** – Ensures **data durability** when needed.

### **📡 Communication Protocols**
- **Cache clients use TCP or UDP** for data transfer.
- **Missed cache requests** are **resolved via fallback mechanisms**.

---

## 🔚 Conclusion

In this lesson, we explored:
- **Functional and non-functional requirements** of a distributed cache.
- **API design** for insertion and retrieval.
- **Storage and eviction strategies** for efficient caching.
- **High-level architecture** of a distributed cache.

## 🏗️ Detailed Design of a Distributed Cache

This lesson identifies **shortcomings** in the high-level design of a **distributed cache** and improves the design to cover the gaps.

---

## 🔍 Identifying Limitations

Before refining the design, we must address **key challenges**:
- **Cache clients cannot detect** the addition or failure of cache servers.
- The system suffers from a **single point of failure (SPOF)** since each cache server holds a unique set of data.
- **Hotkey problem** – Some cache servers store frequently accessed data, leading to **performance bottlenecks**.
- The **internals of cache servers** (data structures and eviction policies) were not clearly defined.

---

## 📜 Maintaining Cache Server List

To resolve the **cache server detection issue**, we explore **three solutions**:

### **📝 Solution 1: Local Configuration File**
- Each **service host** maintains a **configuration file** containing metadata about cache servers.
- **Updated via push service** using DevOps tools.
- **Drawback:** Requires **manual updates** and deployment.

### **📂 Solution 2: Centralized Configuration File**
- Stores the **configuration file in a central location**.
- Cache clients **fetch updated server information** from this location.
- **Drawback:** Still requires **manual updates** and **server health monitoring**.

### **⚙️ Solution 3: Configuration Service**
- A **configuration service** continuously **monitors cache servers**.
- Cache clients **automatically receive updates** when a new cache server is added.
- **Pros:** No **human intervention** required.
- **Cons:** **Higher operational cost** and **complexity**.

Among these solutions, the **configuration service** is the **most robust**.

---

## 🔄 Improving Availability

To prevent **cache unavailability** due to server failures, we introduce **replica nodes**.

### **🖥️ Primary-Secondary Model**
- Each **cache shard** consists of **one primary node** and **two backup nodes**.
- **Synchronous replication** ensures **consistency** between replicas.
- **Advantages**:
    - **Improved availability** in case of failures.
    - **Hot shards** can have **multiple secondary nodes** for read operations.

This solution **enhances both availability and performance**.

---

## 🏗️ Internals of Cache Server

Each **cache client** uses **three mechanisms** to store and evict entries:

### **🔍 Hash Map**
- Stores cache entries in **RAM**.
- Each entry is **mapped to a pointer** for quick lookup.

### **🔗 Doubly Linked List**
- Maintains **ordering of entries** based on **access frequency**.
- Supports **efficient eviction**.

### **🗑️ Eviction Policy**
- The **Least Recently Used (LRU)** eviction policy is assumed.
- **Entries are removed** based on **access patterns**.

### **📌 Cache Shard Structure**
Each **cache shard** consists of:
- **Primary and secondary nodes**.
- **Internally consistent storage mechanisms**.

---

## 🏗️ Formalized Detailed Design

After resolving the **three major issues**, we finalize the **detailed design**:

### **📡 System Components**
1. **Clients** – Send requests to cache servers.
2. **Load Balancer Layer** – Distributes requests efficiently.
3. **Cache Shards** – Store and manage cache entries.
4. **Configuration Service** – Ensures **consistent cache server updates**.
5. **Monitoring Service** – Logs and reports **cache performance metrics**.

### **📌 Key Design Aspects**
- **Consistent hashing** is used to **identify cache servers**.
- **Primary and replica servers** ensure **high availability**.
- **Cache entries are stored in RAM** for **fast retrieval**.

---

## ❓ Point to Ponder

**While consistent hashing is effective, it may result in uneven data distribution. How can we resolve this issue?**

### **✅ Solution**
- Use **advanced consistent hashing algorithms** that distribute load **uniformly**.
- Introduce **virtual servers** within each cache server.
- The **number of virtual servers** depends on **machine capability**.
- This approach **enhances availability** and **balances load**.

---

## 🔚 Conclusion

In this lesson, we refined the **detailed design** of a **distributed cache**, covering:
- **Cache server detection mechanisms**.
- **Availability improvements** using **replica nodes**.
- **Internals of cache servers** (hash maps, linked lists, eviction policies).
- **Formalized architecture** with **consistent hashing and monitoring services**.

Here’s a structured **README.md** file with extracted paragraphs, meaningful icons before headings, and highlighted important sections:

## 📜 Evaluation of a Distributed Cache's Design

Let's evaluate our **distributed cache design** based on key requirements.

---

## 🚀 High Performance

### **🔍 Key Design Choices for Performance**
- **Consistent hashing** ensures efficient key lookup with **O(log(N))** complexity.
- **Hash tables** inside cache servers enable **constant-time key retrieval**.
- **LRU eviction** allows **fast access and updates** using a **doubly linked list**.
- **TCP and UDP protocols** facilitate **high-speed communication** between cache clients and servers.
- **Replica nodes** reduce performance penalties under **high request loads**.
- **RAM-based storage** ensures **low-latency data retrieval**.

### **📊 Impact of Eviction Algorithm on Performance**
A critical factor in performance is the **eviction algorithm**, which affects **cache hit rates**.

#### **Example Calculation**
- **Cache hit service time (99.9th percentile):** **5 ms**
- **Cache miss service time (99.9th percentile):** **30 ms** (includes database retrieval and cache update)

Using the **Most Frequently Used (MFU) algorithm**:
```
EAT = (0.90 × 5 ms) + (0.10 × 30 ms) = 7.5 ms
```
Using the **Least Recently Used (LRU) algorithm**:
```
    EAT = (0.95 × 5 ms) + (0.05 × 30 ms) = 6.25 ms
```

**Conclusion:**  
Each application should **empirically test** eviction algorithms to optimize cache hit rates.

---

## 📈 Scalability

### **🔄 Scaling Strategies**
- **Sharding** allows dynamic scaling based on **server load**.
- **Consistent hashing** minimizes **rehash computations** when adding new cache servers.
- **Replica nodes** reduce load on **hot shards**.
- **Further sharding** within hotkey ranges prevents **single-key bottlenecks**.

### **❓ Handling Hotkeys**
- Cache clients can **intelligently distribute requests** to avoid bottlenecks.
- **Dynamic replication** can be applied to **specific keys**.

---

## 🔄 High Availability

### **🛠️ Redundancy for Reliability**
- **Replica nodes** improve **fault tolerance**.
- **Leader-follower algorithm** efficiently manages **cluster shards**.

### **⚖️ Trade-off: Availability vs. Consistency**
- **Higher availability** can be achieved by **splitting leader and follower servers** across **data centers**.
- **Synchronous writes** ensure **strong consistency** but **increase latency**.
- **Asynchronous replication** improves **performance** but **reduces consistency**.

---

## 🔗 Consistency

### **📌 Synchronous vs. Asynchronous Writes**
- **Synchronous writes** ensure **strong consistency** but **increase latency**.
- **Asynchronous writes** improve **performance** but **introduce inconsistencies**.

### **⚠️ Handling Inconsistencies**
- **Faulty configuration files** can cause **cache inconsistencies**.
- **Cache servers recovering from failure** should **not serve requests** until **fully updated**.

---

## 💰 Affordability

### **💡 Cost Considerations**
- The design is **feasible using commodity hardware**.
- **Lower infrastructure costs** make it **practical for large-scale deployment**.

---

## ❓ Points to Ponder

### **🤔 Leader Node Failure**
If the **leader node fails**, two solutions exist:
1. **Leader election algorithm** selects a new leader from available followers.
2. **Distributed configuration management service** monitors and selects leaders.

---

## 🔚 Summary

We evaluated our **distributed cache design**, covering:
- **High performance** (consistent hashing, eviction strategies, RAM-based storage).
- **Scalability** (sharding, hotkey management).
- **High availability** (replica nodes, leader-follower model).
- **Consistency** (synchronous vs. asynchronous writes).
- **Affordability** (commodity hardware feasibility).

## 🏗️ Memcached vs. Redis: A Comparison

This lesson explores two widely adopted **distributed caching frameworks**: **Memcached** and **Redis**.

---

## 🔍 Introduction

Memcached and Redis are **highly scalable, high-performance caching tools** that follow the **client-server model**.  
Both achieve **sub-millisecond latency**, making them ideal for **fast data retrieval**.

---

## 🚀 Memcached Overview

Memcached was introduced in **2003** as a **key-value store** designed for **fast object storage**.  
It stores data as **key-value pairs**, where both the **key and value are strings**.

### **⚠️ Limitations**
- **Serialization required** – Data must be converted into strings.
- **No support for complex data structures** – Only key-value pairs.
- **Shared-nothing architecture** – Servers **do not communicate** with each other.

### **✅ Advantages**
- **Deterministic query speed** – Achieves **O(1) complexity**.
- **High throughput** – Serves **millions of keys per second**.
- **Horizontal scalability** – Clients use **hashing algorithms** to locate keys.

---

## 📌 Facebook and Memcached

Facebook adopted **Memcached** due to its **simplicity and speed**.  
Memcached sits between **MySQL and the web layer**, handling **frequent reads and updates**.

### **📊 Facebook’s Memcached Usage**
- **28 TB RAM** across **800+ servers** (as of 2013).
- **95% cache hit rate** using **LRU eviction policy**.
- **Reduces database queries** from **50M to 2.5M requests**.

---

## 🏗️ Redis Overview

Redis, introduced in **2009**, is a **data structure store** that functions as a **cache, database, and message broker**.

### **✅ Features**
- **Supports multiple data structures** – Strings, sorted sets, hash maps, bitmaps, hyper logs.
- **Built-in replication** – Ensures **high availability**.
- **Automatic failover** – Redis Sentinel detects failures and **performs recovery**.
- **Pipelining** – Reduces **latency** by batching multiple requests.

### **⚠️ Limitations**
- **Single-threaded process** – Uses **one core**, limiting concurrency.
- **No strong consistency** – Uses **asynchronous replication**.

---

## 🔄 Redis Cluster Architecture

Redis clusters provide **automatic sharding** with **primary and secondary nodes**.  
Each cluster is managed by a **cluster manager**, which detects failures and **performs automatic failovers**.

### **📡 Redis Cluster Components**
- **Primary nodes** – Handle **write operations**.
- **Secondary nodes** – Handle **read operations** and **failover recovery**.
- **Cluster manager** – Monitors **node health** and **performs failovers**.

---

## ⚡ Pipelining in Redis

Redis uses **pipelining** to **reduce latency** by **batching multiple requests**.  
Instead of waiting for each response, the client sends **multiple requests at once**.

### **✅ Benefits**
- **Reduces RTT (Round Trip Time)**.
- **Minimizes socket-level I/O overhead**.
- **Improves throughput** by **fivefold** when used on local machines.

---

## ⚖️ Memcached vs. Redis: Key Differences

| **Feature** | **Memcached** | **Redis** |
|------------|--------------|-----------|
| **Low latency** | ✅ Yes | ✅ Yes |
| **Persistence** | ❌ No (third-party tools) | ✅ Yes (AOF, RDB) |
| **Multithreading** | ✅ Yes | ❌ No |
| **Data structures** | ❌ Only key-value pairs | ✅ Multiple data types |
| **Replication** | ❌ No (third-party tools) | ✅ Built-in |
| **Transaction support** | ❌ No | ✅ Yes |
| **Eviction policy** | ✅ LRU | ✅ Multiple algorithms |
| **Geospatial support** | ❌ No | ✅ Yes |

### **📌 Summary**
- **Memcached** is ideal for **simple, read-heavy systems**.
- **Redis** is better for **complex, read-write-heavy applications**.

---

## 🔚 Conclusion

Caching systems are **essential for high-speed, large-scale applications**.  
This lesson covered **Memcached and Redis**, their **design, features, and trade-offs**.

