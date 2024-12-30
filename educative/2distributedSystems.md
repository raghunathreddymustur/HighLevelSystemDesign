# 📚 Distributed Systems

## 🏁 Getting Started
Learn what a distributed system is and why we need it. We'll cover the following:
- 📚 What is a distributed system?
- 🧩 Parts of a distributed system
- 🌟 Why we need a distributed system
    - 🚀 Performance
    - 📈 Scalability
    - 🔒 Availability

## 📚 What is a Distributed System?
According to Coulouris et al., "A distributed system is a system whose components are located on different networked computers, which communicate and coordinate their actions by passing messages to one another." The components of this system can be thought of as software programs that run on physical hardware, such as computers.

## 🧩 Parts of a Distributed System
There are two categories of the central parts that help distributed systems function:
- 🖥️ The various parts that compose a distributed system: These are located remotely and are separated by a network.
- 🌐 The network that separates the various parts of a distributed system: It acts as a communication mechanism that lets them exchange messages.

## 🌟 Why We Need a Distributed System
There are three main benefits of distributed systems:
- 🚀 Performance
- 🔒 Availability
- 📈 Scalability

### 🚀 Performance
According to Mohan et al., "Performance is the degree to which a software system or component meets its objectives for timeliness."

#### Problem with a Single Computer
The physical constraints of its hardware impose certain limits on the performance of a single computer. Moreover, it is extremely expensive to improve a single computer's performance after a certain point.

#### Solution
We can achieve the same performance with two or more low-spec computers as with a single, high-end computer. So, distributed systems allow us to achieve better performance at a lower cost.

### 📈 Scalability
According to Bondi et al., "Scalability is the capability of a system, network, or process to handle a growing amount of work, or its potential to be enlarged to accommodate that growth."

#### Problem with a Single Computer
A system that comprises a single computer can only scale up to a certain point.

#### Solution
If we build a distributed system, we can split and store the data in multiple computers, and distribute the processing work. Vertical scaling refers to adding resources to a single node, while horizontal scaling refers to adding more nodes to the system.

### 🔒 Availability
Availability is the probability of a system to work as required, when required, during a mission.

#### Problem with a Single Computer
Most online services need to operate 24/7, which is a huge challenge. It would be infeasible to provide this kind of guarantee with a single computer.

#### Solution
Redundancy is used to achieve higher availability by storing data in multiple computers. This way, when one computer fails, we can efficiently switch to another one.

## 🏁 Conclusion
Distributed systems offer significant benefits, but there are trade-offs and limitations. Understanding these constraints is essential for leveraging distributed systems effectively.

# 📚 Fallacies of Distributed Computing

## 🏁 Introduction to Fallacies of Distributed Computing
This section introduces the concept of fallacies in distributed computing and explains why developers often make false assumptions when developing software for distributed systems.

## 🧩 Difference in Developing Software for Distributed Systems
Developing software for distributed systems is different from developing for single-computer systems due to additional constraints. New developers often make incorrect assumptions based on their experience with single-computer systems.

## 🌟 Fallacies of Distributed Computing
L Peter Deutsch and others at Sun Microsystems identified eight false assumptions developers make about distributed computing. These are known as the fallacies of distributed computing.

## 📋 List of Fallacies
The eight fallacies are:
- 🌐 The network is reliable
- ⏱️ Latency is zero
- 📶 Bandwidth is infinite
- 🗺️ Topology doesn’t change
- 🔒 The network is secure
- 👤 There is one administrator
- 💸 Transport cost is zero
- 🖥️ The network is homogeneous

## 📝 Explanation of Fallacies
Each fallacy is briefly explained, highlighting why these assumptions are incorrect and the potential problems they can cause in distributed systems.

### 🌐 The Network is Reliable
This fallacy is based on the misconception that networking protocols like TCP ensure network reliability. However, hardware failures and other issues can disrupt network reliability.

### ⏱️ Latency is Zero
This fallacy assumes that remote procedure calls have the same latency as local calls. In reality, there is a significant difference in latency between remote and local calls, especially across different data centers.

### 📶 Bandwidth is Infinite
While bandwidth has improved, it is not infinite. This fallacy is important to consider when designing distributed systems, especially when data needs to travel across the Internet.

### 🔒 The Network is Secure
This fallacy assumes that the network used for communication between nodes is secure. In reality, the network is often insecure, and security measures must be implemented.

### 🗺️ Topology Doesn’t Change
This fallacy assumes that the network topology remains constant. In reality, network topology can change due to failures and other factors, requiring systems to adapt.

### 💸 Transport Cost is Zero
This fallacy overlooks the financial costs associated with data transport between nodes. These costs must be considered when designing distributed systems.

### 🕰️ The Global Clock Fallacy
This additional fallacy assumes that distributed systems have a global clock to synchronize events. In reality, each node has its own local clock, and synchronization is challenging.

# 🚀 Difficulties Designing Distributed Systems

Let's see what makes distributed systems hard to design. We'll cover the following:
- 🌐 Why distributed systems are hard to design
- 🛠️ Properties that make distributed systems challenging
    - 📡 Network asynchrony
    - ⚠️ Partial failures
    - 🔄 Concurrency

## 🌐 Why distributed systems are hard to design

In general, distributed systems are hard to design, build, and reason about. This increases the risk of error. Understanding why distributed systems are so hard to design helps eliminate blind spots and provides guidance on aspects to pay attention to.

## 🛠️ Properties that make distributed systems challenging

The following illustration shows the main properties that make distributed systems challenging to reason about:
- **📡 Network Asynchrony**
- **⚠️ Partial Failures**
- **🔄 Concurrency**

### 📡 Network Asynchrony

Network asynchrony is a property of communication networks that cannot provide strong guarantees around delivering events, such as a maximum amount of time a message requires for delivery. This can create counter-intuitive behaviors not present in non-distributed systems. For instance, messages might take extremely long to deliver, may deliver out of order, or not at all.

### ⚠️ Partial Failures

Partial failures occur when only some components of a distributed system fail. This contrasts with applications deployed on a single server, which assume either everything is working fine or there has been a server crash. Ensuring atomicity across components in a distributed system introduces significant complexity.

### 🔄 Concurrency

Concurrency is the execution of multiple computations at the same time, potentially on the same piece of data. These computations interleave with each other, introducing additional complexity as they can interfere with each other and create unexpected behaviors.

## 🏁 Conclusion

Network asynchrony, partial failures, and concurrency are major contributors to the complexity of distributed systems. Keeping these properties in mind when building distributed systems helps anticipate edge cases and handle them appropriately.

# 🧩 Measures of Correctness in Distributed Systems

Let's see how to measure the correctness of a distributed system. We'll cover the following:
- ✅ Correctness
- 📏 Measures of Correctness
    - 🛡️ Safety property
    - ⏳ Liveness property

## ✅ Correctness

We can define the correctness of a system in terms of the properties it must satisfy.

## 📏 Measures of Correctness

The correctness measures for distributed systems are the two properties they must satisfy. These are the following:
- **🛡️ Safety property**
- **⏳ Liveness property**

### 🛡️ Safety Property

A safety property defines something that must never happen in a correct system. For example, the oven temperature exceeding the specified limit shouldn't happen.

### ⏳ Liveness Property

A liveness property defines something that must eventually happen in a correct system. For example, the oven temperature eventually reaching the specified limit must happen.

## 🏁 Example of a Correct System

If we consider the correct properties of an oven, we can say that "the oven not exceeding a maximum temperature threshold" is a safety property. The property of "the oven eventually reaching the temperature we specified via the button" is a liveness property. Similar to this example, it’s usually more important in distributed systems to ensure the system satisfies the safety property than the liveness one. The safety property weighs more than liveness in distributed systems.

## ⚖️ Conclusion

Throughout this course, it will become clear that there is an inherent tension between safety and liveness properties. Actually, as we will see later in this course, there are some problems that make it physically impossible to satisfy both kinds of properties. So, we need to compromise some liveness properties to maintain safety.

# 🌐 System Models

## 🌐 Nature of real-life distributed systems
Real-life distributed systems vary greatly due to factors like the network and hardware. A common framework is needed to solve problems generically.

## 🛠️ Making a generic model
To model a distributed system, several properties must be defined. Proving an algorithm's correctness for this model ensures it works for all systems with these properties.

## 🔧 Properties each system follows
Important properties in a distributed system include **how nodes interact and how they can fail.**

## 📚 Categories of distributed systems
Distributed systems are categorized into synchronous and asynchronous systems based on communication nature.

## ⏱️ Synchronous system
In a synchronous system, nodes have accurate clocks, and there is a known upper bound on message transmission delay and processing time. Nodes run in lock-step.

## 🌐 Asynchronous system
In an asynchronous system, there is no fixed upper bound on message delivery time or time between node steps. Nodes run at independent rates, making it closer to real-life systems like the Internet.

# ⚠️ Types of Failures

## 🛠️ Main categories of failures in Distributed Systems
There are several different types of failures. The following illustration shows the most basic categories.

## ⚠️ Fail-stop
A node halts and remains halted permanently. Other nodes can detect that the node has failed (i.e., by communicating with it).

## ⚠️ Crash
A node halts, but silently. So, other nodes may not be able to detect this state. They can only assume its failure when they are unable to communicate with it.

## ⚠️ Omission
A node fails to respond to incoming requests.

## ⚠️ Byzantine
A node exhibits arbitrary behavior: it may transmit arbitrary messages at arbitrary times, take incorrect steps, or stop. Byzantine failures occur when a node does not behave according to its specific protocol or algorithm. This usually happens when a malicious actor or a software bug compromises the node. To cope with these failures, we need complex solutions. However, most companies deploy distributed systems in environments that they assume to be private and secure.

## 🛠️ Fail-stop failures
Fail-stop failures are the simplest and the most convenient ones from the perspective of someone that builds distributed systems. However, they are not very realistic. This is because there are many cases in real-life systems where it’s not easy for us to identify whether another node crashes or not. Most of the algorithms we analyze in this course work under the assumption of crash failures.

# 📜 The Tale of Exactly-Once Semantics

## 📬 Multiple deliveries of a message
Various nodes of a distributed system communicate with each other through the exchange of messages. As the network is not reliable, these messages might get lost. Of course, to cope with this, nodes can retry with the hope that the network will recover at some point and deliver the message. However, this means that the nodes may deliver messages multiple times because the sender can’t know what really happens. The following illustration shows what happens when a node doesn’t deliver a message at all. The following illustration shows a message that a node delivers twice.

## ⚠️ Example consequence
Think about what would happen if the message is supposed to signal the transfer of money between two bank accounts as part of a purchase. The bank may charge a customer twice for a product.

## 🛠️ Avoiding multiple deliveries of a message
To handle scenarios like the one above, we can take multiple approaches to ensure that the nodes only process a message once, even though it may be delivered multiple times. Let’s see these approaches.

## 🔄 Idempotent operations approach
Idempotent is an operation we can apply multiple times without changing the result beyond the initial application.

## ✅ Example of idempotent operation
An example of an idempotent operation is to add a value in a set of values. Even if we apply this operation multiple times, the operations that run after the first will have no effect, since the value will already be added to the set. Of course, we assume here that other operations cannot remove values from the set. Otherwise, the retried operation may add a value that was removed.

## ❌ Example of non-idempotent operation
An example of a non-idempotent operation is to increase a counter by one, where the operation will have additional side effects every time it’s applied. By using idempotent operations, we can have the guarantee that even if a node delivers a message multiple times and repeats the operation, the result will be the same. However, idempotent operations commonly impose tight constraints on the system. So, in many cases, we cannot build our system so that all operations are idempotent by nature. In these cases, we can use another approach: the de-duplication approach.

## 🔄 De-duplication approach
In the de-duplication approach, we give every message a unique identifier, and every retried message contains the same identifier as the original. In this way, the recipient can remember the set of identifiers it received and executed already. It will also avoid executing operations that are executed. It is important to note that in order to do this, we must have control on both sides of the system: sender and receiver. This is because the ID generation occurs on the sender side, but the de-duplication process occurs on the receiver side.

## 📧 Example
Imagine a scenario where an application sends emails as part of an operation. To send an email is not an idempotent operation. If the email protocol does not support de-duplication on the receiver side, we can’t be sure that every email displays exactly once to the recipient.

## 📬 Difference between delivery and processing
When we think about exactly-once semantics, it’s useful to distinguish between the notions of delivery and processing. In the context of the above discussion, let’s consider delivery to be the arrival of the message at the destination node, at the hardware level. Then, we consider processing to be the handling of this message from the software application layer of the node. In most cases, we care more about how many times a node processes a message, than about how many times it delivers it. For instance, in our previous email example, we were mainly interested in whether the application would display the same email twice, and not whether it would receive it twice. As the previous examples demonstrated, it’s impossible to have exactly-once delivery in a distributed system. However, it’s still sometimes possible to have exactly-once processing. In the end, it’s important for us to understand the difference between these two notions, and clarify what we refer to when we talk about exactly-once semantics.

## 📬 Other delivery semantics
As a last note, it’s easy to see that we can easily implement at-most-once delivery semantics and at-least-once delivery semantics. We can achieve the at-most-once delivery when we send every message only one time, no matter what happens. Meanwhile, we can achieve the at-least-once delivery when we send a message continuously until we get an acknowledgment from the recipient.
## More Implementation Info
[Realtime Implementation](#idempotency-implementation)


Sure, here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in bold text:

---

# 📉 Failure in the World of Distributed Systems
Let's see why failures occur in distributed systems, and how we can detect them. We'll cover the following:
- One reason for failure
- One mechanism to detect failure
- Trade-off for the small timeout value
- Trade-off for the large timeout value
- Failure detector
- Properties that categorize failure detectors
- A perfect failure detector

## ⚠️ One reason for failure
The **asynchronous nature of the network** in a distributed system can make it very hard for us to differentiate between a crashed node and a node that is just really slow to respond to requests.

## 🔍 One mechanism to detect failure
**Timeouts** is the main mechanism we can use to detect failures in distributed systems. Since an asynchronous network can infinitely delay messages, timeouts impose an artificial upper bound on these delays. As a result, we can assume that a node fails when it is slower than this bound.

## ⚖️ Trade-off for the small timeout value
If we select a **smaller value for the timeout**, our system will waste less time waiting for the nodes that have crashed. At the same time, the system might declare some nodes that have not crashed dead, while they are actually just a bit slower than expected.

## ⚖️ Trade-off for the large timeout value
If we select a **larger value for the timeout**, the system will be more lenient with slow nodes. At the same time, the system will be slower in identifying crashed nodes, in some cases wasting time while waiting for them.

## 🛠️ Failure detector
A **failure detector** is the component of a node that we can use to identify other nodes that have failed. This component is essential for various algorithms that need to make progress in the presence of failures.

## 📊 Properties that categorize failure detectors
We can distinguish the different categories of failure detectors through two basic properties that reflect the trade-off:
- **Completeness** corresponds to the percentage of crashed nodes a failure detector successfully identifies in a certain period.
- **Accuracy** corresponds to the number of mistakes a failure detector makes in a certain period.

## 🌟 A perfect failure detector
A **perfect failure detector** is the one with the strongest form of completeness and accuracy. That is, it is one that successfully detects every faulty process without ever assuming a node has crashed before it actually does. As expected, it is impossible to build a perfect failure detector in purely asynchronous systems.

---

Sure, here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in bold text:

---

# 🖥️ Stateless and Stateful Systems
Let's see the difference between stateless and stateful systems. We'll cover the following:
- Stateless system
- Examples
- Stateful systems
- Example
- Some interesting observations
- Benefits of stateless systems over stateful systems

## 📊 Stateless system
A **stateless system** maintains no state of what happened in the past and performs its capabilities purely based on the inputs we provide to it.

## 📈 Examples
A contrived stateless system receives a set of numbers as input, calculates their maximum, and returns it as a result. These inputs are either direct or indirect. Direct inputs are included in the request, while indirect inputs are potentially received from other systems to fulfill the request. Imagine a service that calculates the price of a specific product by retrieving its initial price and any currently available discounts from some other services, and then performing the necessary calculations with this data. This service is still stateless.

## 🗂️ Stateful systems
**Stateful systems** are responsible for maintaining and mutating a state. Their results depend on this state.

## 📋 Example
Imagine a system that stores the ages of all the employees of a company, and we can ask it the maximum age. This system is stateful since the result depends on the employees we register in it.

## 💡 Some interesting observations
Stateful systems are beneficial in real life because computers are much more capable than humans of storing and processing data. Maintaining state involves additional complexity. For example, we must decide what’s the most efficient way to store and process it, how to perform back-ups, etc. As a result, it’s usually wise to create an architecture that contains clear boundaries between stateless components (which perform business capabilities) and stateful components (which handle data).

## 🌟 Benefits of stateless systems over stateful systems
**Stateless distributed systems** are much easier to design, build, and scale, compared to stateful ones. The main reason for this is that we consider all the nodes (e.g., servers) of a stateless system identical. This makes it a lot easier for us to balance traffic between them, and scale by adding or removing servers. However, stateful systems present many more challenges. As different nodes can hold different pieces of data, they require additional work. They need to direct traffic to the right place and ensure each instance is in sync with the others. As a result, some of the course’s examples include stateless systems. However, the most challenging problems we cover in this course mainly concern stateful systems.

---

Sure, here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in bold text:

---

# 📊 Partitioning
See how we can make our system scalable by partitioning. We'll cover the following:
- Scalability
- Mechanism to achieve scalability
- Partitioning
- Vertical partitioning
- Horizontal partitioning
- Limitations of partitioning

## 📈 Scalability
**Scalability** lets us store and process datasets much larger than what we could with a single machine.

## 🛠️ Mechanism to achieve scalability
One of the primary mechanisms of achieving scalability is **partitioning**.

## 📂 Partitioning
**Partitioning** is the process of splitting a dataset into multiple, smaller datasets, and then assigning the responsibility of storing and processing them to different nodes of a distributed system. This allows us to add more nodes to our system and increase the size of the data it can handle.

## 📊 Vertical partitioning
**Vertical partitioning** involves splitting a table into multiple tables with fewer columns and using additional tables to store columns that relate rows across tables. We commonly refer to this as a join operation. We can then store these different tables in different nodes. Normalization is one way to perform vertical partitioning. However, general vertical partitioning goes far beyond that: it splits a column, even when they are normalized.

## 📊 Horizontal partitioning
**Horizontal partitioning** involves splitting a table into multiple, smaller tables, where each table contains a percentage of the initial table’s rows. We can then store these different subtables in different nodes. We can perform this split through multiple strategies. A simplistic approach for this is an alphabetical split. For instance, we can horizontally partition a table that contains the students of a school by using the students’ surnames.

## ⚖️ Limitations of partitioning
In a vertically partitioned system, requests that need to combine data from different tables (i.e., join operations) become less efficient. This is because these requests may now have to access data from multiple nodes. In a horizontally partitioned system, we can usually avoid accessing data from multiple nodes because all the data for each row is located in the same node. However, we may still need to access data from multiple nodes for requests that are searching for a range of rows that belong to multiple nodes. Another important implication of horizontal partitioning is the potential for loss of transactional semantics. When we store data in a single machine, we can easily perform multiple operations in an atomic way, where either all or none of them succeed. However, this is much harder to achieve in a distributed system. As a result, it’s much harder to perform atomic operations—when partitioning data horizontally—over data that resides in different nodes. This is a common theme in distributed systems; there’s no silver bullet. We have to make trade-offs to achieve the property we desire. Vertical partitioning is mainly a data modeling practice, which can be performed by the engineers designing a system—sometimes independently of the storage systems used. However, horizontal partitioning is a common feature of distributed databases. So, to use these systems properly, engineers need to know how the system works under the hood. Therefore, we will mostly focus on horizontal partitioning.

---

Sure, here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in bold text:

---

# 🧩 Algorithms for Horizontal Partitioning
Let's look into the algorithms used for horizontal partitioning. We'll cover the following:
- Range partitioning
- Hash partitioning
- Consistent hashing

## 📊 Range partitioning
**Range partitioning** is a technique where we split a dataset into ranges according to the value of a specific attribute. We then store each range in a separate node. For example, an alphabetical split of last names.

## 🌟 Advantages of range partitioning
Some advantages of range partitioning include:
- **Simplicity and ease of implementation**
- The ability to perform range queries using the partitioning key value
- Good performance for small range queries that reside in a single node
- Easier and more efficient repartitioning by adjusting ranges

## ⚠️ Disadvantages of range partitioning
Some disadvantages of range partitioning include:
- Inability to perform range queries using keys other than the partitioning key
- Poor performance for large range queries that span multiple nodes
- Uneven distribution of traffic or data, causing some nodes to overload

## 🔄 Hash partitioning
**Hash partitioning** is a technique where we apply a hash function to a specific attribute of each row, resulting in a number that determines which partition—and thus, node—this row belongs to.

## 🌟 Advantages of hash partitioning
Some advantages of hash partitioning include:
- **Runtime calculation of partitioning mapping** without needing to store and maintain the mapping
- Uniform distribution of data across nodes, preventing overload

## ⚠️ Disadvantages of hash partitioning
Some disadvantages of hash partitioning include:
- Inability to perform range queries without additional data or querying all nodes
- Significant data movement across nodes when adding or removing nodes

## 🔄 Consistent hashing
**Consistent hashing** is a partitioning technique similar to hash partitioning but solves the increased data movement problem. Each node is randomly assigned an integer in a range, and data is assigned based on this range.

## 🌟 Advantages of consistent hashing
The main advantage of consistent hashing is **reduced data movement** when nodes are added or removed.

## ⚠️ Disadvantages of consistent hashing
Some disadvantages of consistent hashing include:
- Potential for nonuniform data distribution due to random node assignment
- Imbalanced data distribution as nodes are added or removed

---

Sure, here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in bold text:

---

# 🔄 Replication
Learn what replication is and why it is used in distributed systems. We'll cover the following:
- Partitioning
- Availability
- Mechanism to achieve availability
- Replication
- Pessimistic replication
- Optimistic replication

## 📊 Partitioning
**Partitioning** can improve the scalability and performance of a system by distributing data and request load to multiple nodes.

## 🌟 Availability
**Availability** refers to the ability of the system to remain functional despite failures in parts of it.

## 🛠️ Mechanism to achieve availability
The technique we use to achieve availability is **replication**.

## 🔄 Replication
**Replication** is the main technique used in distributed systems to increase availability. It consists of storing the same piece of data in multiple nodes (called replicas) so that if one of them crashes, data is not lost, and requests can be served from the other nodes in the meanwhile.

## ⚠️ Complications of replication
The benefit of increased availability from replication comes with a set of new complications. Replication implies that the system now has multiple copies of every piece of data. These copies must be maintained and kept in sync with each other on every update.

## 🧩 Pessimistic replication
**Pessimistic replication** tries to guarantee from the beginning that all the replicas are identical to each other—as if there was only one copy of the data all along.

## 🌟 Optimistic replication
**Optimistic replication**, or lazy replication, allows the different replicas to diverge. This guarantees that they will converge again if the system does not receive any updates, or enters a quiesced state, for a period of time.

---
Sure thing! Here's the updated README without the last line:

---

### 📚 Primary-Backup Replication Algorithm
Learn about primary-backup replication, and its practical application, advantages, and disadvantages.

### 🔄 Primary-backup replication
Primary-backup replication is a technique where we designate a single node amongst the replicas as the leader, or primary, that receives all the updates. This technique is also known as single-master replication. We commonly refer to the remaining replicas as followers or secondaries. These can only handle read requests. Every time the leader receives an update, it executes it locally and also propagates the update to the other nodes. This ensures that all the replicas maintain a consistent view of the data.

### 🔄 Techniques for propagating updates
There are two ways to propagate the updates: synchronously and asynchronously.

### ⏳ Synchronous replication
In synchronous replication, the node replies to the client to indicate the update is complete—only after receiving acknowledgments from the other replicas that they’ve also performed the update on their local storage. This guarantees that the client is able to view the update in a subsequent read after acknowledging it, no matter which replica the client reads from. Furthermore, synchronous replication provides increased durability. This is because the update is not lost even if the leader crashes right after it acknowledges the update. However, this technique can make writing requests slower. This is because the leader has to wait until it receives responses from all the replicas.

### ⏳ Asynchronous replication
In asynchronous replication, the node replies to the client as soon as it performs the update in its local storage, without waiting for responses from the other replicas. This technique increases performance significantly for write requests. This is because the client no longer pays the penalty of the network requests to the other replicas. However, this comes at the cost of reduced consistency and decreased durability. After a client receives a response for an update request, the client might read older (stale) values in a subsequent read. This is only possible if the operation happens in one of the replicas that have not yet performed the update. Moreover, if the leader node crashes right after it acknowledges an update, and the propagation requests to the other replicas are lost, any acknowledged update is eventually lost.

### 📊 Advantages of primary-backup replication
- **Simple to understand and implement**
- **Concurrent operations serialized in the leader node remove the need for more complicated, distributed concurrency protocols**
- **Scalable for read-heavy workloads because the capacity for reading requests can be increased by adding more read replicas**

### 📉 Disadvantages of primary-backup replication
- **Not very scalable for write-heavy workloads because a single node’s capacity (the leader’s capacity) determines the capacity for writes**
- **Imposes an obvious trade-off between performance, durability, and consistency**
- **Scaling the read capacity by adding more follower nodes can create a bottleneck in the network bandwidth of the leader node, if there’s a large number of followers listening for updates**
- **The process of failing over to a follower node when the leader node crashes is not instant. This may create some downtime and also introduce the risk of errors**

### 🔄 Failover
Failover is when the leader node crashes and a follower node takes over.

### 🔄 Managing failover
In general, there are two approaches to perform a failover: manual and automated.

### 🛠️ Manual approach
In the manual approach, the operator selects the new leader node and instructs all the nodes accordingly. This is the safest approach, but it incurs significant downtime.

### ⚙️ Automated approach
An alternative is an automated approach, where follower nodes detect that the leader node has crashed (e.g., via periodic heartbeats), and attempt to elect a new leader node. This is faster but is quite risky. This is because there are many different ways in which the nodes can get confused and arrive at an incorrect state.

---

Sure thing! Here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in **bold**:

---

### 📚 Multi-Primary Replication Algorithm
Look at the multi-primary algorithm for replication.

### 🔄 Primary-backup replication
As we saw in the previous lesson, primary-backup replication is a technique that is easy to implement and operate. It can easily support transactions and hide the distributed nature of the underlying system, i.e., when using synchronous replication. However, primary-backup replication has some limitations in terms of performance, scalability, and availability. As we’ve already discussed, there are many applications where availability and performance are much more important than data consistency or transactional semantics. A frequently cited example is that of an e-commerce shopping cart, where the most important thing is for customers to be able to access their cart at all times and add items quickly and easily. It is acceptable to compromise consistency to achieve this, as long as there is data reconciliation at some point. For instance, if two replicas diverge because of intermittent failures, the customer can still resolve conflicts during the checkout process.

### 🔄 Multi-primary replication
Multi-primary replication is an alternative replication technique that favors higher availability and performance over data consistency. This technique is also known as multi-master replication. In this technique, all replicas are equal and can accept write requests. They are also responsible for propagating the data modifications to the rest of the group. Multi-primary replication has a significant difference from primary-backup replication. In multi-primary replication, there is no single leader node that serializes the requests and imposes a single order, as write requests are concurrently handled by all the nodes. This means that nodes might disagree on what is the right order for some requests. We usually refer to this as a conflict. For the system to remain operational, the nodes need to resolve this conflict when it occurs by agreeing on a single order from the available ones.

### 🔄 Conflict resolution
There are many different ways to resolve conflicts, depending on the guarantees the system wants to provide. An important aspect of different approaches to resolving conflicts is whether they do it eagerly or lazily. In the eagerly case, the conflict is resolved during the write operation. In the lazily case, the write operation proceeds to maintain multiple, alternative versions of the data record that are eventually resolved to a single version later on, i.e., during a subsequent read operation.

### 🛠️ Approaches to conflict resolution
Here are some common approaches to conflict resolution:

- **Exposing conflict resolution to the clients**: When there is a conflict, the multiple available versions return to the client. The client then selects the right version and returns it to the system. This resolves the conflict. An example of this is the shopping cart application, where the customer selects the correct version of their cart.
- **Last-write-wins conflict resolution**: Each node in the system tags each version with a timestamp, using a local clock. During a conflict, the version with the latest timestamp is selected. However, this technique can lead to some unexpected behaviors, as there is no global notion of time. For example, write A can override write B, even though B happened “as a result” of A.
- **Causality tracking algorithms**: The system uses an algorithm that keeps track of causal relationships between different requests. When there is a conflict between two writes (A, B) and one is determined to be the cause of the other one (suppose A is the cause of B), then the resulting write (B) is retained. However, there can still be writes that are not causally related, i.e., requests are actually concurrent. In such cases, the system cannot make an easy decision. We’ll elaborate more on some of these approaches later in the chapters about time and order.

---
Sure thing! Here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in **bold**:

---

### 📚 Quorums in Distributed Systems
Look at the concept of quorums and see how they solve low availability problems in synchronous replication.

### 🔄 Main Pattern
The main pattern we’ve seen so far is this: writes are performed to all the replica nodes, while reads are performed to one of them. When we ensure that writes are performed to all of them synchronously before replying to the client, we guarantee that the subsequent reads see all the previous writes—regardless of the node that processes the read operation.

### 🔄 Write and Read Requests
While one node receives a write request in either of the replication algorithms discussed earlier, the data is updated on all the nodes as a result of this request. Similarly, when a node receives a read request, it reads it from its local storage rather than performing a read on all the nodes. In the case of multi-primary replication, reads may be performed on all the nodes to handle write conflicts, but that is one possible solution and can’t be generalized as a pattern.

### 📉 Problem in Synchronous Replication
Availability is quite low for write operations because the failure of a single node makes the system unable to process writes until the node recovers.

### 🛠️ Possible Solution
To solve this problem, we can use the reverse strategy. That is, we write data only to the node that is responsible for processing a write operation, but process read operations by reading from all the nodes and returning the latest value. **This increases the availability of writes significantly but decreases the availability of reads at the same time. So, we have a trade-off that needs a mechanism to achieve a balance. Let’s see that mechanism.**

### 🔄 Quorums
A useful mechanism to achieve a balance in this trade-off is to use quorums.

### 🛠️ Example of Quorums
In a system of three replicas, we can say that writes need to complete in two nodes (as a quorum of two), while reads need to retrieve data from two nodes. This way, we can be sure that the reads will read the latest value. This is because at least one of the nodes in the read quorum will also be included in the latest write quorum. This is based on the fact that in a set of three elements, two subsets of two elements must have at least one common element.

### 📜 Quorum-Based Voting Protocol
A past paper introduced this technique as a quorum-based voting protocol for replica control. In general, in a system that has a total of V replicas, every read operation should obtain a read quorum of V_r replicas. Meanwhile, a write operation should obtain a write quorum of V_w replicas. The values of these quorums should obey the following properties:
- **V_r + V_w > V**
- **V_w > V / 2**

### 📊 Ensuring Data Consistency
The first rule ensures that a data item is not read and written by two operations concurrently. The second rule ensures that at least one node receives both of the two write operations and imposes an order on them. This means that two write operations from two different operations cannot occur concurrently on the same data item. Both of the rules together guarantee that the associated distributed database behaves as a centralized, one-replica database system.

### 🔄 Use of Quorums
The concept of a quorum is really useful in distributed systems that have multiple nodes. The concept of a quorum is used extensively in other areas, like distributed transactions or consensus protocols.

<details>
<summary>Rationale Why Availability is effected</summary>

### 📉 Problem in Synchronous Replication
In the context of synchronous replication, availability is a problem because the system requires all replicas to acknowledge a write operation before it can be considered complete. This means that if even one replica is unavailable or slow to respond, the entire write operation is delayed or fails. This dependency on all replicas being available and responsive reduces the overall availability of the system for write operations.

**Key Points:**
- **Synchronous Replication**: Requires all replicas to acknowledge a write before completion.
- **Availability Issue**: If one replica is down or slow, the write operation is delayed or fails.
- **Performance Trade-off**: While synchronous replication ensures data consistency, it sacrifices availability for write operations.

**Example:**
Imagine a system with three replicas. In synchronous replication, a write operation must be acknowledged by all three replicas. If one replica is down, the write operation cannot be completed, reducing the system's availability for writes. This is why availability is a problem in synchronous replication, rather than performance.

By using quorums, we can balance this trade-off by allowing a subset of replicas to acknowledge the write operation, thus improving availability while still maintaining a level of consistency.
</details>
---



Sure thing! Here's a summary of each paragraph from the current page, with meaningful icons before headings and important sections highlighted in **bold**:

---

### 🔒 Safety Guarantees in Distributed Systems
Explore the properties that guarantee safety in distributed systems and their relation to the difficulties in designing these systems.

### 🔄 Importance of Safety Guarantees
Since distributed systems involve a lot of complexity, some safety guarantees ensure that the system will behave in specific, predictable ways. This makes it easier for people to reason about a system and any potential anomalies that can occur. This will allow them to build proper safeguards to prevent these anomalies from occurring.

### 🛡️ Safety Guarantors
The main safety guarantees that systems provide are around the three properties shown in the illustration:
- **Atomicity**
- **Consistency**
- **Isolation**

### 📜 Properties that Guarantee Safety in Distributed Systems
Three properties guarantee safety in a distributed system:
- **Atomicity**
- **Consistency**
- **Isolation**

### 📚 Origin of Concepts
The concepts of atomicity and isolation originate from database research and ACID transactions. When we mention consistency in this course, we will mostly refer to the notion of consistency made popular by the CAP theorem. Before going any further, it is useful to look at these topics. We will study these two topics in detail in the next two lessons.

### 🔄 Relation to Design Challenges
It is interesting to observe that each of these safety guarantees is tightly related to the aforementioned reasons that make distributed systems hard to design.

### ⚙️ Achieving Atomicity
It is challenging to achieve atomicity in a distributed system because of the possibility of partial failures. A partial failure occurs when some components in the system fail.

### 🔄 Achieving Consistency
It is challenging to achieve consistency because of network asynchrony. Network asynchrony occurs when different nodes in a network have different values for the current time.

### 🔄 Achieving Isolation
It is challenging to achieve isolation because of the inherent concurrency of distributed systems. Concurrency occurs when multiple things happen at the same time.

---












































# Realtime Implementation

# Idempotency Implementation

## 🛠️ Understanding Idempotency in REST APIs and Microservices
Idempotency in REST APIs ensures that making the same request multiple times results in the same outcome as making it once. This is crucial for maintaining consistency and reliability in distributed systems, where network failures or retries are common.

## 🔑 Importance of Idempotency in Microservices
Idempotency is essential in microservices for ensuring data consistency, reliable retries, and preventing unintended side effects. It supports scalability, fault tolerance, and simplifies client logic while enabling effective caching strategies.

## 🧰 Implementation Techniques for Idempotent Operations in Spring Boot
Spring Boot provides tools to implement idempotency, such as using idempotency keys, database transactions, Redis for distributed systems, conditional requests with HTTP headers, and transaction tokens to ensure operations are processed only once.

### Example: Using Idempotency Keys
```java
@RestController
@RequestMapping("/orders")
public class OrderController {
    private final Map<String, OrderResponse> idempotencyStore = new ConcurrentHashMap<>();

    @PostMapping
    public ResponseEntity<OrderResponse> placeOrder(@RequestBody OrderRequest request,
                                                    @RequestHeader("Idempotency-Key") String idempotencyKey) {
        if (idempotencyStore.containsKey(idempotencyKey)) {
            return ResponseEntity.ok(idempotencyStore.get(idempotencyKey));
        }
        // Process the order
        OrderResponse response = new OrderResponse(/*...*/);
        idempotencyStore.put(idempotencyKey, response);
        return ResponseEntity.ok(response);
    }
}
```

### Example: Using Database Transactions
```java
@Service
public class OrderService {
    @Transactional
    public Order placeOrder(OrderRequest request) {
        // Logic to place an order
    }
}
```

### Example: Using Redis for Idempotency
```java
@Bean
public RedisTemplate<String, IdempotencyValue> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
    RedisTemplate<String, IdempotencyValue> template = new RedisTemplate<>();
    template.setConnectionFactory(redisConnectionFactory);
    // Set serializers
    return template;
}

public class IdempotenceFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)
            throws ServletException, IOException {
        String cacheKey = generateCacheKey(request);
        BoundValueOperations<String, IdempotencyValue> keyOperation = redisTemplate.boundValueOps(cacheKey);
        boolean isAbsent = keyOperation.setIfAbsent(IdempotencyValue.init(), ttl, TimeUnit.MINUTES);
        if (isAbsent) {
            // Process request
        } else {
            // Return cached response
        }
    }
}
```

### Example: Conditional Requests
```java
@PostMapping("/{id}")
public ResponseEntity<Item> createOrUpdateItem(@PathVariable String id, @RequestBody Item item,
                                               @RequestHeader(value = "If-None-Match", required = false) String ifNoneMatch) {
    if (itemMap.containsKey(id)) {
        Item existingItem = itemMap.get(id);
        String currentETag = generateETag(existingItem);
        if (ifNoneMatch != null && ifNoneMatch.equals(currentETag)) {
            return ResponseEntity.status(HttpStatus.NOT_MODIFIED).build();
        }
    }
    // Save or update the item
    return ResponseEntity.ok(item);
}
```

### Example: Transaction Tokens
```java
@PostMapping("/{id}")
public ResponseEntity<Item> createOrUpdateItem(@PathVariable String id, @RequestBody Item item,
                                               @RequestHeader(value = "Transaction-Token", required = false) String transactionToken) {
    if (transactionToken != null && itemMap.containsValue(transactionToken)) {
        return ResponseEntity.ok(itemMap.get(transactionToken));
    }
    // Process the request
    String newToken = UUID.randomUUID().toString();
    itemMap.put(newToken, item);
    return ResponseEntity.ok().header("Transaction-Token", newToken).body(item);
}
```

## ✅ Best Practices for Implementing Idempotency
To implement idempotency effectively, define clear policies, use idempotency libraries, test for duplicate requests, optimize key storage, handle errors robustly, use appropriate HTTP methods, and implement distributed locks when necessary.

## ⚠️ Challenges in Maintaining Idempotency
Challenges include managing concurrency, ensuring unique identifiers, maintaining idempotency across interconnected services, balancing eventual consistency with idempotency, and addressing HTTP method limitations.

## 📌 Conclusion
Idempotency is a fundamental principle for building robust and reliable microservices. By leveraging Spring Boot's features, adopting best practices, and addressing challenges, developers can create systems that handle retries gracefully, maintain data consistency, and provide a seamless user experience.

