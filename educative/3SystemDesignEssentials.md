# System Design Essentials

## 🚀 Introduction to Modern System Design
Get an overview of the topics we’ll cover in this module.

### 📌 What is system design?
System design is the process of defining components and their integration, APIs, and data models to build **large-scale systems** that meet a specified set of **functional and non-functional requirements**.

System design uses the concepts of:
- **Computer networking**
- **Parallel computing**
- **Distributed systems** to craft systems that **scale well** and are **performant**.

However, distributed systems are inherently complex. The discipline of **system design** helps us **tame this complexity** and get the work done.

### 🔍 Key Goals of System Design
System design aims to build systems that are:
- **Reliable**: Handle faults, failures, and errors.
- **Effective**: Meet all user needs and business requirements.
- **Maintainable**: Flexible and easy to scale up or down. The ability to add new features also comes under maintainability.

## 🏗️ Modern System Design Using Building Blocks
We have separated commonly used design elements, such as **load balancers**, as **basic building blocks** for **high-level system design**. This serves two purposes:
1. **Detailed discussions** on building blocks and their **mini-design challenges**.
2. **Focus on problem-specific aspects**, mentioning the building block we’ll use and **how** we’ll use it.

We have identified **sixteen** critical building blocks in **modern system design**.

## 📚 About This Module
This module focuses on designing systems that:
- **Scale** with increasing users.
- Remain **available** under various fault conditions.
- Meet **functional goals** with **good performance**.

### 🌀 Iterative Process of System Design
Real-world system building is an **iterative process**. We start with a **reasonably good design**, measure **performance**, and improve the design in the **next iteration**.

## 🎯 A Fresh Look at System Design
Many system design courses offer **a formulaic approach**, which might seem attractive for an interview but **fails to instill true understanding**. System design is as much **an art as a science**, and **approaching it from first principles** gives a **fresh perspective**.

## 🌍 Going Deep & Broad
We address both **traditional and novel design problems** touching on aspects such as:
- **Scalability**
- **Availability**
- **Maintainability**
- **Consistency**
- **Fault-tolerance**

### 🔄 Handling Complexity with Assumptions
Real systems are **complex**, and often we must **make appropriate assumptions** to scope a problem effectively.

## 🧠 Interactive Learning Experience
We offer **ample opportunities** for hands-on experience with **system design**:
- **Guided steps** to design systems.
- **End-to-end system design challenges**.
- **Testing concepts through quizzes**.

---

## 📜 Consistency Models

In this lesson, we will explore the different forms of consistency in distributed systems.

### 🔹 CAP Theorem & Consistency
According to the **CAP Theorem**, consistency ensures that every **successful read request returns the most recent write**. However, there are multiple forms of consistency beyond this basic definition.

### 🏗️ Consistency Model Definition
A **consistency model** defines the valid execution histories of a system. In layperson's terms, it specifies the possible behaviors in a **distributed system**.

### 🎯 Importance of Consistency Models
Consistency models serve crucial purposes:
- **Formalizing behaviors** of distributed systems.
- **Guaranteeing safe operations** for software engineers using distributed databases.
- **Providing abstraction**, allowing engineers to treat systems as reliable black boxes.

---

## 📌 Types of Consistency Models

### ⚖️ Strong Consistency Model
A **stronger consistency model** allows fewer histories and **imposes more restrictions** on system behavior. The stricter the model, the **easier** it is to develop applications with reliable guarantees.

### 🔄 Linearizability
A **linearizable system** ensures that operations appear **instantaneous** to an external client:
- If a client **writes a value**, all other clients must see the updated value immediately.
- In **distributed systems**, achieving linearizability is **challenging** due to **asynchronous replication**.

**Example:**
- **Centralized system**: Linearizability is simple.
- **Distributed system**: If a client reads a value before replication completes, it may receive **stale data**.

**Trade-offs:**
- **Synchronous replication** ensures linearizability but **increases latency**.
- Consider the **PACELC theorem**, which highlights the trade-off between **latency** and **consistency**.

### 📏 Sequential Consistency
In **sequential consistency**, operations may **take effect** before their invocation or after completion, but:
- **Ordering of operations must be preserved** globally across all clients.
- **Individual client operations remain sequential**.

**Example:**
In a **social network**, posts from different users can appear **out of order**, but an individual user’s posts must be **displayed sequentially**.

### 🔗 Causal Consistency
**Causal consistency** allows operations to be seen in **different orders** between clients, but **causally dependent actions** must follow the correct sequence.

**Example:**
- **A comment on a post must appear after the post itself**.
- **Replies to comments must maintain logical ordering**, even if general post order varies.

### ⏳ Eventual Consistency
**Eventual consistency** guarantees that if no new writes occur, **all replicas will eventually converge** to the same state.

**Example:**
- **A write request updates Node A**.
- **A read request on Node B may return stale data**.
- Once replication **completes**, all nodes hold the latest value.

---

## 📌 Summary

Different consistency models provide varying levels of guarantees:
- **Linearizability:** Strong but costly.
- **Sequential consistency:** Preserves individual client order.
- **Causal consistency:** Maintains dependencies.
- **Eventual consistency:** Weakest, but ensures eventual correctness.

## ⚡ Spectrum of Failure Models

Failures in **distributed systems** vary in complexity. This section explores different failure models and their impact.

### 🛠️ Understanding Failures
Failures in distributed systems can:
- **Appear intermittently** or **persist for long periods**.
- **Disrupt communication** between nodes.
- **Affect system performance** significantly.

### 🏗️ Purpose of Failure Models
Failure models offer a framework to:
- **Understand different types of failures**.
- **Evaluate possible recovery strategies**.
- **Optimize system reliability** based on expected risks.

---

## 📊 Types of Failure Models

### ✅ Fail-stop Failure
In a **fail-stop failure**, a node **halts permanently**, but other nodes **can detect its absence** by communicating with it.

**Key Takeaways:**
- **Simplest failure type** for engineers to manage.
- **Explicit detection mechanisms** available.

### 🚨 Crash Failure
A **crash failure** occurs when a node halts **silently**—other nodes **cannot detect** its failure.

**Challenges:**
- **No clear failure indication**.
- **Requires advanced monitoring** to detect crashes.

### 🔄 Omission Failure
An **omission failure** occurs when a node fails to **send or receive messages**.

**Types:**
- **Send omission failure** – Node fails to respond to incoming requests.
- **Receive omission failure** – Node fails to acknowledge a request.

### ⏳ Temporal Failure
A **temporal failure** happens when a node produces **correct results**, but **too late** to be useful.

**Causes:**
- **Bad algorithms** leading to delays.
- **Poor system design** affecting performance.
- **Loss of synchronization** between processor clocks.

### 🔥 Byzantine Failure
A **Byzantine failure** is the most challenging type, where nodes exhibit **random behavior**, such as:
- **Sending arbitrary messages** unpredictably.
- **Generating incorrect results**.
- **Stopping halfway through processing**.

**Causes:**
- **Software bugs** introducing corruption.
- **Malicious attacks** disrupting operations.

Byzantine failures are **the hardest to handle** due to their unpredictable nature.

---

## 🚀 Availability

Learn about **availability**, how to **measure** it, and its **importance**.

### 📖 What is Availability?
**Availability** is the **percentage of time** a **service or infrastructure** is accessible to clients and operates under **normal conditions**.

For example:
- A **100% available** service functions and **responds as intended** all the time.

### 📏 Measuring Availability
**Mathematically,** availability (**A**) is a ratio, calculated as:

`A (in percent) = [(Total Time - Downtime) / Total Time] * 100`


- **Higher A values** indicate **better availability**.

### 🔢 The Nines of Availability
Availability is often measured in **nines**, where **each additional nine** represents **less downtime**:

| **Availability %** | **Downtime per Year** | **Downtime per Month** | **Downtime per Week** |
|------------------|------------------|------------------|------------------|
| **90% (1 nine)** | **36.5 days** | **72 hours** | **16.8 hours** |
| **99% (2 nines)** | **3.65 days** | **7.20 hours** | **1.68 hours** |
| **99.9% (3 nines)** | **8.76 hours** | **43.8 minutes** | **10.1 minutes** |
| **99.99% (4 nines)** | **52.56 minutes** | **4.32 minutes** | **1.01 minutes** |
| **99.999% (5 nines)** | **5.26 minutes** | **25.9 seconds** | **6.05 seconds** |
| **99.9999% (6 nines)** | **31.5 seconds** | **2.59 seconds** | **0.605 seconds** |

### 🛠️ Availability and Service Providers
Each service provider may **measure availability** differently:
- Some **start tracking** availability when the service **launches**.
- Some **measure availability** from when a **specific client starts using the service**.
- Some **exclude planned downtimes** or **cyberattack-related outages** from calculations.

### ⚠️ Key Considerations
When assessing **availability data**, it’s **important to**:
- **Understand how a provider calculates** availability.
- **Check if reported availability excludes** planned maintenance or external disruptions.

---

Here’s a well-structured **README.md** version of the extracted content with **meaningful icons**, **bold highlights**, and organized sections using level two headings:

## 🔄 Reliability

Learn about **reliability**, how to **measure** it, and its **importance**.

### 🏗️ What is Reliability?
**Reliability (R)** is the **probability** that a service performs its functions for a **specified time** under varying operating conditions.

To measure **R**, two key metrics are used:
- **Mean Time Between Failures (MTBF)**:
  ```
    MTBF = (Total Elapsed Time - Sum of Downtime) / Total Number of Failures
  ```
- **Mean Time to Repair (MTTR)**:
  ```
    MTTR = Total Maintenance Time / Total Number of Repairs
  ```

A **higher MTBF** and **lower MTTR** indicate **better reliability**.

---

## ⏳ Reliability vs. Availability

Both **reliability and availability** are crucial for ensuring a service meets its **service level objectives (SLOs)**.

| **Metric**   | **Definition** |
|-------------|---------------|
| **Reliability (R)** | Measures how well a service functions over time. |
| **Availability (A)** | Measures the **percentage of time** a system is **accessible**. |

**Key Observations:**
- **Availability (A)** is a **function of Reliability (R)**.
- **R** can fluctuate **independently**, while **A** depends on **R**.
- Possible scenarios:
  - **Low A, Low R** ❌
  - **Low A, High R** ⚠️
  - **High A, Low R** ⚠️
  - **High A, High R** ✅ *(Desirable)*

### 📌 Understanding Failures
There are variations of **MTBF**, such as **Mean Time to Failure (MTTF)**:
- **MTTF** applies when a failed component **cannot be repaired** and requires **replacement**.
- **Examples**:
  - A **bad disk** needs replacement.
  - A **failed bulb** is irreparable.

---

## 💡 Real-World Examples

### 🏗️ Reliability in Systems
**Example 1**: A system might be **90% available** but **only 80% reliable** due to frequent minor failures.

**Example 2**: Imagine a **data center**:
- A **network failure** disrupts external traffic.
- Internal components **function correctly** (100% reliability).
- However, **external clients experience 0% availability**.

### 🛠️ Industry Practices
Different industries focus on either:
- **Reliability (R)** – Used in **hardware metrics**, like **storage disks (MTTF)**.
- **Availability (A)** – Used in **online services**, like **uptime in SLAs**.

**Example**: Amazon EC2 guarantees **99.95% uptime** in their SLA.

---

By understanding reliability and availability, engineers can **design resilient systems**, reduce **downtime**, and **optimize performance**. 🚀


## 🚀 Scalability

Learn about **scalability** and its **importance in system design**.

### 📖 What is Scalability?
**Scalability** is a system’s ability to **handle increasing workloads** while maintaining **performance efficiency**.

For example:
- A **search engine** must accommodate **growing numbers of users** and index **more data**.
- Various workloads can impact scalability, including:
    - **Request workload** – Number of requests served by the system.
    - **Data/storage workload** – Amount of data stored.

---

## 📏 Dimensions of Scalability

### 📌 Size Scalability
A system is **size scalable** if we can **add more users and resources** to it **without affecting performance**.

### 🔗 Administrative Scalability
This defines the **capacity for multiple organizations or users** to share a **single distributed system smoothly**.

### 🌍 Geographical Scalability
A system that can operate **efficiently across different regions** while **maintaining acceptable performance constraints** is geographically scalable.

---

## ⚖️ Approaches to Scalability

There are two main approaches:

### ⬆️ Vertical Scalability (Scaling Up)
**Vertical scaling** refers to **enhancing existing hardware or software** by increasing:
- **CPU power**
- **RAM**
- **Storage capacity**

**Limitations**:
- Growth is **bounded by server limitations**.
- **Higher costs** due to exotic components required for scaling.

### ⬆️ Horizontal Scalability (Scaling Out)
**Horizontal scaling** means **adding more machines** to the network.
- Uses **commodity nodes** with better **cost benefits**.
- Requires **distributed architecture** so multiple nodes work together as a **single unit**.

| **Vertical Scaling** | **Horizontal Scaling** |
|-----------------|----------------|
| Scaling **up** existing systems | Scaling **out** by adding more nodes |
| **Costly** due to expensive components | **Cheaper**, leveraging commodity nodes |
| **Limited by hardware capacity** | **Flexible**, can scale indefinitely |
| **Simpler implementation** | **Requires distributed coordination** |

---

## 📌 Summary

Different scalability approaches have **trade-offs**, and the best approach depends on system needs:

- **Size Scalability** ensures **growth in users & resources**.
- **Administrative Scalability** helps **large-scale organizations** share services.
- **Geographical Scalability** ensures **global performance**.
- **Vertical Scaling** offers **hardware upgrades** but is **costly**.
- **Horizontal Scaling** provides **flexibility** but requires **distributed computing strategies**.

Choosing the right scalability approach ensures **efficient system performance** even as demands **grow over time**. 🚀

## 🛠️ Maintainability

Understand **maintainability**, how to **measure** it, and its **relationship with reliability**.

### 📖 What is Maintainability?
Beyond building a system, one of the **key tasks** is ensuring it remains **operational** over time. Maintainability involves:
- **Finding and fixing bugs**.
- **Adding new functionalities**.
- **Keeping the system platform updated**.
- **Ensuring smooth operations**.

A well-designed system should be **highly maintainable** to minimize downtime and support future modifications.

### 🔎 Core Aspects of Maintainability
Maintainability can be categorized into three aspects:

- **⚙️ Operability** – The ease with which the system can be maintained under **normal conditions** and after **fault recovery**.
- **🧩 Lucidity** – Simplicity of the code base. **Clearer code** makes maintenance **easier** and **efficient**.
- **🔄 Modifiability** – The ability of the system to **seamlessly integrate** new features and modifications **without disruptions**.

---

## 📏 Measuring Maintainability

Maintainability (**M**) represents the **probability** that a system restores its functionality within a given timeframe.

For example:
- A component with a **maintainability value of 95% for 30 minutes** means there’s a **95% chance** it will be **fully restored within half an hour** after failure.

### 🔢 Key Metric: Mean Time to Repair (MTTR)
Maintainability is measured using **Mean Time to Repair (MTTR)**:

## ⚙️ Fault Tolerance

Understand **fault tolerance**, its importance, and how to measure it.

### 📖 What is Fault Tolerance?
**Fault tolerance** is a system’s ability to continue operating even if **one or more components fail**. These components may be **hardware or software**.

Since achieving **100% fault tolerance** is impractical, systems implement techniques to **reduce failures** and **ensure high availability**.

### 🔑 Why Fault Tolerance Matters
- **🛡️ Data Safety** – Prevents data loss due to failures.
- **🚀 Availability** – Ensures services remain **accessible 24/7**.
- **🔄 Reliability** – Guarantees proper functioning, taking **correct actions on requests**.

---

## 🔄 Fault Tolerance Techniques

Failures can occur at the **hardware or software level**, impacting data and services. The following techniques help achieve fault tolerance in different system designs.

### 📌 Replication-Based Fault Tolerance
Replication ensures redundancy by **creating multiple copies** of services and data.
- **🖥️ Swapping failed nodes** with healthy ones maintains service uptime.
- **🗄️ Replicated storage** prevents data loss due to failures.

**Challenges with Replication:**
- **Consistency management** – Ensuring **all replicas update simultaneously**.
- **Trade-offs** – Choosing between **strong consistency (synchronous updates)** vs. **eventual consistency (asynchronous updates)**.

### 🔄 Checkpointing
Checkpointing stores the system’s **state periodically**, allowing recovery after failures.

**Types of Checkpointing States:**
- ✅ **Consistent State** – All system processes hold **coherent snapshots** representing a stable execution.
- ❌ **Inconsistent State** – Snapshots across processes **do not align**, leading to errors during recovery.

Example:  
Processes **i, j, and k** exchange messages **m1 and m2**.  
A consistent checkpoint ensures:
1. **Saved updates reflect completed actions**.
2. **No messages are lost in transit**.
3. **Processes align their snapshots to the same global state**.

In contrast, an **inconsistent checkpoint** results in:
- **Missing or conflicting data**.
- **Processes failing to resume properly after recovery**.

---

## 📌 Summary

Fault tolerance ensures systems operate **smoothly despite failures** using:
- **Replication** – Creates redundant copies to replace failed components.
- **Checkpointing** – Saves system state for recovery.
- **Consistency trade-offs** – Balancing between **strong and eventual consistency**.

By implementing fault tolerance strategies, engineers can **enhance reliability, availability, and data protection** in distributed systems. 🚀

Here’s a well-structured **README.md** version of the extracted content with **meaningful icons**, **bold highlights**, and formatted sections using level two headings:

## 🔢 Back-of-the-Envelope Calculations

Understand the **importance of quick estimations** in system design.

### 📖 What Are Back-of-the-Envelope Calculations?
Back-of-the-envelope calculations help **ignore unnecessary details** and focus on **high-level estimates** that influence system design.

These calculations assist in:
- **Estimating resource needs** (e.g., storage or processing power).
- **Analyzing system scalability**.
- **Avoiding flawed design choices** based on unreasonable assumptions.

Example calculations include:
- **Number of concurrent TCP connections** a server can support.
- **Requests per second (RPS)** a server can handle.
- **Storage requirements for a large-scale system**.

---

## 🏗️ Types of Data Center Servers

Data centers host **multiple types of servers** to manage different workloads efficiently.

### 🖥️ Web Servers
Web servers act as the **first point of contact** after load balancers. These servers handle **API requests** from clients.

- **Computational resources** – High
- **Memory & storage needs** – Low to medium
- **Example**: Facebook's web server with **32GB RAM**, **500GB storage**, and **custom 16-core processor**.

### 🔧 Application Servers
Application servers run **business logic** and provide **dynamic content** to users.

- **Computational & storage resources** – High
- **Example**: Facebook's application servers with **256GB RAM** and storage of up to **6.5TB** (using rotating disks + flash storage).

### 💾 Storage Servers
Storage servers **manage structured and unstructured data** for large-scale applications.

Examples of storage solutions:
- **Blob storage** for YouTube’s video data.
- **Bigtable** for storing video thumbnails.
- **RDBMS** for metadata like comments, likes, and channels.

Facebook storage servers can house **up to 120TB of data**, enabling **exabyte-scale storage**.

---

## ⏳ Important Latencies

System designers must be aware of **latency numbers** to correctly estimate performance.

| **Component** | **Time (Nanoseconds / Milliseconds)** |
|--------------|-------------------|
| L1 Cache | **0.9 ns** |
| L2 Cache | **2.8 ns** |
| L3 Cache | **12.9 ns** |
| Main Memory | **100 ns** |
| Read 1MB from SSD | **200μs** |
| Disk Seek | **4ms** |
| Sending Packet (SF -> NYC) | **71ms** |

Understanding **latencies** enables better system performance optimization.

---

## 🔄 Requests Estimation

Estimating **requests per second (RPS)** helps design scalable architectures.

Two main types:
- **CPU-bound requests** – Limited by available processing power.
- **Memory-bound requests** – Limited by available RAM.

### 🖥️ CPU-Bound Requests Calculation
Formula:
```
RPS_CPU = (Number of CPU Threads) / (Task Time)
```

Example:
- **72 CPU threads**
- **200ms per request**
```
RPS_CPU = 72 / 0.2s = 360 RPS
```
Thus, **360 requests per second** can be processed.

### 💾 Memory-Bound Requests Calculation
Formula:
```
RPS_memory = (Total RAM / Memory per worker) * (1 / Task Time)
```

Example:
- **240GB RAM**
- **Each worker uses 300MB**
- **50ms per request**
```
RPS_memory = (240GB / 300MB) * (1 / 0.05s) ≈ 16,000 RPS
```
Thus, **16,000 requests per second** can be processed.

Combining both:
- **50% CPU-bound requests**
- **50% memory-bound requests**
```
  Total RPS = (360 / 2) + (16,000 / 2) = 8,180 ≈ 8,000 RPS
```
A system handling **mixed request types** may process up to **8,000 RPS**.

---

## 📌 Summary

Back-of-the-envelope calculations help in **estimating key system parameters**:
- **Types of data center servers** – Web, Application, Storage.
- **Latency considerations** – Crucial for optimizing response times.
- **RPS Estimation** – Helps in system scalability planning.

By leveraging quick estimations, engineers can **avoid flawed designs** and **optimize system performance** effectively. 🚀

Here’s a well-structured **README.md** version of the extracted content with **meaningful icons**, **bold highlights**, and formatted sections using level two headings:


## 📊 Resource Estimation

Understand **resource estimation**, including server, storage, and bandwidth calculations.

### 📖 Introduction
Now that we’ve established the basics, let's apply **back-of-the-envelope calculations** to estimate resources for large-scale services.

We will explore:
- **Estimating the number of servers required**.
- **Calculating storage needs**.
- **Determining bandwidth requirements**.

---

## 🖥️ Estimating the Number of Servers

Let’s assume a **Twitter-like service** with the following:
- **500 million daily active users (DAU)**.
- **Each user makes 20 requests per day**.
- **One commodity server handles 8,000 requests per second (RPS)**.

### 📌 Calculations
1. **Total daily requests**:  
   ```
    Total Requests = DAU × Requests per day
    500M × 20 = 10 Billion requests/day
   ```
2. **Total requests per second**:  
   ```
    Total Requests per Second = Total Requests / Seconds in a Day
    10B / 86,400 = ~115K RPS
   ```
3. **Required servers**:  
   ```
    Number of Servers = Total Requests per Second / RPS per Server
    115K / 8K ≈ 15 servers
   ```

However, **this estimate is highly unrealistic**! Large services need millions of servers due to:
- **Load distribution across multiple layers** (web, application, and storage servers).
- **Redundant hardware ensuring high availability**.
- **Different response times per request type**.

Thus, more refined estimation techniques include:
- **Queuing theory** for precise calculations.
- **Prototyping and monitoring** in real-world scenarios.

---

## 💾 Estimating Storage Requirements

Using Twitter as an example, let’s determine storage needs for new tweets.

### 📌 Assumptions
- **250M DAU**, posting **3 tweets per day**.
- **10% contain images**, **5% contain videos**.
- **Image size = 200 KB**.
- **Video size = 3 MB**.
- **Tweet text & metadata = 250 Bytes**.

### 📊 Storage Calculations
1. **Tweets per day**:
   ```
    250M × 3 = 750M tweets/day
   ```
    2. **Storage for tweet text**:
   ```
    750M × 250B = 187.5 GB/day
   ```
3. **Storage for images**:
   ```
    (750M × 10%) × 200KB = 15 TB/day
   ```
4. **Storage for videos**:
   ```
    (750M × 5%) × 3MB = 112.5 TB/day
   ```
5. **Total storage required**:
   ```
    187.5 GB + 15 TB + 112.5 TB ≈ 128 TB/day
   ```

6. **Annual storage estimation**:
   ```
    128 TB × 365 days = 46.72 PB/year
   ```

This highlights the **massive storage requirements** for services like Twitter, which need **efficient data management**.

---

## 🚀 Bandwidth Estimation

To estimate bandwidth needs, consider **incoming and outgoing data**.

### 📌 Incoming Traffic
Since Twitter **stores 128 TB/day**, the incoming traffic must support:

```
  Bandwidth = (Storage per day × 8 bits per byte) / Total seconds per day
  128 × 10¹² × 8 / 86,400 ≈ 12 Gbps
```

### 📌 Outgoing Traffic
Each user views **50 tweets per day**, and considering **5% videos, 10% images**:

1. **Tweets viewed per second**:
   ```
    (250M × 50) / 86,400 = ~145K tweets/sec
   ```
2. **Bandwidth for tweets**:
   ```
    145K × 250B × 8 = ~0.3 Gbps
   ```
3. **Bandwidth for images**:
   ```
    (145K × 10%) × 200KB × 8 = 23.2 Gbps
   ```
4. **Bandwidth for videos**:
   ```
    (145K × 5%) × 3MB × 8 = 174 Gbps
   ```

### 📈 Total bandwidth required:
```
Incoming: 12 Gbps
Outgoing: 0.3 + 23.2 + 174 = ~197.5 Gbps
Total Bandwidth ≈ 209.5 Gbps
```

Large-scale platforms need **hundreds of Gbps** to sustain user activity.

---

## 📌 Summary

Resource estimation provides a **coarse-grained approach** for system design:
- **Server estimation** considers total user requests but requires finer analysis.
- **Storage requirements** account for user-generated content like tweets, images, and videos.
- **Bandwidth calculations** reveal traffic demands based on daily user interactions.

By leveraging **simplified back-of-the-envelope calculations**, engineers can set **reasonable upper bounds** for system capacity planning! 🚀
