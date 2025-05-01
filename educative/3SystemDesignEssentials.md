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
