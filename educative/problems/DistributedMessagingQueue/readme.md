# Distributed Messaging Queue

## 📜 System Design: The Distributed Messaging Queue

Learn about the **messaging queue**, why we use it, and important use cases.

---

## 🔄 What is a Messaging Queue?

A **messaging queue** is an intermediate component between the interacting entities known as **producers** and **consumers**.
- The **producer** generates messages and places them in the queue.
- The **consumer** retrieves messages from the queue and processes them.
- Multiple producers and consumers can interact with the queue simultaneously.

**Example:**  
Here is an illustration of two applications interacting via a single messaging queue.

---

## 🎯 Motivation

A **messaging queue** has several advantages and use cases:

### 🚀 Improved Performance
- Enables **asynchronous communication** between producers and consumers.
- Eliminates **relative speed differences** between interacting entities.
- **Reduces client-perceived latency** by separating slower operations from the critical path.

**Example:**  
Instead of waiting for a long-running task to complete, the producer sends a message to the queue and continues operations.  
The consumer processes the message when available and **notifies success or failure** via another queue.

### 🔄 Better Reliability
- **Fault tolerance:** Producers or consumers can fail independently without affecting others.
- **Replication:** Messaging queues can be replicated across multiple servers to ensure availability.

### 📈 Granular Scalability
- **Asynchronous communication** makes the system more scalable.
- **Workload distribution:** When requests increase, the workload is spread across multiple consumers.
- Applications can **adjust the number of producers or consumers** dynamically.

### 🔗 Easy Decoupling
- **Decouples dependencies** among different entities.
- **Entities communicate via messages** without knowing each other’s internal mechanisms.

### ⚖️ Rate Limiting
- Helps **absorb load spikes** and prevents services from becoming overloaded.
- Acts as a **rudimentary form of rate limiting** to avoid dropping incoming requests.

### 🎭 Priority Queue
- Multiple queues can be used to **implement different priorities**.
- **Example:** Assigning more service time to a **higher-priority queue**.

---

## 🛠️ Messaging Queue Use Cases

A **messaging queue** has various applications in both **single-server** and **distributed environments**.

### 📧 Sending Many Emails
- Used for **account verification, password resets, marketing campaigns**, etc.
- Emails don’t require **immediate processing**, preventing disruption to core system functionality.
- A **messaging queue** helps coordinate large email volumes efficiently.

### 🎥 Data Post-Processing
- Multimedia applications process content for different devices (e.g., **mobile phones, smart TVs**).
- Content is **uploaded to storage**, and a **messaging queue schedules post-processing**.
- **Reduces client-perceived latency** and schedules tasks during off-peak hours.

### 🔍 Recommender Systems
- Platforms use **recommender systems** to provide personalized content.
- The system **processes user history** and predicts relevant content.
- Since this is **time-consuming**, a **messaging queue** improves performance.

---

## 🏗️ How Do We Design a Distributed Messaging Queue?

The design is divided into **five lessons**:

### 📌 Requirements
- Focuses on **functional and non-functional requirements**.
- Discusses **single-server messaging queues** and their drawbacks.

### ⚙️ Design Considerations
- Covers **message ordering, extraction, visibility**, and **concurrency**.

### 🏗️ Design
- Explains **queue replication** and **interaction between components**.

### 📊 Evaluation
- Evaluates the **design based on functional and non-functional requirements**.

### 🎯 Quiz
- Tests understanding of **distributed messaging queue design**.

---

## 🔚 Conclusion

A **distributed messaging queue** enhances **performance, reliability, scalability, and decoupling**.  
It is widely used in **email processing, multimedia post-processing, recommender systems**, and more.

## 📜 Requirements of a Distributed Messaging Queue’s Design

Learn about the **requirements** of designing a distributed messaging queue using a strawman solution.

---

## 🔍 Functional Requirements

A **distributed messaging queue** should support the following actions:

- **Queue Creation** – Clients should be able to create a queue and set parameters like **queue name, queue size, and maximum message size**.
- **Send Message** – Producer entities should be able to send messages to a queue.
- **Receive Message** – Consumer entities should be able to retrieve messages from their respective queues.
- **Delete Message** – Consumers should be able to **delete messages** after successful processing.
- **Queue Deletion** – Clients should be able to **delete specific queues** when needed.

---

## ⚙️ Non-Functional Requirements

The system should adhere to the following **non-functional requirements**:

- **Durability** – Data should be **persistent** and not lost due to failures.
- **Scalability** – The system should **handle increased load** dynamically.
- **Availability** – The queue should be **highly available**, even during failures.
- **Performance** – The system should provide **high throughput and low latency**.

---

## 🏗️ Single-Server Messaging Queue

Before designing a **distributed messaging queue**, we must understand how **single-server queues** work.

- A **single-server queue** allows producers and consumers to interact **on the same node**.
- A **locking mechanism** ensures data consistency by allowing only **one entity** (producer or consumer) to access the queue at a time.

However, **single-server queues have drawbacks**:
- **High Latency** – Lock contention slows down access.
- **Low Availability** – If the server fails, the queue becomes **inaccessible**.
- **Lack of Durability** – Data may be lost due to **lack of replication**.
- **Limited Scalability** – Cannot handle **large numbers of messages, producers, or consumers**.

To extend this design to a **distributed messaging queue**, we must **eliminate these drawbacks**.

---

## 🏗️ Building Blocks of a Distributed Messaging Queue

A **distributed messaging queue** relies on the following **key components**:

- **Database** – Stores metadata of queues and users.
- **Cache** – Keeps frequently accessed data for **faster retrieval**.
- **Load Balancer** – Directs incoming requests to the appropriate servers.

These components ensure **scalability, durability, and availability**.

---

## 🤔 Point to Ponder

**Can we extend the design of a single-server messaging queue to a distributed messaging queue?**

A **single-server queue** has several limitations, including **high latency, low availability, lack of durability, and poor scalability**.  
To build a **distributed messaging queue**, we must **overcome these challenges**.

## 📜 System Design: The Distributed Messaging Queue

Learn about the **messaging queue**, why we use it, and important use cases.

---

## 🔄 What is a Messaging Queue?

A **messaging queue** is an intermediate component between the interacting entities known as **producers** and **consumers**.
- The **producer** generates messages and places them in the queue.
- The **consumer** retrieves messages from the queue and processes them.
- Multiple producers and consumers can interact with the queue simultaneously.

**Example:**  
Here is an illustration of two applications interacting via a single messaging queue.

---

## 🎯 Motivation

A **messaging queue** has several advantages and use cases:

### 🚀 Improved Performance
- Enables **asynchronous communication** between producers and consumers.
- Eliminates **relative speed differences** between interacting entities.
- **Reduces client-perceived latency** by separating slower operations from the critical path.

**Example:**  
Instead of waiting for a long-running task to complete, the producer sends a message to the queue and continues operations.  
The consumer processes the message when available and **notifies success or failure** via another queue.

### 🔄 Better Reliability
- **Fault tolerance:** Producers or consumers can fail independently without affecting others.
- **Replication:** Messaging queues can be replicated across multiple servers to ensure availability.

### 📈 Granular Scalability
- **Asynchronous communication** makes the system more scalable.
- **Workload distribution:** When requests increase, the workload is spread across multiple consumers.
- Applications can **adjust the number of producers or consumers** dynamically.

### 🔗 Easy Decoupling
- **Decouples dependencies** among different entities.
- **Entities communicate via messages** without knowing each other’s internal mechanisms.

### ⚖️ Rate Limiting
- Helps **absorb load spikes** and prevents services from becoming overloaded.
- Acts as a **rudimentary form of rate limiting** to avoid dropping incoming requests.

### 🎭 Priority Queue
- Multiple queues can be used to **implement different priorities**.
- **Example:** Assigning more service time to a **higher-priority queue**.

---

## 🛠️ Messaging Queue Use Cases

A **messaging queue** has various applications in both **single-server** and **distributed environments**.

### 📧 Sending Many Emails
- Used for **account verification, password resets, marketing campaigns**, etc.
- Emails don’t require **immediate processing**, preventing disruption to core system functionality.
- A **messaging queue** helps coordinate large email volumes efficiently.

### 🎥 Data Post-Processing
- Multimedia applications process content for different devices (e.g., **mobile phones, smart TVs**).
- Content is **uploaded to storage**, and a **messaging queue schedules post-processing**.
- **Reduces client-perceived latency** and schedules tasks during off-peak hours.

### 🔍 Recommender Systems
- Platforms use **recommender systems** to provide personalized content.
- The system **processes user history** and predicts relevant content.
- Since this is **time-consuming**, a **messaging queue** improves performance.

---

## 🏗️ How Do We Design a Distributed Messaging Queue?

The design is divided into **five lessons**:

### 📌 Requirements
- Focuses on **functional and non-functional requirements**.
- Discusses **single-server messaging queues** and their drawbacks.

### ⚙️ Design Considerations
- Covers **message ordering, extraction, visibility**, and **concurrency**.

### 🏗️ Design
- Explains **queue replication** and **interaction between components**.

### 📊 Evaluation
- Evaluates the **design based on functional and non-functional requirements**.

### 🎯 Quiz
- Tests understanding of **distributed messaging queue design**.

---

## 🔚 Conclusion

A **distributed messaging queue** enhances **performance, reliability, scalability, and decoupling**.  
It is widely used in **email processing, multimedia post-processing, recommender systems**, and more.

## 📜 Considerations of a Distributed Messaging Queue’s Design

Learn about the **factors that affect the design** of a messaging queue.

---

## 🔄 Overview

Before designing a **distributed messaging queue**, we must consider several key factors that significantly impact its design:
- **Ordering of messages**
- **Effect of ordering on performance**
- **Management of concurrent access to the queue**

Each of these factors is discussed in detail below.

---

## 📌 Ordering of Messages

A **messaging queue** receives messages from producers, which are then consumed by consumers at their own pace.  
Some operations require **strict ordering**, while others can tolerate **some reordering**.

### **Examples**
- **Strict Ordering:** Chat applications must deliver messages in order to avoid confusion.
- **Flexible Ordering:** Emails from different users do not require strict sequencing.

---

## 🎯 Types of Message Ordering

### 🔹 Best-Effort Ordering
- Messages are placed in the queue **in the order they are received**, not necessarily in the order they were sent.
- **Example:** Due to network congestion, message **B** may arrive after message **D**, altering the expected sequence.

### 🔹 Strict Ordering
- Messages are placed in the queue **in the exact order they were produced**.
- Requires a mechanism to **identify the original order**, such as **timestamps or sequence numbers**.

---

## 🏗️ Approaches to Ordering Messages

### 🔢 Monotonically Increasing Numbers
- Assigns **incremental numbers** to messages on the server side.
- **Drawbacks:**
    - Acts as a **bottleneck** during high request bursts.
    - Does not guarantee correct ordering when messages arrive out of sequence.

### 🔄 Causality-Based Sorting
- Sorts messages based on **timestamps generated at the client side**.
- **Drawback:** Cannot determine the absolute order across multiple client sessions.

### ⏳ Synchronized Clocks
- Uses **globally synchronized timestamps** to ensure correct sequencing.
- **Advantages:**
    - Provides **unique identifiers** for each message.
    - Helps detect **delayed messages**.

---

## 📊 Sorting Messages

Once messages arrive at the server, they must be **sorted based on timestamps** using an **online sorting algorithm**.

### **Handling Delayed Messages**
- If a message arrives **late due to network delay**, the queue must be **reordered**.
- If newer messages have already been handed out, the delayed message is placed in a **special queue** for client-side handling.

---

## ⚡ Effect on Performance

### **FIFO Operations**
- A queue is designed for **First-In, First-Out (FIFO)** processing.
- However, maintaining **strict order** in distributed systems is challenging.

### **Trade-offs**
- **Monotonically increasing identifiers** provide **high throughput** but require **online sorting**.
- **Online sorting introduces latency**, so a **time-window approach** is used to minimize delays.

---

## 🔄 Managing Concurrency

### **Concurrency Challenges**
- Multiple messages may arrive **at the same time**.
- Multiple consumers may request messages **simultaneously**.

### **Solutions**
- **Locking Mechanism:** Ensures exclusive access but **reduces scalability**.
- **Serialized Requests:** Uses a **buffered queue** to maintain order **without locking**.
- **Multiple Queues:** Dedicated producers and consumers **reduce ordering costs** but increase complexity.

---

## 🏁 Conclusion

In this lesson, we explored key considerations in **distributed messaging queue design**, including:
- **Message ordering techniques**
- **Performance trade-offs**
- **Concurrency management strategies**


## 📜 Design of a Distributed Messaging Queue: Part 1

Learn about the **high-level design** of a messaging queue and how to scale the metadata of queues.

---

## 🔄 Overview

So far, we’ve discussed the **requirements and design considerations** of a distributed messaging queue.  
Now, let’s begin with learning about the **high-level design** of a distributed messaging queue.

---

## 🌐 Distributed Messaging Queue

Unlike a **single-server messaging queue**, a **distributed messaging queue** resides on **multiple servers**.  
A distributed messaging queue has its own **challenges**. However, it **resolves the drawbacks** of a single-server messaging queue **if designed properly**.

The following sections focus on the **scalability, availability, and durability** issues of designing a distributed messaging queue by introducing a **fault-tolerant architecture**.

---

## 🏗️ High-Level Design Assumptions

Before diving deep into the design, let’s assume the following points to make the discussion **simpler and easier to understand**:

- **Queue data is replicated** using either a **primary-secondary** or **quorum-like system** inside a cluster.
- **Data partitioning** is used if the queue **gets too long** to fit on a server.
- A **consistent hashing-like scheme** or **key-value store** is used for partitioning.
- The system can **auto-expand and auto-shrink** resources as needed.

These assumptions help **eliminate the problems** in a **single-server solution**.

---

## 🏗️ High-Level Architecture Components

The following figure demonstrates a **high-level design** of a distributed messaging queue composed of several components:

### **🔀 Load Balancer**
- Receives requests from **producers and consumers**.
- Forwards requests to **front-end servers**.
- Consists of **multiple load balancers** to ensure **minimal latency** and **high availability**.

### **🖥️ Front-End Service**
The **front-end service** consists of **stateless machines** distributed across **data centers**.  
It provides the following services:

- **Request Validation** – Ensures requests contain all necessary information.
- **Authentication & Authorization** – Verifies user identity and access permissions.
- **Caching** – Stores frequently used **queue metadata** and **user-related data**.
- **Request Dispatching** – Calls **back-end** and **metadata store** services.
- **Request Deduplication** – Prevents **duplicate requests** from being placed in a queue.
- **Usage Data Collection** – Gathers **real-time data** for auditing purposes.

### **📂 Metadata Service**
- Stores, retrieves, and updates **queue metadata** in the **metadata store and cache**.
- Acts as a **middleware** between **front-end servers** and the **data layer**.
- Uses **cache-first retrieval** to improve performance.

### **🗄️ Metadata Cluster Organization**
There are **two approaches** to organizing metadata cache clusters:

1. **Small Metadata Approach**
    - Metadata is **replicated** on each cluster server.
    - Requests can be served from **any random server**.
    - A **load balancer** can be introduced between **front-end servers** and **metadata services**.

2. **Large Metadata Approach**
    - Uses **sharding** to divide data into **different shards**.
    - Each shard is **stored and replicated** across multiple hosts.
    - The **front-end server** maintains a **mapping table** to direct requests.

---

## 🔚 Conclusion

In this lesson, we explored the **high-level design** of a **distributed messaging queue**, including:
- **Front-end servers** and their role in request handling.
- **Load balancers** for efficient request distribution.
- **Metadata services** and their organization.


## 📜 Design of a Distributed Messaging Queue: Part 2

Learn about the **detailed design** of a messaging queue and its management at the back-end servers.

---

## 🔄 Overview

In the previous lesson, we discussed the **responsibilities of front-end servers and metadata services**.  
Now, we’ll focus on the **core part of the design** where the queues and messages are stored: the **back-end service**.

---

## 🏗️ Back-End Service

The **back-end service** is the **heart of the architecture**, where major activities take place.  
When the **front-end receives a message**, it refers to the **metadata service** to determine the **host** where the message needs to be sent.  
The message is then **forwarded to the host** and **replicated** on relevant hosts to ensure **availability**.

### **Message Replication Models**
Message replication in a cluster can be performed using one of the following models:
1. **Primary-Secondary Model**
2. **Cluster of Independent Hosts**

Before diving into these models, let’s first discuss the **two types of cluster managers** responsible for queue management.

---

## 🏢 Internal vs. External Cluster Managers

Cluster managers help in **queue assignment and management**.  
The differences between **internal** and **external** cluster managers are:

| Feature | Internal Cluster Manager | External Cluster Manager |
|---------|-------------------------|-------------------------|
| **Queue Assignment** | Manages queues **within a cluster** | Manages queues **across clusters** |
| **Node Awareness** | Knows about **every node** in a cluster | Knows about **each cluster**, but not individual hosts |
| **Health Monitoring** | Listens to **heartbeat signals** from nodes | Monitors **cluster health** |
| **Failure Handling** | Manages **host failures, instance additions, and removals** | Manages **cluster utilization** |
| **Queue Partitioning** | Splits a queue into **several parts**, each with a **primary server** | May distribute a queue **across multiple clusters** |

---

## 🔄 Primary-Secondary Model

In the **primary-secondary model**, each node acts as a **primary host** for a collection of queues.  
The **primary host** is responsible for:
- **Receiving requests** for a queue.
- **Managing data replication** across secondary hosts.
- **Deleting messages** upon successful processing.

### **Example Scenario**
Consider **two queues (101 and 102)** stored on **four hosts (A, B, C, D)**:
- **Queue 101** → **Primary Host: B**, **Secondary Hosts: A, C**
- **Queue 102** → **Primary Host: D**, **Secondary Hosts: B, C**

When a **message request** arrives, the **front-end server** identifies the **primary host** via the **metadata service**.  
The **primary host** retrieves the message, processes it, and **removes all replicas**.

---

## 🏢 Cluster of Independent Hosts

In this approach, multiple **independent hosts** are distributed across **data centers**.  
When the **front-end receives a message**, it determines the **corresponding cluster** via the **metadata service**.  
The message is then **forwarded to a random host**, which **replicates it** across other hosts storing the queue.

### **Point to Ponder**
**How does a random host replicate messages across other hosts in the same cluster?**  
Each host maintains a **mapping table** between queues and hosts, making replication easier.

### **Example Scenario**
Consider **Cluster Y** with **hosts A, B, and C**, storing **queues 101 and 103**:
- **Queue 101** → **Stored on Hosts A, C**
- **Queue 103** → **Stored on Hosts B, A**

If **Host C** receives a message for **Queue 103**, it **replicates the message** on **Hosts A and B**.

---

## 🔄 Message Replication Strategies

There are **two ways** to replicate messages across hosts:

### **🔁 Synchronous Replication**
- The **primary host** replicates the message across **all secondary hosts**.
- After receiving **acknowledgment**, the **primary host notifies the client**.
- **Pros:** Ensures **message consistency** across replicas.
- **Cons:** **Higher latency** and **temporary unavailability** during primary host election.

### **⚡ Asynchronous Replication**
- The **primary host acknowledges the client** immediately.
- **Replication occurs afterward** on secondary hosts.
- **Pros:** **Lower latency** and **faster processing**.
- **Cons:** **Replication lag** and **potential consistency issues**.

**Choosing between synchronous and asynchronous replication depends on application needs.**

---

## 🔚 Conclusion

In this lesson, we explored:
- **Back-end server organization** in a distributed messaging queue.
- **Primary-secondary model** vs. **cluster of independent hosts**.
- **Internal vs. external cluster managers**.
- **Synchronous vs. asynchronous replication**.

In the next lesson, we’ll evaluate how our system meets **functional and non-functional requirements**.

## 📜 Evaluation of a Distributed Messaging Queue’s Design

Analyze whether the **proposed system** meets the **functional and non-functional requirements** of a distributed messaging queue.

---

## 🔄 Functional Requirements

### 🏗️ Queue Creation and Deletion
- When a request for a queue is received at the **front-end**, the queue is created with all necessary details after undergoing **essential checks**.
- The **cluster manager** assigns servers to the newly created queue and updates the **metadata stores and caches**.
- Similarly, when a queue is **deleted**, the cluster manager **deallocates space** and removes data from all metadata stores and caches.

### ❓ Point to Ponder
**How do we handle messages that can’t be processed after maximum attempts?**  
A **dead-letter queue** is used to store messages that:
- Were intended for a **deleted queue**.
- Exceeded the **queue length limit** (rare in our design).
- **Expired** due to per-message **time-to-live (TTL)**.

A **dead-letter queue** helps **identify faults** and determine the **cause of failure**.

---

## 📩 Sending and Receiving Messages
- **Producers** deliver messages to specific queues once they are created.
- At the **back-end**, messages are **sorted based on timestamps** to preserve order.
- **Consumers** retrieve messages from specified queues.

### 🔄 Message Flow
1. The **front-end** identifies the **primary host or cluster** where the queue resides.
2. The request is **forwarded** to the corresponding entity.
3. The message is **placed in the queue** for retrieval.

---

## 🗑️ Message Deletion
Two approaches exist for **message deletion**:

### **1️⃣ Consumer-Tracked Deletion**
- Messages are **not deleted immediately** after consumption.
- The **consumer keeps track** of consumed messages.
- A **job deletes messages** when expiration conditions are met.
- **Example:** Apache Kafka uses this approach, allowing multiple processes to consume a message.

### **2️⃣ Visibility Timeout**
- Messages are **not deleted immediately** but are **made invisible** for a set duration.
- Other consumers **cannot access** the message during this time.
- The message is **deleted via an API call** after processing.

### ❓ Point to Ponder
**What happens if the visibility timeout expires while the consumer is still processing the message?**
- The message **becomes visible again**, allowing another worker to **process it**.
- To **avoid duplication**, applications must **set a safe threshold** for visibility timeout.

---

## ⚙️ Non-Functional Requirements

### 🔒 Durability
- **Metadata replication** ensures queue persistence across **multiple nodes**.
- **Message replication** prevents data loss if a node **fails**.

### 📈 Scalability
- **Horizontally scalable components** (front-end servers, metadata servers, caches, back-end clusters).
- **Queue expansion** when message count **exceeds 80%** of capacity.
- **Queue shrinking** when message count **drops below a threshold**.
- **Cluster manager adds extra servers** when the number of queues increases.

### 🔄 Availability
- **Metadata and messages** are replicated **inside and outside data centers**.
- **Load balancer** routes traffic around **failed nodes**.

### ⚡ Performance
- **Caches, replication, and partitioning** reduce **data read/write time**.
- **Best-effort ordering** increases **throughput** and **lowers latency**.
- **Time-window sorting** minimizes **latency** in strict ordering scenarios.

---

## ⚖️ Trade-offs in Distributed Messaging Queues
- **Strict ordering vs. throughput** – Enforcing strict order **reduces performance**.
- **Relaxed ordering** improves **throughput and latency**.
- **Replication and partitioning** help **scale data** but introduce **complexity**.

---

## 🔚 Conclusion
We explored the **evaluation of a distributed messaging queue**, covering:
- **Functional requirements** (queue creation, message handling, deletion).
- **Non-functional requirements** (durability, scalability, availability, performance).
- **Trade-offs** between **ordering, throughput, and latency**.

