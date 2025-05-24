# Blob Store

## 📦 What is a Blob Store?
Blob store is a **storage solution for unstructured data**. It can store **photos, audio, videos, binary executable codes, or other multimedia items**. Every type of data is stored as a blob, following a **flat data organization pattern** without hierarchies like directories and sub-directories.

Mostly, applications use it with a **write once, read many (WORM) requirement**, meaning data is written once and cannot be modified. **Blobs can’t be deleted until a specified interval** and are read multiple times to protect critical data.

⚠️ **Note:** Not all applications require WORM. If modification is needed, **a new version of the blob can be uploaded** instead.

## 🎯 Why Do We Use a Blob Store?
Blob store is an essential component of **data-intensive applications like YouTube, Netflix, and Facebook**, which generate a **huge amount of unstructured data daily**. These applications need **scalable, reliable, and highly available storage solutions**.

Since **data volume increases continuously**, these applications must store **an unlimited number of blobs**. For example, **YouTube requires more than a petabyte of additional storage per day**. Videos are stored in multiple resolutions and **replicated across different data centers** for availability.

### 🔍 Blob Store Systems in Use:
| **System** | **Blob Storage Used** |
|------------|----------------------|
| **Netflix** | S3 |
| **YouTube** | Google Cloud Storage |
| **Facebook** | Tectonic |

## 🛠️ How Do We Design a Blob Store System?
The design of a **blob store system** is divided into five key lessons and a quiz:

### ✅ Requirements
- Identify **functional and non-functional requirements**.
- Estimate the **resources needed** for the blob store system.

### 📐 Design
- **High-level design and API design**.
- **Detailed design explaining components and workflow**.

### ⚙️ Design Considerations
- **Database schema, partitioning strategy, blob indexing, pagination, and replication**.

### 📊 Evaluation
- Assess the **blob store based on identified requirements**.

## 📌 Requirements of a Blob Store's Design
Understand the **functional and non-functional requirements** of a blob store system and estimate the necessary resources.

## 🎯 Functional Requirements
Here are the functional needs for a blob store:
- **Create a container**: Users should be able to **group blobs** within separate containers, such as storing user-specific data separately or categorizing videos and images.
- **Put data**: The system must support **blob uploads** to containers.
- **Get data**: Each blob should have a **generated URL** for retrieval.
- **Delete data**: Users must be able to **delete blobs**, with optional retention periods.
- **List blobs**: The ability to **fetch a list** of blobs within a container.
- **Delete a container**: Users can **delete a container along with its blobs**.
- **List containers**: The system should **list all containers** under a user account.

## 🏗️ Non-Functional Requirements
Key attributes for system performance:
- **Availability**: The system must be **highly accessible**.
- **Durability**: Uploaded data should **not be lost** unless explicitly deleted.
- **Scalability**: Must be capable of **handling billions of blobs**.
- **Throughput**: Should ensure **high data transfer rates** for efficiency.
- **Reliability**: Must **detect and recover** from failures promptly.
- **Consistency**: Ensures a **strongly consistent view** across users.

## 🔢 Resource Estimation
Estimating storage, bandwidth, and server requirements for a blob store using **YouTube data as an example**.

### 🖥️ Number of Servers Estimation
Formula for estimating required servers:


\[
\frac{Number\ of\ active\ users}{Queries\ handled\ per\ server} = 10,000\ servers
\]



### 💾 Storage Estimation
Computing **total storage per day** using assumptions:


\[
Total\ storage/day = Number\ of\ videos/day \times (Storage\ per\ video + Storage\ per\ thumbnail)
\]


Using the given data, this results in **12.51 TB/day** of storage needed.

### 🔗 Bandwidth Estimation
Estimating **incoming and outgoing bandwidth**:
- **Incoming traffic**: Based on data uploads, requiring **1.16 Gbps**.
- **Outgoing traffic**: Read-intensive operations need **462.96 Gbps**.

## 🛠️ Building Blocks of a Blob Store
Components essential to a blob store system:
- **Rate Limiter**: Controls **user interaction frequency**.
- **Load Balancer**: Distributes requests **across servers**.
- **Database**: Stores **metadata information** for blobs.
- **Monitoring**: Tracks **storage usage** and availability.

---

Here’s your formatted **README.md** with level two headings, meaning icons for clarity, and highlighted key sections to enhance readability:


## 🔍 High-Level Design of a Blob Store
At a high level, a blob store consists of the following components:
- **Clients**: End-users or programs making requests.
- **Front-end servers**: Process and forward client requests.
- **Storage disks**: Store blobs efficiently.

### 📜 How It Works
The **client sends a request** to the front-end servers. These servers **process the request** and store the blobs on **attached storage disks**.

## 🔌 API Design
The blob store provides multiple **APIs for registered and authenticated users**. Here’s an overview of core functionalities:

### 🏗️ Create a Container
Creates a **new container** under the logged-in account.

```md
createContainer ( containerName )
```
- **containerName**: Should be **unique** within a storage account.

### 📤 Upload a Blob
Stores **user data as a blob** within a container.

```md
putBlob ( containerPath, blobName, data )
```
- **containerPath**: Path to the container (includes account ID and container ID).
- **blobName**: Should be **unique** within the container.
- **data**: File to upload.

⚠ **Note**: If the blob name isn't unique, the system assigns a **version number** to differentiate uploads.

### 📥 Download a Blob
Retrieves **blob data** using a unique ID.

```md
getBlob ( blobPath )
```
- **blobPath**: Fully qualified path to the blob.

### 🗑️ Delete a Blob
Marks a blob for **deletion**.

```md
deleteBlob ( blobPath )
```
- **blobPath**: Path of the blob to delete.

### 📜 List Blobs
Fetches a **list of blobs** from a container.

```md
listBlobs ( containerPath )
```
- **containerPath**: Path to the container.

### 🏗️ Delete a Container
Marks a container for **deletion**, including all blobs inside it.

```md
deleteContainer ( containerPath )
```
- **containerPath**: Path to the container.

### 📂 List Containers
Retrieves a **list of containers** under the user’s account.

```md
listContainers ( accountID )
```
- **accountID**: User ID for listing containers.

## ⚙️ Detailed Design
### 🔑 Key Components
- **Clients**: Perform API operations.
- **Rate limiter**: Limits excessive API calls.
- **Load balancer**: Distributes network traffic.
- **Front-end servers**: Handle requests.
- **Data nodes**: Store actual blob data.
- **Manager node**: Manages storage paths and access privileges.
- **Metadata storage**: Stores blob, container, and account metadata.
- **Monitoring service**: Tracks storage usage and detects failures.
- **Administrator**: Ensures system reliability.

### 🔄 Workflow for Blob Operations
#### ✍️ Writing a Blob
1. **Client sends a request** to upload a blob.
2. **Rate limiter checks** the request validity.
3. **Load balancer forwards** the request to front-end servers.
4. **Front-end server contacts the manager node** to determine storage locations.
5. **Blob is split into chunks** and distributed among data nodes.
6. **Metadata is updated** with blob storage details.
7. **Client receives the blob path** for future retrieval.

#### 📝 Reading a Blob
1. **Client requests blob retrieval**.
2. **Front-end server queries the manager node** for metadata.
3. **Manager node checks access privileges** (private/public).
4. **Manager node returns chunk locations**.
5. **Client reads blob chunks from data nodes**.

🔹 **Metadata caching accelerates repeat reads**, reducing manager node workload.

#### 🗑️ Deleting a Blob
1. **Manager node marks blob as deleted**.
2. **Blob data is freed later** using garbage collection.

⚠ **Backup and Recovery**: A shadow server maintains **snapshots** of the manager node for recovery.

---

## 📜 Introduction
Even though we discussed the design of the **blob store system** and its major components in detail, several important questions remain unanswered:
- **How do we store large blobs?** Do we store them on the same disk or divide them into chunks?
- **How many replicas** of a blob should exist to ensure **reliability and availability**?
- **How do we efficiently search for blobs**?

These questions are addressed in this lesson.

## 📂 Blob Metadata
Every blob has metadata that ensures **efficient storage and retrieval**. When a blob is uploaded:
- It is **split into small-sized chunks** for handling large files.
- Chunks are stored across **different data nodes**, optimizing storage usage.
- **Manager node assigns IDs** to chunks and tracks storage locations.
- **Replication ensures fault tolerance**, maintaining multiple copies.

⚠ **Choosing a reasonable chunk size is critical.**
- **Small chunks increase metadata size**—this is inefficient for a **single manager-based design**.
- **Large chunks can reduce read/write performance** due to fragmented disk allocation.

## 🗂️ Partitioning Data
To prevent slow data retrieval, blobs are grouped into **partitions** rather than searching across **billions of blobs**.
- **Problem:** If blobs are distributed **independently**, fetching **user-specific blobs** requires checking multiple partitions.
- **Solution:** Partition blobs **based on their complete path** (account ID, container ID, and blob ID). This ensures a **user’s blobs are stored in the same partition**, improving performance.

## 🔍 Blob Indexing
Searching through a massive blob store can be slow. **Blob indexing** solves this by:
- Allowing **key-value tagging** (e.g., container name, blob name, upload date).
- Using an **indexing engine** to store tags, making queries efficient.
- Sorting blobs **in advance** when storing them, speeding up **pagination**.

## 📜 Pagination for Listing
Since users often request long blob lists, pagination optimizes retrieval:
- Instead of fetching all blobs **at once**, they are **listed in parts**.
- **Indexing ensures sorted results**, improving the retrieval process.
- A **continuation token** allows users to **resume listing** from the last retrieved blob.

## 🏷️ Replication Strategy
Replication enhances **availability and consistency**:
1. **Synchronous replication** occurs **within a storage cluster**, ensuring immediate redundancy.
2. **Asynchronous replication** spreads data **across multiple data centers and regions**.

⚠ **Data consistency vs. availability tradeoff:**
- **Synchronous replication ensures consistency** but increases **write latency**.
- **Asynchronous replication enhances availability**, preventing regional data loss.

## 🗑️ Garbage Collection for Deletion
Instead of **instantly removing blobs**, deletion is handled efficiently:
- Blob is **marked as DELETED** in metadata but **not erased immediately**.
- **Garbage collector** removes old metadata inconsistencies later.
- **Storage space increases gradually**, ensuring **fast delete operations**.

⚠ **Optimized deletion prioritizes user experience.**
- **Immediate deletion can cause slow responses**—hence, metadata marking speeds up the process.
- **Actual removal happens asynchronously**, freeing storage without performance impact.

## 📡 Streaming Files
For streaming:
- Files are read in **small chunks** rather than **entirely at once**.
- An **offset tracks** previously read **bytes**, ensuring smooth playback.

## 🚀 Blob Store Caching
Caching enhances **response time and throughput**:
- **Client-side caching** prevents redundant metadata lookups.
- **Front-end servers cache partition maps**, reducing routing delays.
- **Manager node caches frequently accessed blobs**, speeding up large object streaming.

⚠ **Azure Blob Storage integrates with a CDN** to cache **public blobs**, ensuring **fast global access**.

---


## 📜 Evaluation of a Blob Store's Design
Examining how our **blob store design** fulfills its key requirements.

## 🌍 Availability
The **replication strategy** ensures system availability.
- **For read operations**, we maintain **four replicas per blob**, distributing request loads.
- **Failure resilience**: If one node fails, **replica nodes step in** to handle requests.
- **Regional availability**: Replica placement strategies **safeguard data** against natural disasters.
- **Monitoring service**: Constantly verifies replica count—**new copies are created** if failures exceed a threshold.
- **Write operations**: Data replication within **fault-tolerant clusters** ensures **fast user responses**.
- **Manager node backup**: A **saved state** allows quick recovery from **manager-node failure**.

## 🔐 Durability
Replication and monitoring ensure **data remains intact**.
- **Synchronous replication** across storage clusters **preserves uploaded blobs**.
- **Fault-tolerance**: Lost data on one node can be **recovered from replicas**.
- **Disk monitoring**: Alerts administrators when storage **disks fail**.
- **Automatic recovery**: Failed disk contents are **copied to alternative disks**, keeping metadata updated.

## 🚀 Scalability
Design elements that enable **handling billions of blob requests**.
- **Partitioning system** groups blobs into distinct **ranges**, preventing bottlenecks.
- **Load balancing**: Automated **distribution of requests** across partition servers.
- **Horizontal scalability**: **Adding data nodes increases storage** capacity.
- **Manager node limitations**: A **single instance supports up to 10,000 QPS**. Further scaling requires **independent system instances**.

⚠ **Scaling beyond a single instance requires a new design approach.**

## ⚡ Throughput
Optimizing read/write speeds with **parallel processing**.
- **Chunks are stored on multiple nodes**, allowing parallel retrieval.
- **Multi-layer caching** (client-side, front-end servers, manager node) **reduces latency**.
- **Fetching chunks concurrently enhances speed**.

## 🔄 Reliability
Ensuring system **stability and fault detection**.
- **Heartbeat protocol** allows **manager node to verify active data nodes**.
- **Node failure handling**: If a node fails, a **new replica is created** to maintain reliability.
- **Hardware monitoring**: Alerts administrators about **failed disks, network links, and switches**.
- **Storage tracking**: Low available space **triggers disk expansion alerts**.

## 🔁 Consistency
Maintaining **data correctness** across storage clusters.
- **Write operations** ensure **strong consistency** using **synchronous replication** inside clusters.
- **Read operations** use **the same storage cluster** for consistent responses.
- **Asynchronous replication** expands availability but **ensures consistency after write operations**.

## 🏁 Conclusion
We designed a blob store system to handle **large-scale unstructured data storage**, ensuring reliability, scalability, durability, and performance. Popular platforms like **YouTube, Facebook, Instagram, and Twitter** rely on such architectures.

---
