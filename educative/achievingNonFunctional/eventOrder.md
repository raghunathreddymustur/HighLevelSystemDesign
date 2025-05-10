# Event Ordering

1. **Causality** – Establishing the sequence of events to determine dependencies (e.g., event A must happen before event B).
2. **Concurrent Events** – Events that occur independently with no causal relationship.
3. **Logical Clocks** – Using numerical counters rather than actual time to order events, ensuring proper sequencing.
    - **Lamport Clocks** – Provide happened-before relationships but lack a way to determine causal dependencies globally.
    - **Vector Clocks** – Maintain causal history by tracking the sequence of events across different nodes.
4. **Physical Clocks** – Using system clocks to establish ordering.
    - **Time-of-Day Clock** – Susceptible to drift and adjustments by Network Time Protocol (NTP).
    - **Monotonic Counters** – More stable but lack cross-system consistency.
5. **Unique Identifiers with Timestamps** – Assigning unique IDs that encode causality, such as:
    - **UNIX Time Stamps** – Granular to milliseconds but may not uniquely distinguish concurrent events.
    - **Twitter Snowflake** – Uses a combination of timestamps, worker IDs, and sequence numbers for ordering.
    - **TrueTime API** – Provides time intervals instead of precise timestamps, ensuring global synchronization.

These techniques help maintain order and consistency in distributed systems. Do you need more details on any specific method?