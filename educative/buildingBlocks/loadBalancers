# Load Balancer

## 📘 Introduction to Load Balancers

Learn about the basics of load balancers and the **services offered** by them.

### 🔄 What is Load Balancing?
Millions of requests could arrive per second in a typical data center. To serve these requests, thousands (or even a hundred thousand) servers work together to share the load.
**Note:** It’s important to consider how the incoming requests are divided among all the available servers.

A **load balancer (LB)** is the answer—it fairly distributes all clients’ requests among the pool of available servers. This prevents any single server from getting overloaded or crashing. The load balancing layer acts as the first point of contact within a data center right after the firewall.

While a load balancer might not be required for a few hundred or even a few thousand requests per second, for increasing client requests it provides key capabilities such as **scalability**, **availability**, and **performance**:
- **Scalability:** By adding servers, the capacity of the application or service can be increased seamlessly. The upscaling or downscaling is transparent to the end users.
- **Availability:** Even if some servers fail, the system remains available as load balancers hide faults and failures.
- **Performance:** Load balancers forward requests to servers with a lesser load, giving users quicker response times and improved resource utilization.

---

## 🎭 Abstract Depiction of Load Balancer Operation

Here’s an abstract depiction of how load balancers work:

- **Servers Involved:**
  - Server 1
  - Server 2
  - Server 3

- **Users Impacted:**
  - User 1
  - User 2
  - User 3
  - User 4

- **Central Role:**
  - The **load balancer** directs incoming requests to the proper **server pool**.

This simplified illustration demonstrates the core concept of how load balancers distribute traffic from multiple users across multiple servers.

---

## 📍 Placing Load Balancers

Generally, LBs sit between **clients and servers**, serving as the gateway through which requests pass to and from servers via the load balancing layer.

However, load balancers are not only used at the network edge; they can be strategically placed between different groups of servers. In a three-tier architecture—for example, involving web, application, and database servers—the load balancers can be positioned as follows:

- **Between end users and web servers/application gateways.**
- **Between web servers and application servers** that run the business or application logic.
- **Between application servers and database servers.**

These placements ensure traffic is efficiently balanced across all layers, optimizing both performance and reliability.
**Note:** In practice, load balancers can be used between any two services with multiple instances.

---

## 🛠 Services Offered by Load Balancers

Load balancers not only ensure that services are **scalable**, **available**, and **highly performant** but also offer several specialized functions:

- **Health Checking:** Regular use of the heartbeat protocol monitors the health (and therefore the reliability) of end-servers, leading to an improved user experience.
- **TLS Termination:** By handling TLS termination with the client, load balancers alleviate the processing burden on end-servers.
- **Predictive Analytics:** Through analytics, LBs can predict traffic patterns by analyzing current traffic or historical data.
- **Reduced Human Intervention:** Automation in load balancing minimizes the need for manual system administration during failures.
- **Service Discovery:** Clients’ requests are directed to the appropriate hosting servers by inquiring about the service registry.
- **Security:** Load balancers help mitigate attacks like denial-of-service (DoS) at various layers of the OSI model (layers 3, 4, and 7).

Together, these services provide overall **flexibility**, **reliability**, **redundancy**, and **efficiency** in system design.

---

## 🤔 Food for Thought: What if Load Balancers Fail?

A common question to ponder is: **What if load balancers fail? Are they a single point of failure (SPOF)?**

Typically, load balancers are deployed in pairs or in clusters for disaster recovery. This arrangement ensures that if one load balancer fails, the backup is ready to take over immediately. Enterprises use heartbeat communication between units to monitor their health. If the primary LB fails, its backup assumes control, and in emergencies—if an entire cluster fails—manual rerouting can be performed to maintain service availability.

---

## 🌍 Global and Local Load Balancing

### 📌 Introduction
From the previous lesson, it may seem like **load balancing is performed only within the data center**. However, load balancing is required at both **global and local** scales.

### 🌎 Global Server Load Balancing (GSLB)
**GSLB distributes traffic load across multiple geographical regions**. It ensures that globally arriving traffic load is intelligently forwarded to a data center.

For example, **in case of power or network failure**, all traffic is rerouted to another data center. **GSLB takes forwarding decisions based on users’ geographic locations, the number of hosting servers in different locations, and the health of data centers**.

👉 **GSLB can be installed on-premises or obtained through Load Balancing as a Service (LBaaS)**.

### 🏢 Local Load Balancing
This refers to **load balancing within a data center**, focusing on **improving efficiency and resource utilization** of hosting servers.

Each **local load balancing layer** within a data center maintains a **control plane connection** with the GSLB, providing information about the health of the load balancers and the server farm.

### 🖥️ GSLB and DNS
**DNS can perform GSLB** by responding with **multiple IP addresses** for a single domain name query. Using a simple technique, **DNS reorders the list of IP addresses** in response to each query.

#### 🔄 Round-Robin DNS Load Balancing
Round-robin DNS distributes **user requests to different data centers in a strict circular order**.

Example:
1. A user from **ISP 1** requests the **DNS infrastructure** for an IP address.
2. DNS responds with **Data Center 1's IP address**.
3. The user is served at **Data Center 1**.
4. A user from **ISP 2** requests the same service.
5. DNS responds with **Data Center 2’s IP address**.
6. The user is served at **Data Center 2**.

#### ⚠️ Limitations of Round-Robin DNS
- **Different ISPs have different user numbers**, leading to uneven distribution.
- **Doesn't consider end-server crashes**, distributing IP addresses of crashed servers until TTL expires.
- **Service availability might be impacted**.

🔹 **Despite limitations, round-robin is widely used, and DNS uses short TTL to improve load balancing**.

### 🚀 Alternative GSLB Solutions
✅ **Application Delivery Controllers (ADCs)**
ADCs are part of the **Application Delivery Network (ADN)**, acting as **a superset of load balancers**.

Key functions:
- **Web acceleration**
- **Caching**
- **SSL offloading**
- **Reverse proxy**
- **Traffic optimization**

### 🔍 Why Local Load Balancers Are Needed
While **DNS plays a vital role**, it suffers from certain **limitations**:
- **Small DNS packet size** (512 Bytes) can't include all possible IP addresses.
- **Limited control** over client selection.
- **Recovery from failures is slow** due to caching.

👉 **Local load balancers** reside within a **data center** and act as **reverse proxies**, optimizing incoming traffic distribution.

### ❓ Point to Ponder
Can **DNS be considered a Global Server Load Balancer (GSLB)?**
✅ **Yes**! There are two ways of implementing **Global Traffic Management (GTM)**:
1. **Through ADCs**, which forward requests **based on health and capacity**.
2. **Through DNS**, which forwards requests **based on geographic proximity**.

---
## ⚖️ Advanced Details of Load Balancers

### 📌 Introduction
Understanding load balancers and their usage within a system. This lesson covers **well-known load balancing algorithms** and how load balancers are connected **in a hierarchical structure** across different tiers.

## 🔄 Algorithms of Load Balancers
Load balancers distribute client requests based on different **scheduling algorithms**. Some notable ones include:

### 🔁 Round-Robin Scheduling
Each request is forwarded to a server in a **repeating sequential manner**, ensuring an **equal distribution** of client loads.

### ⚖️ Weighted Round-Robin
When **some servers have higher capacity**, they get assigned a **greater weight**, resulting in **more requests being forwarded to those servers**.

### 📉 Least Connections
Newer arriving requests are assigned to **servers with fewer active connections**, ensuring **balanced loads** when requests vary in complexity.

### ⏳ Least Response Time
In performance-sensitive services, requests are forwarded to the **server with the fastest response time**.

### 🔑 IP Hash
Client requests are assigned to servers based on **their IP address hash**, ensuring **consistent routing** for certain users.

### 🌐 URL Hash
When certain services must be routed to **specific servers**, URL hashing helps **assign users to the appropriate backend**.

## 📌 Static vs Dynamic Algorithms
Algorithms can be classified as **static or dynamic** depending on whether they account for the current system state.

### 🏗️ Static Algorithms
- **Do not consider real-time changes in server states**.
- **Assignments are based on pre-existing server configurations**.
- **Simpler implementation, works well for commodity machines**.

### 🔄 Dynamic Algorithms
- **Consider the live state of servers** for better decisions.
- **Require communication between load balancers**, increasing overhead.
- **Enhance forwarding precision but add complexity**.

🚀 **Dynamic algorithms offer better efficiency** by maintaining **real-time server health status**.

## 🗂️ Stateful vs Stateless Load Balancers

### 🔄 Stateful Load Balancing
- **Maintains session information between clients and hosting servers**.
- **Uses a mapping structure for routing requests efficiently**.
- **Higher complexity but ensures better tracking** of client-server communication.

### ⚡ Stateless Load Balancing
- **Does not store session information**, making it faster and more lightweight.
- **Uses consistent hashing** to forward requests.
- **May struggle with infrastructure changes**, requiring local states.

## 🌐 Types of Load Balancers

### 🛜 Layer 4 Load Balancers
- **Work at the transport layer** using TCP/UDP.
- **Ensure session persistence** for ongoing communication.
- **Faster processing compared to Layer 7 LBs**.

### 🖥️ Layer 7 Load Balancers
- **Operate at the application layer**, using HTTP headers, cookies, and URLs.
- **Perform smart routing based on application data**.
- **Provide additional services like rate limiting and TLS termination**.

🔹 **Layer 4 load balancers focus on speed, while Layer 7 prioritizes intelligence and adaptability**.

## 🏗️ Load Balancer Deployment Strategy

### 🏛️ Three-Tier Load Balancer Hierarchy
**Data centers typically use a multi-tiered load balancing structure**, as shown below:

1️⃣ **Tier-1 Load Balancers (DNS, ECMP routers)**
   - **Initial traffic distribution among load balancers**.
   - **Horizontal scalability** across paths.

2️⃣ **Tier-2 Load Balancers (Layer 4 TCP/UDP LBs)**
   - **Ensure packet consistency for connections**.
   - **Glue between tier-1 and tier-3 LBs**.

3️⃣ **Tier-3 Load Balancers (Layer 7 LBs)**
   - **Perform application-aware routing**.
   - **Reduce server burden** by handling protocol complexities.
   - **Perform health monitoring of backend servers**.

👉 **Each tier ensures better load balancing**, enabling scalability and efficient packet forwarding.

## ⚙️ Implementation of Load Balancers
Load balancers come in **different forms** depending on the needs:

### 🖥️ Hardware Load Balancers
- **Standalone devices** with dedicated performance.
- **Expensive and harder to configure**.
- **Higher maintenance and operational costs**.

### 💻 Software Load Balancers
- **Implemented on commodity hardware**, making them **cost-effective**.
- **Easier to configure and scale** compared to hardware LBs.

### ☁️ Cloud Load Balancers
- **Offered as Load Balancing as a Service (LBaaS)**.
- **Ideal for global traffic management** across multiple zones.
- **Provides real-time monitoring and predictive analytics**.

🔹 **Cloud-based solutions complement local LBs** and improve **global server load balancing (GSLB)**.

## 📌 Conclusion
Load balancers have evolved **from standalone hardware** into **cloud-based services**. They are **essential for enterprise applications**, ensuring:

✅ **Scalability and optimal traffic distribution**
✅ **Session persistence and fault tolerance**
✅ **Improved resource utilization and efficiency**

---
