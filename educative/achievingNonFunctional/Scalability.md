# Scalability

## Consistent Hashing

Scalability in key-value stores is achieved using **consistent hashing**, **virtual nodes**, and **efficient replication** strategies.

1. **Consistent Hashing**: Instead of using a modulus operation that requires reassigning many keys when nodes change, **consistent hashing** maps nodes and keys onto a conceptual ring. This ensures **minimal key movement** when nodes join or leave, making scaling more efficient.

2. **Virtual Nodes for Load Balancing**: Some nodes may receive **disproportionate traffic**, creating hotspots. Using **virtual nodes**, multiple hash functions place each node in **different positions** on the ring, distributing the load **more evenly**.

