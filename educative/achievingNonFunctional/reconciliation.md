# Reconciliation

Vector clocks help resolve versioning issues in distributed systems by maintaining causality between events and identifying conflicting versions of data.

### 🔄 How Vector Clocks Solve Versioning Issues
When a network partition or node failure occurs, multiple versions of the same object might exist across different nodes. **Vector clocks provide a structured way to track these versions and determine their causal relationships.**

#### 🖧 Step-by-Step Process:
1. **Initial Write:** A node (e.g., Node A) processes the first version (`E1`), and the vector clock starts as `[A,1]`.
2. **Subsequent Write:** Another write request (`E2`) updates the object, increasing the counter to `[A,2]`.
3. **Network Partition Occurs:** Separate nodes (`B` and `C`) handle new requests independently.
4. **Divergent Versions Appear:** The vector clocks for these versions become `[A,2], [B,1]` and `[A,2], [C,1]`, indicating they evolved separately.
5. **Network Restored:** When connectivity resumes, the system detects conflicts and returns all diverging versions.
6. **Client Reconciliation:** The system requires the client to merge the versions into a unified state.
7. **Final Update:** The merged version gets a new vector clock `[A,3], [B,1], [C,1]`, preserving history and resolving inconsistencies.

### ⚖️ Why Vector Clocks Are Effective
- **Causality Tracking:** Vector clocks maintain event order, ensuring updates don’t overwrite unrelated changes.
- **Conflict Detection:** If two versions have distinct vector clocks, they are considered conflicting.
- **Efficient Resolution:** Clients merge conflicting versions manually or through automatic reconciliation methods.

However, vector clocks can grow in size when multiple servers handle updates simultaneously. **A truncation strategy helps limit excessive growth by removing older entries based on timestamps.**

The main **non-functional requirements** achieved in this page are:

### 🛠️ **Scalability**
The system is designed to handle increasing data volumes efficiently. Vector clocks allow version reconciliation without performance bottlenecks.

### 🔄 **Consistency**
By using vector clocks and a reconciliation strategy, the system ensures that multiple versions of the same object are properly merged to avoid inconsistencies.

