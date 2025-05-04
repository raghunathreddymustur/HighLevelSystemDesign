# Availability

## Key-value store 

### 🔄 **Availability in Key-Value Stores**
Availability in key-value stores refers to the system's ability to **serve requests reliably** even in the presence of **failures or network partitions**.

#### ✅ **Ensuring High Availability**
1. **Replication Strategies**
    - **Primary-Secondary Replication**: A primary node handles **writes**, while secondary nodes replicate data and handle **reads**.
    - **Peer-to-Peer Replication**: All nodes act as **peers**, allowing **read and write operations** on multiple nodes.
    - **Replication Factor (n)**: Determines how many nodes store each key, ensuring **durability** and **fault tolerance**.

2. **Handling Failures**
    - **Synchronous Replication**: Guarantees **strong consistency** but **slows writes**.
    - **Asynchronous Replication**: Prioritizes **availability**, allowing **fast writes** but may cause **temporary inconsistencies**.
    - **Hinted Handoff**: If a node is temporarily unavailable, another node **stores updates** and forwards them when the failed node recovers.

3. **CAP Theorem Consideration**
    - Key-value stores prioritize **availability** over **strong consistency**.
    - If replication fails due to network partitions, nodes continue serving requests.
    - Synchronization happens when the connection is restored, and **conflict resolution** mechanisms handle inconsistencies.

