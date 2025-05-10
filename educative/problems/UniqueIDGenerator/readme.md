## Unique ID Generator

## 🎯 Overview
**System Design: Sequencer**  
 Understand the basics of designing a sequencer. This page explains how to generate and use unique identifiers to distinguish between the millions of events that occur within distributed systems.

---

## 💡 Motivation
There can be **millions of events** happening per second in a large distributed system. For example, consider scenarios such as:
- **Commenting** on a Facebook post,
- **Sharing** a Tweet,
- **Posting** a picture on Instagram.

These high-frequency events require a robust mechanism to ensure each event is uniquely identifiable.

---

## 🔑 Unique ID Assignment
One effective mechanism is to assign a **globally unique ID** to each event. This not only helps in distinguishing events, but it also serves as a primary key in databases, allowing for easier tracking and debugging across complex systems.

---

## 💾 Limitations of Auto-Increment
Assigning a primary key using the **auto-increment feature** in databases is a common practice. However, this approach typically works for a single database instance and **won’t work for a distributed database** where different nodes operate independently. This highlights the need for alternative approaches in distributed setups.

---

## 🛠️ Distributed Unique ID Generator
In distributed settings, a **unique ID generator** is essential—often acting as the primary key in a horizontally-sharded table. This design ensures that even when multiple nodes generate IDs independently, every event still gets a unique identifier without relying on centralized counters.

---

## 🐞 Debugging and Tracing
A unique ID not only guarantees differentiation between events but also helps in tracking and **debugging**. By following the unique identifier (like a **TraceID**), engineers can trace the flow of an event throughout its lifecycle across various microservices.

---

## 📊 Real-World Example: Canopy
A practical demonstration of this concept is found in **Facebook’s Canopy** system. Canopy uses a **TraceID** to uniquely identify each event as it traverses hundreds of microservices to complete a user request—such as sharing a Facebook post (event A) or uploading a video (event B). This ensures that even in a complex, distributed environment, every event remains traceable.

---

## 🔀 Sequencer Design Lessons
The overall design is divided into two lessons:
- **Design of a Unique ID Generator:** Covers three approaches: using **UUIDs**, employing a **database-based method**, and implementing a **range handler**.
- **Unique IDs with Causality:** Focuses on integrating time factors into ID generation to maintain the causality of events.

---

## 🚀 Next Steps
While **unique IDs** are crucial for identifying events and objects in a distributed system, their design presents challenges. The next phase involves exploring the requirements and designing a distributed unique ID generation system, building on the foundational concepts discussed here.

---



Feel free to modify this **README.md** as needed!

## 🎯 Overview
**Design of a Unique ID Generator**  
Learn how to design a system that generates a unique ID. In this lesson, we explore why unique identifiers are essential for many use cases—such as identifying Tweets, uploaded videos, or tracing execution flows in distributed service architectures—and lay out how to meet the requirements for a robust ID generator.

---

## 🔑 Requirements for Unique Identifiers
**The system must satisfy these key requirements:**
- **Uniqueness:** Each event must be assigned a unique identifier.
- **Scalability:** The ID generation system should be able to generate at least a **billion unique IDs per day**.
- **Availability:** The system must handle rapid events (even at the nanosecond level) so that all events receive an identifier.
- **64-bit Numeric ID:** By restricting the ID to 64 bits, we ensure that the available range (roughly 1.8 × 10¹⁹ total values) lasts for over **50 million years** given an estimated rate of 365 billion events per year.

---

## 🛠️ First Solution: UUID
**UUIDs (Universally Unique Identifiers)** offer a straw man solution:
- A UUID is a **128-bit number** typically written in hexadecimal (for example, `123e4567-e89b-12d3-a456-426614174000`), which provides around 10³⁸ possible values.
- **Pros:**
    - **Decentralized generation:** Each server can generate its own UUID without coordination, ensuring high scalability and availability.
- **Cons:**
    - **Indexing issues:** Using 128-bit numbers as primary keys can slow down database indexing—leading to slower insert operations.
    - **Non-deterministic uniqueness:** There is a non-zero chance of duplication, and values are not guaranteed to be monotonically increasing.

---

## ⚙️ Second Solution: Using a Database
This approach mimics the auto-increment feature of databases:
- A **central database** maintains a counter that provides a unique ID for each request and then increments its value by one.
- **Important drawback:**
    - **Single Point of Failure (SPOF):** Relying on a central counter creates a bottleneck; if the central database experiences issues or goes down, the entire system’s ID generation is jeopardized.
- **Synchronization Overhead:**
    - Every request requires a synchronous transaction to update the counter, which limits throughput and scalability—especially in systems with high write demands.

---

## 💡 Third Solution: Using a Range Handler
To overcome previous challenges, a range-based system is proposed:
- A central microservice (the **range handler**) allocates a **range of numbers** (for example, 300,001 to 400,000) to each application server.
- Each server then uses its local range to generate sequential IDs until it exhausts the range; once finished, it requests a new range.
- **Pros:**
    - This approach is **scalable**, **available**, and ensures **unique 64-bit numeric IDs** across distributed servers.
- **Cons:**
    - If a server fails, a part of its range might get wasted until that server recovers or a new range is provided. Allocating smaller ranges can help mitigate this loss.

---

## 🔍 Final Considerations
The overall design ultimately produces a solution that assigns **unique IDs** to events and can serve as a **primary key** for data records. However, if an additional requirement is introduced—such as ensuring that IDs are **time sortable**—the design must evolve further (for example, by integrating a sequencing mechanism to preserve event causality).

---

Here is the full extracted text from the current page:

---

### Unique IDs with Causality
We'll cover the following:
- Causality
- Use UNIX time stamps (Pros & Cons)
- Twitter Snowflake (Pros & Cons)
- Using logical clocks (Lamport clocks, Vector clocks, TrueTime API - Pros & Cons)
- Summary

### 🔗 Causality
In the previous lesson, we generated **unique IDs** to differentiate between various events. Apart from having unique identifiers for events, we’re also interested in finding the **sequence** of these events.

Let’s consider an example where Peter and John are two Twitter users. John posts a comment (**Event A**), and Peter replies to John’s comment (**Event B**). **Event B depends on Event A** and can’t happen before it. The events are not concurrent here.

We can also have **concurrent events**—two events that occur **independently** of each other. For example, if Peter and John comment on two different Tweets, there’s **no happened-before relationship** or causality between them.

It’s **essential** to identify the **dependence** of one event over the other, but not in the case of concurrent events.

**Note:** This scenario can also be handled by **assigning a unique ID** and encoding the **dependence of events using a social graph**. We might also use a **separate time data structure** and a simple unique ID. However, **we want a unique ID to do double duty**—providing unique identification and **helping with the causality of events**.

### ⏳ Using Logical and Physical Clocks
Some applications need **unique identifiers** for events while also carrying any **causality information**.

For example, an identifier can be given to **concurrent writes** of a key into a **key-value store**, helping implement a **last-write-wins strategy**.

We can use either **logical** or **physical clocks** to infer **causality**. Some systems require event identifiers to **map wall-clock time**, like **financial applications** complying with MiFID regulations that require clocks to be within **100 microseconds of UTC** to detect anomalies during **high-speed market trades**.

### 🕰️ Physical Clocks
Computers typically have two types of physical clocks:
- **Time-of-day clocks:** Lower resolution, affected by **Network Time Protocol (NTP)**
- **Monotonic counters:** Higher resolution, but **not meaningful** across different nodes

**Clock Drift Causes:**
- **Temperature differences**
- **Hardware aging**
- **Manufacturing defects**
- **Virtualization effects**

A study showed that **public Internet-based NTP** couldn’t achieve **clock accuracy better than 35 milliseconds**, and congestion could cause **spikes up to one second**.

**Mitigation:** GPS and atomic clocks improve accuracy but **increase system complexity and cost**.

### ⚖️ Logical Clocks
**Lamport clocks** help **establish happened-before relationships**.

However, given two clock values from separate servers, **we can’t infer happened-before directly**, since the events could be **concurrent**. **Vector clocks** provide a better way to infer **causality**, requiring a **counter per participating entity**.

### ⏳ Using UNIX Time Stamps
UNIX time stamps **granular to the millisecond** can distinguish different events.

We have an **ID-generating server**, capable of **generating one ID per millisecond**. Any request to generate a unique ID is **routed to this server**, returning a **timestamp** and **unique ID**.

With this method, we can generate:  
**24(hours) × 60(min/hour) × 60(sec/min) × 1000(IDs/sec) = 86,400,000 IDs per day**.

However, **this poses a crucial problem**—the **ID-generating server is a single point of failure (SPOF)**.

### 🚀 Handling SPOF
To solve SPOF:
- **Multiple servers** generate IDs independently.
- Attach **server ID + UNIX timestamp** to maintain **uniqueness** across the system.
- **Load balancing** efficiently distributes traffic.

---

### ⏳ TrueTime API

TrueTime is Google's **highly available, distributed clock** system used in Spanner, a globally distributed database. It provides **monotonically increasing timestamps**, ensuring that timestamps assigned to transactions reflect their actual order across multiple servers.

#### 🔗 How TrueTime Works
Unlike traditional clocks, TrueTime represents time as an **interval of uncertainty** rather than a single timestamp. It provides:
- `TT.now()`: Returns a time interval `[earliest, latest]`, ensuring that the actual event time falls within this range.
- `TT.after(t)`: Confirms if time `t` has definitely passed.
- `TT.before(t)`: Confirms if time `t` has definitely not arrived.

#### 🕰️ Why TrueTime Matters
TrueTime enables **external consistency**, meaning transactions behave as if executed sequentially, even though they run across multiple servers. This prevents anomalies in financial applications, ensuring that transactions are ordered correctly and **never appear out of sequence**.

#### 🚀 Implementation
TrueTime relies on **GPS and atomic clocks** deployed across Google’s data centers. These clocks synchronize regularly, ensuring minimal drift and high accuracy.
