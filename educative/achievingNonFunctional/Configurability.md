# Configurability

### 🔧 **Configurability in Distributed Systems**
Configurability is a key non-functional requirement that allows users to **fine-tune trade-offs** between availability, consistency, cost-effectiveness, and performance in a distributed system.

#### 📌 **Configurable API Design**
The system modifies its API to support version tracking and conflict resolution:
- **`get(key)`**: Retrieves objects along with metadata (`context`), which includes version details.
- **`put(key, context, value)`**: Stores objects while handling version conflicts using vector clocks.

#### 🔢 **Using `r` and `w` for Configurability**
The system allows users to configure read (`r`) and write (`w`) parameters to balance consistency and availability:
- **`r`**: Minimum nodes needed for a successful read.
- **`w`**: Minimum nodes needed for a successful write.

✅ Ensuring consistency: **`r + w > n`**, where `n` is the total number of replicas.

| **n** | **r** | **w** | **Effect** |
|------|------|------|-------------|
| 3    | 2    | 1    | ❌ Violates `r + w > n` |
| 3    | 2    | 2    | ✅ Allowed |
| 3    | 3    | 1    | 🏃‍♂️ Fast writes, slow reads |
| 3    | 1    | 3    | 📖 Fast reads, slow writes |

#### 🔗 **Replication Strategy**
If `n = 3`, data is replicated to nodes **A, B, and C**:
- Write operation updates **first two nodes synchronously**.
- **Third node updates asynchronously**.

### 🎯 **Why Configurability Matters**
Configurability ensures that the system can adapt to different workloads and failure scenarios:
- **High availability**: Prioritizing quick responses over strict consistency.
- **Strong consistency**: Ensuring all nodes have the latest data before confirming operations.
- **Optimized performance**: Reducing latency by selecting appropriate read/write parameters.

