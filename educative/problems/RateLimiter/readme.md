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
This `README.md` file provides **structured, readable**, and **contextually enriched** information. You can **edit and expand** it further based on your needs. Let me know if you'd like refinements! 🚀
