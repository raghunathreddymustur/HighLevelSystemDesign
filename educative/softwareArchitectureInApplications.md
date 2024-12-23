# 🛠️ Quality Attributes

## 🔎 Intro
- Quality attributes (QAs) are measurable or testable properties of a software system that indicate how well it meets the needs of stakeholders.
- Architects must choose architectural styles and design elements that align with the desired quality attributes.
- An important point to note about a QA is that the property must be measurable or testable.
- Quality attributes are not only nonfunctional requirements of the system, but also include service-level agreements and other concerns as well.

## 📌 Architecturally Significant Quality Attributes

- These QAs may be used to narrow our attention to the essential issues that our design must address. Based on our needs, we may or may not need to take into account every single quality aspect.
- Every application design, for example, must consider security and speed, but not every design must include interoperability. We need to understand our needs so that we can determine which characteristics are critical.

## 🌟 Important QAs

| QA            | Description                                                                 | How to Test It                                                                                       |
|---------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| Availability  | Defined as the proportion of time that the system is up and working         | Can be measured as a percentage of total system downtime over a predefined time period               |
| Maintainability | Defined as the ability to undergo changes as required                      | Can be measured by calculating the time it takes to undergo the changes as required                  |
| Performance   | An indication of the responsiveness of a system to execute our commands within a given interval of time | Can be measured in terms of latency or throughput                                                    |
| Reliability   | Defined as the chances that a product will perform its intended behaviour under the defined circumstances | Can be measured in terms of the correlation between two scores of test-retests                       |
| Reusability   | If we can use the product, or some specific part of the product, in the production of any other product | Can be tested by evaluating the software system’s functionality in different scenarios, testing modularity and compatibility, and assessing the performance and integration abilities |
| Security      | Measures taken to protect the system and its resources from unauthorized access and attacks | Can be tested via penetration testing, security code reviews, security testing tools, security assessments, user acceptance testing, and production monitoring |
| Scalability   | Defined as a scale of the system’s increasing or decreasing capability      | Can be measured in terms of its capacity to extend or reduce the quantity of user requests           |
| Load Balancing| Defined as a technique used to distribute workloads evenly across multiple computing resources to optimize resource utilization, increase reliability, and improve scalability | Can be measured by evaluating the distribution of incoming requests among the servers, response time, resource utilization, and the reliability of the system |
| Caching       | The temporary storage of frequently accessed data in a fast-access memory to reduce the number of expensive I/O operations, speed up access to the data, and reduce response time | Can be measured by evaluating the hit rate (ratio of cache hits to total requests), response time, and reduction of I/O operations |

# 📋 Requirements and Constraints

- Requirements are what actually drive the architecture.
- Constraints are design decisions on which no compromise can be made.

## ⚔️ Conflicting Constraints in Ride-Sharing App Design

### 1. ⚡ Real-time Responsiveness
- **Requirement:** Users expect real-time updates on driver location, estimated arrival times, and immediate booking.
- **Demand:** Low-latency communication and quick processing are essential.

### 2. 🔒 Data Security
- **Requirement:** Protect user data, including personal and payment information.
- **Measures:** Strong security measures like encryption, secure authentication, and rigorous access controls.

### Conflict
- **Issue:** Implementing strong security measures can introduce latency.
- **Challenge:** Prioritizing real-time responsiveness might lead to security vulnerabilities.

### ⚖️ Balancing Act
- **Trade-offs:** Improving real-time responsiveness may compromise data security; focusing on security could slow down real-time aspects.
- **Solution:** Software architects and designers need to find an acceptable compromise between these conflicting constraints.

# 🏗️ Application Types

- Represent different fundamental approaches or paradigms for designing and structuring software applications and help in providing a high-level understanding of how an application is built.
- Choosing an appropriate app type depends on specific requirements and infrastructure limitations.

## 💻 Application Types with Real-Time Examples

---

### 📱 Mobile Apps

#### Description:
- Can be developed as **web applications** or **rich client applications**.
- Support **occasionally connected** scenarios.
- Run on devices with **limited hardware resources**.

#### Real-Time Examples:
- **WhatsApp**: A rich client application that supports disconnected scenarios (e.g., sending messages offline that sync when reconnected).
- **Google Maps**: A hybrid web and rich client app with features like offline maps for occasional connectivity.
- **Spotify**: A music app that allows offline playback of downloaded songs.

---

### 💼 Rich Client Apps

#### Description:
- Developed as **stand-alone applications**.
- Can support **disconnected** or **occasionally connected** scenarios.
- Use the **processing and storage resources** of the local machine.

#### Real-Time Examples:
- **Microsoft Word**: Allows users to create and edit documents offline, saving them locally.
- **Photoshop**: A design application that heavily utilizes local processing power for rendering and editing.
- **IntelliJ IDEA**: A standalone IDE for developers with features working offline.

---

### 🌐 Rich Internet Applications (RIAs)

#### Description:
- Support **multiple platforms and browsers**.
- Are deployed over the **internet**.
- Designed for **rich media and graphical content**.
- Run in the **browser** for **maximum security**.
- Use the **processing and storage resources** of the local machine.

#### Real-Time Examples:
- **Canva**: An online design tool for creating graphics and media.
- **Google Docs**: Offers collaborative editing with rich features, all in the browser.
- **Figma**: A browser-based design tool that provides a rich user experience for UI/UX design.

---

### 🌍 Service Apps

#### Description:
- Support **multiple platforms and browsers**.
- Support only **connected** scenarios.
- Use the **processing and storage resources** of the server.

#### Real-Time Examples:
- **Stripe**: A payment gateway that offers APIs to process payments across platforms.
- **Twilio**: A communication platform providing messaging and voice APIs.
- **Amazon S3**: A service app for scalable cloud storage.

---

### 🌐 Web Apps

#### Description:
- Support **multiple platforms and browsers**.
- Support only **connected** scenarios.
- Use the **processing and storage resources** of the server.

#### Real-Time Examples:
- **Facebook**: A social media platform accessible via a browser.
- **YouTube**: A video-sharing platform, where all processing happens on the server.
- **Salesforce**: A CRM tool that runs entirely in the browser for connected use cases.

---

Each application type caters to specific scenarios based on connectivity, resource usage, and target platforms.

# 🚀 Deployment Strategy

1. **Application type and deployment strategy relationship**:
   The choice of deployment strategy depends on the application's nature, requirements, scalability, and architectural style.

2. **Monolithic vs. Microservices architecture**:
   Monolithic applications have a single deployment unit, while microservices require independent deployment of multiple services.

3. **Organizational rules and environmental constraints**:
   Consider organizational rules and environmental constraints in the deployment strategy, even if the target environment is inflexible.

4. **Quality attributes and early identification of requirements**:
   Identify requirements and restrictions early to choose a relevant deployment strategy and resolve conflicts between the app and infrastructure.

# 🖼️ Architecture Frame

1. **Definition and purpose**:
   The architecture frame within the meta-frame is a collection of hotspots used to analyze application structure, converting primary functions into actions.

2. **Hotspots and engineering decisions**:
   Each hotspot represents key engineering decisions and opportunities to improve design and build a more effective architecture.

## 🔍 Examples in Action

### 🛒 Example 1: Product Search Optimization (Hotspot: Performance)
- **Hotspot**: Product search response time.
- **Decision**: Use Elasticsearch for full-text search capabilities.
- **Impact**: Improved response times for search queries and better user experience.

### 📈 Example 2: Handling High Traffic (Hotspot: Scalability)
- **Hotspot**: Scalability of the checkout service during peak sales.
- **Decision**: Deploy the checkout service in a Kubernetes cluster with horizontal pod scaling.
- **Impact**: Ensured the system handled 1 lakh requests per second during a flash sale.

# 🌐 Cross-Cutting Concerns

1. **🔐 Authentication and authorization**:
   Identify users and determine their access to resources and operations.

2. **⚡ Caching**:
   Improve performance by temporarily storing frequently accessed data.

3. **🔗 Communication**:
   Define strategies for communication between layers and tiers, including protocols and security.

4. **❌ Exception management**:
   Handle errors, log them for auditing, and notify users of error conditions.

5. **📋 Instrumentation and logging**:
   Log key business events and security actions, providing an audit trail.

6. **🌀 Concurrency and transaction**:
   Manage conflicts from multiple users and treat multistep operations as atomic.

7. **💾 Data access**:
   Abstract and access data in the data store, including entity design and error management.

8. **🖱️ User experience**:
   Enhance interaction between users and the application, improving efficiency and effectiveness.

