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

