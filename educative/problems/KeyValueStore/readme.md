# key-value store

## 🏗 Introduction to Key-value Stores
Key-value stores are **distributed hash tables (DHTs)** where a **key is generated** using a hash function and mapped to a specific value.  
**Key Points:**
- The key is **unique** and **does not assume structure** for the value.
- Values can be **blobs, images, server names**, or any stored data.
- Keeping values **small (KB to MB)** is preferred.
- **Large data** can be stored separately, referencing its location in the value field.

### 🌍 Use Cases of Key-value Stores
Key-value stores are useful for:
- **User session management** in web applications.
- Building **NoSQL databases** for scalable solutions.
- **Primary-key access** for large services (e.g., Amazon, Facebook, Netflix).
- Storing **bestseller lists, shopping carts, preferences, session data**, etc.

### ⚖️ Traditional RDBMS vs. Key-value Stores
While relational databases offer **rich programming models**, they may not be **cost-effective** for simple use cases.  
**Key Considerations:**
- **Scaling RDBMS** with **strong consistency** is **challenging**.
- **High availability** is critical in distributed systems.
- Using RDBMS for applications that don’t require **complex relations** is **costly**.

### 🏗 How to Design a Key-value Store?
The design process is divided into **four key lessons**:
1. **API Definition** - Understanding how the key-value store functions.
2. **Scalability & Replication** - Using **consistent hashing** and partition replication.
3. **Versioning & Configurability** - Handling **conflicts** and adapting storage options.
4. **Fault Tolerance & Failure Detection** - Ensuring **system reliability**.

### 📜 Conclusion
Key-value stores are **powerful solutions** for storing **structured data efficiently** in distributed environments.  
They **optimize scalability**, **enhance system availability**, and **support high-performance applications**.

---



## 🔑 Design of a Key-value Store
Learn about the **functional and non-functional requirements** and the **API design** of a key-value store.

### 📋 Requirements
Key-value stores are designed to **overcome traditional database limitations**.

#### ✅ Functional Requirements
Key-value stores generally offer `get` and `put` functions, but additional features include:
- **Configurable service**: Allowing applications to trade **consistency** for **higher availability**.
- **Always-write capability**: Ensures availability (based on **CAP theorem**).
- **Hardware heterogeneity**: Supporting **different capacity servers** within the cluster.

#### ⚙️ Non-functional Requirements
- **Scalability**: Should handle **thousands of servers globally**.
- **Fault tolerance**: Ensures **continuous operation** despite **server failures**.

### 🧐 Why Use Multiple Servers?
A single-node hash table **cannot meet** storage and query needs.  
Using **multiple servers** prevents **system downtime** and **storage limitations**.

### 🔍 Assumptions
To **simplify the design**, we assume:
- **Trusted data centers** host the service.
- **Authentication & authorization** are already completed.
- **User requests are secured** via HTTPS.

### 🛠 API Design
Key-value stores provide **two core functions**:

#### 🔄 Get Function
Fetches stored values using the `get(key)` API.

```plaintext
get(key) -> value
```
- **If data is replicated**, multiple values may be returned under **eventual consistency**.

#### ➕ Put Function
Stores key-value pairs using the `put(key, value)` API.

```plaintext
put(key, value)
```
- The system **determines storage location** and maintains **metadata** (such as **versioning**).

### 🔐 Data Integrity
For **data integrity checks**, hashes are stored either **before or after compression/encryption**.  
It must be **consistent** across `put` and `get` operations.

### 🔢 Data Type
- **Key**: Typically a **primary key**.
- **Value**: Can be **any binary data**.

### 🌍 Distributed Hashing in Dynamo
- Dynamo uses **MD5 hashing** to generate a **128-bit identifier** for keys.
- These identifiers **help allocate** data to specific **server nodes** efficiently.

### 🚀 Next Steps
The next lesson covers:
- **Scalability & replication** strategies.
- **Versioning & fault tolerance** to ensure system stability.

## 🚀 Ensure Scalability and Replication
Learn how **consistent hashing** enables **scalability** and how we efficiently **replicate partitioned data**.

### 📈 Add Scalability
Scaling a **key-value store** involves **partitioning data** across nodes.

**Key Points:**
- We store key-value data in **storage nodes**.
- Nodes need to be added or removed **based on demand**.
- Load distribution is crucial for **balancing traffic**.
- A simple solution: **Modulus operation** (`hash(key) % number_of_nodes`) assigns requests to nodes.

#### ⚠️ Limitations of Modulus-based Partitioning
- **Adding/removing nodes** disrupts key assignments.
- Large-scale **replication costs** increase **latency**.
- Requires **redistributing many keys** upon node failure.

### 🔄 Consistent Hashing
Consistent hashing is an **efficient method** for managing distributed workloads.

**Concept:**
- We model a **conceptual ring** of hashes from `0` to `n-1`.
- Nodes and keys are mapped to **specific positions** in the ring.
- The next node in a **clockwise direction** processes the request.
- Adding new nodes **affects only the immediate next node**, preventing large-scale disruption.

### 📊 Load Balancing Challenge
**Issue:** Some nodes may become **hotspots** (handling disproportionately large requests).  
**Solution:** Use **virtual nodes** for a more even distribution.

### 🌍 Virtual Nodes for Load Balancing
Instead of applying **one hash function**, we apply **multiple hashes** per node.

**Benefits:**
- **Uniform request distribution** across nodes.
- **Dynamic scalability**—nodes with greater **capacity** can handle more **virtual nodes**.
- Ensures **efficient failover** in case of node failure.

### 🔄 Data Replication Strategies
Replication ensures **high availability** and **data durability**.

#### 🏗 Primary-Secondary Approach
- A **primary node** handles **writes**.
- **Secondary nodes** replicate data and handle **reads**.
- **Single point of failure risk**—if the primary node fails, **writes are lost**.

#### 🤝 Peer-to-Peer Approach
- All nodes are **peers** and replicate data.
- Allows **read and write operations** on all nodes.
- Typically, replication occurs across **3 to 5 nodes** for efficiency.

### 🔁 Coordinator and Replication Factor
Each node **replicates data** across multiple hosts.

- A **coordinator** is assigned a key and **replicates it** to `n-1` successors.
- The **replication factor (n)** determines **how many nodes** store each key.
- Preference lists **ensure physical diversity**, avoiding storing multiple replicas on the same physical node.

### 🧐 Synchronous vs. Asynchronous Replication
- **Synchronous replication**: Guarantees **consistency**, but **slows writes**.
- **Asynchronous replication**: Prioritizes **availability**, but may cause **temporary inconsistencies**.

### 🔄 CAP Theorem Consideration
Key-value stores **favor availability** over **strong consistency**.

- If replication fails due to network partitions, nodes continue serving requests.
- Synchronization happens when the connection is restored.
- **Conflict resolution** mechanisms handle **data inconsistencies**.

### 🎯 Next Steps
Our next lesson covers:
- **Versioning** to resolve inconsistencies.
- **Configurable storage** for handling different workloads.

---

## 📌 Versioning Data and Achieving Configurability
Learn how to resolve conflicts via versioning and how to make the key-value storage into a configurable service.

### 🔄 Data Versioning
**When network partitions and node failures occur during updates**, an object’s version history might fragment, requiring reconciliation to avoid data loss.  
Handling multiple copies of data is crucial, as some failure scenarios lead to divergence. **Resolving these conflicts is critical for consistency.**

#### ✅ Steps in a Distributed System:
1. Two nodes replicate data while handling requests.
2. The network connection breaks.
3. Both nodes continue handling requests independently.
4. The connection is restored, but **data inconsistency** arises.

**Solution**: Maintain causality using timestamps or vector clocks.

### 🛠️ Modify the API Design
To handle causality in operations, we modify our API:
- **`get(key)`**: Retrieves object(s) along with metadata (`context`).
- **`put(key, context, value)`**: Stores objects while handling version conflicts.

### ⏳ Vector Clock Usage Example
A vector clock is a list of `(node, counter)` pairs that help determine causal relationships between objects.

#### 🖧 Scenario:
1. Node A writes the first version (`E1`) → Clock: `[A,1]`
2. Node A writes again (`E2`) → Clock: `[A,2]`
3. **Network partition occurs**, and requests are handled separately by nodes B and C.
4. Conflicting versions appear when the network restores.
5. **Client reconciliation** merges versions, forming a new clock `[A,3], [B,1], [C,1]`.

### ⚖️ Compromise with Vector Clock Limitations
Excessive vector clock sizes complicate storage and reconciliation.  
**Optimization**: Use timestamp-based clock truncation to remove older entries when the vector exceeds a threshold.

### 🔁 The `get` and `put` Operations
In a configurable system, **availability, consistency, cost-effectiveness, and performance must be balanced.**

#### 📌 Node Selection:
1. **Load balancer routing**: Generic approach.
2. **Partition-aware client**: Direct routing with lower latency.

#### 🔢 Using `r` and `w` for Configurability:
- **`r`**: Minimum nodes needed for read success.
- **`w`**: Minimum nodes needed for write success.

✅ Ensuring consistency: **`r + w > n`**

| **n** | **r** | **w** | **Effect** |
|------|------|------|-------------|
| 3    | 2    | 1    | ❌ Violates `r + w > n` |
| 3    | 2    | 2    | ✅ Allowed |
| 3    | 3    | 1    | 🏃‍♂️ Fast writes, slow reads |
| 3    | 1    | 3    | 📖 Fast reads, slow writes |

### 🔗 Replication Example:
If `n = 3`, data is replicated to nodes **A, B, and C**.
- Write operation updates **first two nodes synchronously**.
- **Third node updates asynchronously**.

### 🎯 Ensuring Scalability and Conflict Resolution
The system maintains multiple versions until reconciliation, prioritizing availability and configurability.

---

## 🛡️ Enable Fault Tolerance and Failure Detection

Learn how to make a key-value store **fault tolerant** and able to detect failure.

## 📋 We'll Cover the Following

- **Handle temporary failures**
- **Handle permanent failures**
- **Anti-entropy with Merkle trees**
- **Promote membership in the ring to detect failures**
- **Conclusion**

## 🔄 Handle Temporary Failures

Typically, distributed systems use a **quorum-based approach** to handle failures. A *quorum* is the minimum number of votes required for a distributed transaction to proceed. If a server is part of the consensus and is down, then the operation cannot proceed, affecting the **availability and durability** of the system.

A **sloppy quorum** is used instead of strict quorum membership. Usually, a leader manages communication among participants, who send acknowledgments after a successful write. The leader then responds to the client. However, if the leader is temporarily down and participants can't reach it, they declare the leader dead, triggering a new leader election. **Frequent elections negatively impact performance** as the system spends more time electing leaders than doing actual work.

In a sloppy quorum, the first $$ n $$ healthy nodes from the preference list handle all read and write operations. These may not always be the first $$ n $$ nodes discovered in the consistent hash ring.

**Example with $$ n=3 $$:**  
If node **A** is briefly unavailable during a write, the request is sent to the next healthy node (e.g., node **D**). Node **D** includes a *hint* indicating the intended receiver (**A**). Once **A** is back, **D** sends the request information to **A** for data update. After transfer, **D** removes the item from its storage, maintaining the total number of replicas.

**Preference List:** $$[A, D, C, B, G, E]$$  
If node **A** is down, the next node in the list handles the request.  
This approach is called a **hinted handoff**, ensuring reads and writes are fulfilled even if a node faces temporary failure.

> **Note:** A highly available storage system must handle data center failures (power outages, cooling, network, disasters). **Replication across data centers** is essential for recovery.

**Point to Ponder**

### ❓ Question

**What are the limitations of using hinted handoff?**

**Answer:**  
Hinted handoff works best with minimal churn and transient node failures. However, **hinted replicas may become unavailable before being restored to the originating node** in some cases.

## 🏚️ Handle Permanent Failures

In the event of **permanent node failures**, replicas must be synchronized to maintain durability. To detect inconsistencies quickly and reduce data transfer, **Merkle trees** are used.

A **Merkle tree** hashes individual keys as leaves, with parent nodes containing hashes of their children. Each branch can be verified independently, so nodes do not need to download the entire dataset for verification. If the root hashes of two trees are the same, their data is consistent. Otherwise, nodes recursively compare child hashes to find differences and synchronize as needed.

Merkle trees **reduce data transmission** and the number of disk accesses during synchronization (**anti-entropy** process).

**Merkle Tree Operations:**

- Hashes of child nodes are calculated and stored in parent nodes.
- If a value (e.g., $$ K_2 $$) is updated, its hash and all parent hashes up to the root are recalculated.
- Each node keeps a Merkle tree for each key range it hosts.
- Nodes exchange root hashes for common key ranges and only traverse branches with differences.

**Example Range Mapping:**

| Node A (Virtual Node) | Range         | Node B (Virtual Node) | Range         |
|-----------------------|---------------|-----------------------|---------------|
| N1                    | [5+1, 5]      | N2                    | [0, m]        |
| N3                    | [m+1, n]      | N4                    | [n+1, o]      |
| N5                    | [o+1, p]      | N6                    | [p+1, q]      |
| ...                   | ...           | N7                    | [q+1, r]      |

**Advantages:**  
Each branch can be examined independently, reducing synchronization data and disk access.

**Disadvantages:**  
When a node joins or leaves, **multiple key ranges are affected**, requiring tree hash recalculation.

## 👥 Promote Membership in the Ring to Detect Failures

Nodes may go offline temporarily or permanently. **Partition rebalancing or replica fixes should be done cautiously**-not every node departure is permanent.

**Membership changes** (node addition/removal) are recorded persistently and reconciled among ring members using a **gossip protocol**. This protocol maintains an **eventually consistent view of membership** by synchronizing histories when nodes randomly choose peers.

**Gossip Protocol Example:**

- Node **A** starts up, adds **B** and **E** to its token set, and stores this info locally.
- When **A** handles a change, it communicates with **B** and **E**.
- Other nodes do the same, ensuring all nodes eventually know about each other's status.
- This method is **efficient and bandwidth-friendly**.

### ❓ Question 1

**Can the gossip-based protocol fail in consistent hashing?**

**Answer:**  
Yes. For example, if two virtual nodes of the same physical node are unaware of each other, they may both consider themselves part of the ring, causing **logical partitioning**. The gossip protocol only works if all nodes are connected (single component). High churn or mapping issues can partition the network, preventing updates from reaching all nodes. Thus, **gossip alone is insufficient**; **network topology must remain connected**.

**Decentralized failure detection** uses gossip so each node learns about others' addition/removal. Nodes explicitly notify others when joining/leaving. Temporary failures are detected by failed communications; after a timeout, administrators are notified of dead nodes.

## 🏁 Conclusion

A **key-value store** offers flexibility and scalability for applications with unstructured data. It is ideal for **rapid reads and writes**, such as storing user sessions and preferences, and powering real-time recommendations and advertising due to swift data access and presentation.

