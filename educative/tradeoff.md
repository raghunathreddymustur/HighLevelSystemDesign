# Trade-Offs

## CAP

### 📜 The CAP Theorem
The CAP theorem outlines an inherent trade-off in the design of distributed systems.

### 📜 Initial statement of the CAP theorem
It is impossible for a distributed data store to provide more than two of the following properties simultaneously: **consistency**, **availability**, and **partition tolerance**.

### 📜 Partition Tolerance
In a distributed system, there is always the risk of a network partition. If this happens, the system needs to decide either to continue operating and compromise **data consistency**, or stop operating and compromise **availability**.

### 📜 Final statement of the CAP theorem
A distributed system can be either **consistent** or **available** in the presence of a network partition.

### 📜 Proof
The system has two options during a network partition: fail one of the operations and break the **availability** property, or process both operations and break the **consistency** property.

### 📜 Importance of the CAP theorem
The CAP theorem forces designers of distributed systems to make explicit trade-offs between **availability** and **consistency**.

### 📜 Categorization of distributed systems based on the CAP theorem
Systems are usually classified into two basic categories: **CP** (Consistency and Partition tolerance) and **AP** (Availability and Partition tolerance). This classification depends on which property the system violates during a network partition.

### 📜 Trade-off between latency and consistency
When no network partition is present, there’s a trade-off between **latency** and **consistency**. To guarantee data consistency, the system will have to delay write operations until the data has been propagated across the system successfully, thus taking a latency hit.

## PACELC theorem

### 📜 PACELC theorem
The PACELC theorem states that in the case of a network partition (P), the system has to choose between **availability** (A) and **consistency** (C), but else (E), when the system operates normally, it has to choose between **latency** (L) and **consistency** (C).

### 📜 Categorization of distributed systems based on PACELC theorem
Each branch of the PACELC theorem creates two sub-categories of systems: **AP/EL** (Availability during partition, Latency during normal operation) and **CP/EC** (Consistency during partition, Consistency during normal operation). Most systems fall into the AP/EL or CP/EC categories.
