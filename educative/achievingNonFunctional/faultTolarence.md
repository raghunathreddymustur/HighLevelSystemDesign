# Fault Tolerance

## 🕑 Handling Temporary Failures

To address **temporary failures** in distributed systems, the approach shifts from strict quorum to a *sloppy quorum*. In a strict quorum, if any server involved in consensus is down, operations cannot proceed, impacting system availability and durability. A sloppy quorum, however, allows the first $$ n $$ healthy nodes from the preference list to handle all read and write operations, even if they are not the first $$ n $$ nodes in the consistent hash ring.

When a node (e.g., node A) is temporarily unavailable during a write, the system forwards the request to the next healthy node (e.g., node D). This node processes the request and stores a *hint* indicating the intended recipient. Once the original node is back online, the healthy node transfers the data back, after which it deletes the item from its local storage. This process, called **hinted handoff**, ensures that reads and writes are still fulfilled during temporary outages, maintaining the desired level of availability and durability.

**Key points:**
- **Sloppy quorum** allows healthy nodes to temporarily take over responsibilities.
- **Hinted handoff** ensures data eventually reaches its intended node when it recovers.
- This method is robust for brief outages but less effective if the hinted node or its replacement also becomes unavailable before recovery.
- **Replication across data centers** is recommended to recover from larger-scale failures like data center outages[1].

> **Limitation:** Hinted handoff is most effective with minimal churn and transient failures. If hinted replicas become unavailable before the original node is restored, data may be at risk[1].

## 🏚️ Handling Permanent Failures

For **permanent failures**, it is crucial to keep replicas synchronized to maintain system durability. The main tool for this is the **Merkle tree**, which enables efficient detection and reconciliation of inconsistencies between replicas.

A Merkle tree hashes individual keys as leaves, with parent nodes containing hashes of their children. When comparing replicas, nodes exchange the root hashes of their respective Merkle trees for a given key range. If the root hashes match, the data is consistent; if not, the comparison continues recursively down the tree to identify and synchronize only the differing branches.

**Key points:**
- **Merkle trees** allow independent verification of each branch, reducing the amount of data exchanged and minimizing disk accesses during synchronization.
- Each node maintains a Merkle tree for every key range it hosts.
- When a node joins or leaves, the affected key ranges require hash recalculation, which is a potential disadvantage[1].

> **Advantage:** Only inconsistent data is transferred, making synchronization efficient.
>
> **Disadvantage:** Node membership changes require recalculating hashes for multiple key ranges, which can be resource-intensive[1].

---

**Summary Table**

| Failure Type         | Approach           | Key Mechanism         | Notes/Limitations                                               |
|----------------------|--------------------|-----------------------|-----------------------------------------------------------------|
| Temporary Failure    | Sloppy quorum      | Hinted handoff        | Effective for short outages; less so if multiple nodes fail     |
| Permanent Failure    | Replica sync       | Merkle trees          | Efficient sync; hash recalculation needed on membership changes |[1]




