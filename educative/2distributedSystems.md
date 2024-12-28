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