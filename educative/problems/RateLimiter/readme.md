# Rate Limiter

## 🚦 System Design: The Rate Limiter

### ❓ What is a rate limiter?
A **rate limiter**, as the name suggests, puts a limit on the number of requests a service fulfills. It **throttles requests** that cross the predefined limit.  
For example, a client using an API configured to allow **500 requests per minute** would **block further incoming requests** if the client exceeds that limit.

### 🎯 Why do we need a rate limiter?
A **rate limiter** acts as a **defensive layer** for services, preventing **excessive usage**, whether intentional or unintended. It protects services from **abusive behaviors** such as **Denial-of-Service (DoS) attacks** and **brute-force password attempts**.

#### 🔒 Preventing resource starvation
Some **denial of service incidents** are caused by software errors or **misconfigurations**, leading to **resource starvation**. Such attacks are called **friendly-fire DoS**.  
A **rate limiter** ensures **resource allocation** by **preventing unintentional or malicious overload**.

#### 🏷 Managing policies and quotas
Rate limiters enforce **fair usage policies** by **setting limits on time duration or allocated quotas** to **prevent misuse of shared resources**.

#### 🔄 Controlling data flow
Systems **processing large amounts of data** use rate limiters to **distribute workloads evenly** across machines, avoiding overload on a **single machine**.

#### 💰 Avoiding excess costs
Organizations use **rate limiting** to **control costs**, preventing **uncontrolled experiments** leading to **high operational expenses**.  
Cloud providers implement **freemium services** with limits that can be **expanded for a fee**.

### 🛠 How will we design a rate limiter?
In the upcoming sections, we'll explore:

- **📜 Requirements**: Functional and non-functional needs, types of throttling, and placement of rate limiters.
- **🔍 High-level design**: An overview of the rate limiter's **architecture**.
- **🔬 Detailed design**: Explanation of **building blocks** involved.
- **🔢 Rate limiter algorithms**: Discussion of different **algorithms** crucial for rate limiter operations.



## 📌 Requirements of a Rate Limiter’s Design
Understand the **requirements** and important concepts of a **rate limiter**.

### 📜 Functional requirements
- **Limit the number of requests** a client can send to an API within a time window.
- **Configurable request limits** per time window.
- **Notify clients** when the request limit is exceeded, either through error messages or notifications.

### ⚙️ Non-functional requirements
- **High availability**: Since the rate limiter protects the system, it must be **highly available**.
- **Low latency**: Requests pass through the rate limiter, so it should introduce **minimal latency**.
- **Scalability**: The system must **handle increasing requests** effectively.

## 🚀 Types of Throttling
Rate limiters use **different throttling mechanisms** based on needs.

### ⛔ Hard throttling
A strict limit on requests—**any request beyond the limit is discarded** immediately.

### 🔄 Soft throttling
Allows **requests to exceed the limit** by a small percentage (e.g., **5% over 500 requests per minute**).

### 🌐 Elastic or dynamic throttling
Requests **exceed the predefined limit** if **excess resources** are available.

## 🖥️ System-Level Resource Management
Linux provides **cgroups (control groups)** to **limit, monitor, and isolate system resources** like CPU time, memory, disk storage, and network bandwidth.

### 🔒 Benefits of cgroups
- **Resource limiting**: Restrict **memory usage** or file system access.
- **Prioritization**: Allocate **CPU cycles** or **disk I/O throughput** preferentially.
- **Accounting**: Measure **resource consumption** (useful for billing).
- **Process control**: **Checkpoint, restart, and manage groups** dynamically.

## 📍 Placement Strategies for Rate Limiter
Where the rate limiter is placed affects **security and effectiveness**.

### 🤖 On the client side
- **Easy to implement** but **vulnerable to tampering**.
- **Difficult to configure centrally**.

### 🏢 On the server side
- **More secure** since requests **pass through a server-side limiter**.
- **Better enforcement of policies**.

### 🔗 As middleware
- The **rate limiter sits between clients and API servers**.
- Ensures **fine-grained throttling across multiple servers**.

## 🛠️ Models for Implementing a Rate Limiter
**Multiple rate limiters** may be necessary in large-scale systems.

### 🌍 Centralized database model
- **Stores rate limits centrally** (e.g., **Redis or Cassandra**).
- **Prevents clients from exceeding the limit**.
- **Drawbacks**: **Latency issues** when handling a large number of requests and **potential race conditions**.

### 🌎 Distributed database model
- **Each node tracks its own rate limits**.
- **Possible to exceed limits momentarily** due to **state synchronization delays**.
- **Requires sticky sessions** in a **load balancer** for enforcement.

### 🎭 Global vs. Individual Counters
Rate-limiting can be enforced using:
1. **A shared counter** for all requests (global enforcement).
2. **Individual counters per user** (personalized rate limits).

Choosing the right method depends on **specific use cases**.

## 🧠 Points to Ponder
### 🔀 Can a load balancer act as a rate limiter?
- **Load balancers regulate traffic** by distributing requests but **do not recognize operation complexities**.
- **Rate limiters provide fine-grained control**, helping **throttle specific operations efficiently**.

## 🏗️ Building Blocks Used in Rate Limiter Design
### 🏛️ Database
Stores **rate-limiting rules and metadata** of users.

### ⚡ Cache
Caches **rules and user data** for quick access.

### 🎟️ Queue
Holds **incoming requests** permitted by the rate limiter.

---

## 🚀 Design of a Rate Limiter

### 🏗 High-level design
A rate limiter can be deployed as a separate service that interacts with a web server. When a request is received, the rate limiter suggests whether it should be forwarded.

**Rate-limiting rules:**  
The rate limiter consists of rules defining the throttling limit for each operation. A sample rule from Lyft states:
- **Domain:** Messaging
- **Descriptors:** `message_type: marketing`
- **Rate limit:** `Unit: day, Request_per_unit: 5`

### 📌 Detailed design
The high-level design leaves unanswered questions such as **where rules are stored and how rate-limited requests are handled**.

To expand the architecture, several components are introduced:
- **Rule database:** Contains defined rules.
- **Rules retriever:** Periodically checks for updates.
- **Throttle rules cache:** Stores rules for fast access.
- **Decision-maker:** Decides if a request should be allowed.
- **Client identifier builder:** Generates unique request IDs.

### 🔄 Request Processing
Upon receiving a request, the **client identifier builder** forwards it to the **decision-maker**, which checks the **throttle rules cache**.

If within limits, the request proceeds to the **request processor**. **Soft or elastic throttling** allows exceeding the limit but may queue requests, while **hard throttling** outright rejects excess requests.

### ⚠ Race Condition
A race condition occurs during high concurrency when multiple processes update counters simultaneously, potentially **bypassing rate limits**.

**Solutions include:**
- **Locking mechanism** (causes bottlenecks).
- **Set-then-get approach** (avoids contention).
- **Sharded counters** (distribute quota across multiple locations).

### 🎯 Rate Limiter in Client’s Critical Path
In high-traffic scenarios, **checking request count first and updating cache later** improves performance.

Example:
| Request ID | Maximum Limit | Current Count |
|------------|-------------|--------------|
| 100        | 5           | 4            |
| 101        | 5           | 3            |

If below the limit, the rate limiter allows the request and **updates the cache offline** to **reduce latency**.

### 📌 Conclusion
The designed rate limiter meets key **non-functional requirements**:
- **Availability:** Eliminates single points of failure.
- **Low Latency:** Uses cache instead of database queries.
- **Scalability:** Adapts to incoming request load.

---

Here are the tradeoffs mentioned in the rate limiter design:

### ⚖️ Tradeoffs in Rate Limiter Design

#### 🔄 Race Condition Handling
- **Locking Mechanism:** Ensures only one process updates the counter at a time, preventing inconsistencies.
    - **Tradeoff:** Causes bottlenecks and degrades performance under high concurrency.
- **Set-then-get Approach:** Increments values efficiently without locking.
    - **Tradeoff:** Works well with minimal contention but may still lead to inconsistencies.
- **Sharded Counters:** Distributes quota across multiple locations to reduce contention.
    - **Tradeoff:** Improves scalability but slows down read operations due to data collection from multiple shards.

#### 🚀 Rate Limiter in Client’s Critical Path
- **Online Updates:** Requests are checked against limits before being forwarded.
    - **Tradeoff:** Ensures real-time enforcement but increases latency.
- **Offline Updates:** Request counts are updated asynchronously to reduce contention.
    - **Tradeoff:** Improves performance but may lead to temporary inconsistencies.

#### ⚠️ Hard vs. Soft Throttling
- **Hard Throttling:** Strictly rejects requests exceeding the limit.
    - **Tradeoff:** Guarantees control but may frustrate users.
- **Soft/Elastic Throttling:** Allows exceeding limits and queues requests for later processing.
    - **Tradeoff:** Improves user experience but risks system overload.

## 🚀 Rate Limiter Algorithms

### 🏗 Overview
Rate limiting is a crucial technique used to control the rate of incoming requests to a system. Various algorithms help achieve this, each with distinct advantages and disadvantages.

### 🎭 Token Bucket Algorithm
This algorithm uses a bucket analogy where tokens are periodically added at a constant rate. Each request consumes a token, and if the bucket is empty, the request is rejected.

**Key Parameters:**
- **Bucket Capacity (C):** Maximum number of tokens.
- **Rate Limit (R):** Allowed requests per unit time.
- **Refill Rate (1/R):** Time interval for adding tokens.
- **Requests Count (N):** Tracks incoming requests.

**Advantages:**
- **Allows bursts** of traffic within defined limits.
- **Space-efficient** due to minimal memory usage.

**Disadvantages:**
- **Choosing optimal values** for parameters is challenging.
- **Can exceed limits** at the edges due to refill timing.

### 💧 Leaking Bucket Algorithm
Similar to the token bucket but processes requests at a **constant rate**. Incoming requests are queued in a bucket and processed in FIFO order.

**Key Parameters:**
- **Bucket Capacity (C):** Maximum request storage.
- **Inflow Rate (R_in):** Varies based on incoming requests.
- **Outflow Rate (R_out):** Fixed processing rate.

**Advantages:**
- **Prevents bursts** by processing requests steadily.
- **Space-efficient** with minimal state tracking.

**Disadvantages:**
- **Bucket overflow** can lead to dropped requests.
- **Determining optimal bucket size** is difficult.

### ⏳ Fixed Window Counter Algorithm
Divides time into fixed intervals (windows) and assigns a counter to each. If the counter exceeds the limit, new requests are discarded.

**Key Parameters:**
- **Window Size (W):** Defines time intervals.
- **Rate Limit (R):** Allowed requests per window.
- **Requests Count (N):** Tracks incoming requests.

**Advantages:**
- **Space-efficient** due to limited state tracking.
- **Services new requests** even if previous ones were rejected.

**Disadvantages:**
- **Edge case issues** can lead to bursts exceeding limits.

### 📜 Sliding Window Log Algorithm
Tracks each request’s arrival time in a log. Requests are allowed based on log size and timestamps.

**Key Parameters:**
- **Log Size (L):** Defines request limit.
- **Arrival Time (T):** Tracks timestamps.
- **Time Range (T_r):** Defines window duration.

**Advantages:**
- **Avoids edge case issues** of fixed window counters.

**Disadvantages:**
- **Consumes extra memory** for storing timestamps.

### 🔄 Sliding Window Counter Algorithm
Combines fixed window and sliding window log approaches for smoother request flow.

**Key Parameters:**
- **Rate Limit (R):** Maximum allowed requests.
- **Window Size (W):** Defines time intervals.
- **Previous Window Requests (R_p):** Tracks past requests.
- **Current Window Requests (R_c):** Tracks ongoing requests.
- **Overlap Time (O_t):** Defines rolling window overlap.

**Advantages:**
- **Smooths out bursts** for better request distribution.
- **Space-efficient** with limited state tracking.

**Disadvantages:**
- **Assumes evenly distributed requests**, which may not always be true.

### ⚖️ Comparison of Rate-Limiting Algorithms
| Algorithm | Space Efficiency | Burst Handling |
|-----------|----------------|---------------|
| Token Bucket | ✅ Yes | ✅ Allows bursts within limits |
| Leaking Bucket | ✅ Yes | ❌ No bursts allowed |
| Fixed Window Counter | ✅ Yes | ✅ Allows bursts at edges |
| Sliding Window Log | ❌ No | ❌ No bursts allowed |
| Sliding Window Counter | ✅ Yes | ✅ Smooths out bursts |

----
