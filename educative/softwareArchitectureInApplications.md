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

## Architecture Patterns

## 🏛️ Centralized and Decentralized Architecture

### 📜 Overview
Centralized and decentralized architectures represent two fundamental ways of organizing systems. They define how entities function, make choices, distribute resources, and manage tasks.

### 🖥️ Centralized Architecture
Centralized architecture involves a server node (controller) managing client nodes (workers). The server node distributes work, and client nodes perform the tasks.

#### Characteristics
- **Global clock**: Client nodes sync their clocks with the server node.
- **Single server node**: One server node serves all client nodes, and its failure affects the whole system.

#### Advantages
- **Ease of security**: Easy to secure server and client nodes.
- **Quick updates**: Updates are made only to the central server, ensuring efficiency.

#### Disadvantages
- **Network connectivity**: If the server disconnects, the whole network slows down.
- **Data backup**: All data is stored in the server node, risking data loss if it fails.

### 🌐 Decentralized Architecture
Decentralized architecture allows each node to make its own decisions, with no single controller node. Examples include cryptocurrency and blockchain systems.

#### Characteristics
- **System resilience**: Failure of one node doesn't affect the whole system.
- **Multiple servers**: More than one server can handle requests, improving efficiency.

#### Disadvantages
- **Node failure**: Individual node failures can disrupt the system.
- **Security risks**: Vulnerable to attacks on individual nodes.

#### Advantages
- **Avoid bottlenecks**: Load is distributed among nodes, preventing bottlenecks.
- **High availability**: Nodes make independent decisions, ensuring some are always available.

# Software Architecture Patterns with Realtime Examples

## 🏗️ Layered Architecture

### 📜 Overview
Layered architecture divides a system into units or layers, allowing independent development and clear documentation. Each layer provides a consistent set of services and can only access its next lower neighbor.

### 🔄 Open vs. Closed Layers
- **Closed Layers**: Requests must go through each layer without bypassing, ensuring separation and easier modifications.
- **Open Layers**: Layers can be bypassed, increasing complexity but reducing traffic on individual levels.

### ✅ Advantages
- **Simplifies Structure**: Divides the application into distinct layers, reducing complexity.
- **Decreases Dependencies**: Allows easier substitution of different implementations for a particular layer.
- **Improves Testability**: Isolates layers for testing, increasing reusability and scalability.
- **Enhances Security**: Separate tiers improve security with firewalls between layers.

### ❌ Disadvantages
- **Interdependence**: Changes in one layer can require changes in multiple layers, reducing flexibility.
- **Increased Code**: Requires more code for communication between layers, risking logic leaks.
- **Inefficiencies**: Requests through multiple layers can be inefficient, and deploying multiple layers increases costs.

### 🔧 Realtime Example: E-commerce Application
- **Presentation Layer**: A web or mobile interface showing product catalogs, search functionality, and shopping cart.
- **Business Logic Layer**: Processes product recommendations, applies discounts, and calculates taxes.
- **Data Access Layer**: Handles interactions with databases to fetch product information, order details, and user profiles.
- **Example Flow**: A customer searches for a product -> The request goes to the business layer for processing -> Fetches product details from the data access layer -> Returns to the presentation layer to display results.

---

## 🏛️ N-Tier Architecture

### 📜 Overview
N-tier architecture organizes system components into distinct layers or tiers. Tiers can be based on functionality or computing environment, defining control and communication patterns or allocation patterns.

### 🖥️ Tiers vs. Layers
- **Layers**: Logical separation of functionality and components.
- **Tiers**: Physical separation of different components of the software system.

### 🎨 Presentation Tier
The presentation tier handles the application's user interface. It focuses on usability and should have minimal logic to simplify testing.

### 🏢 Business Tier
The business tier implements the application's business logic, including rules, validations, and calculations. It acts as a bridge between the presentation and data tiers.

### 📊 Data Tier
The data tier provides data access and management functions. It includes a data store for persistent storage and interacts with the business tier.

### ✅ Advantages
- **Secure**: Easy to secure each tier.
- **Flexible**: Extendable in multiple ways.
- **Scalable**: Scale or update any tier independently.
- **Improved Modularity**: Separate development and maintenance of components.
- **Better Scalability**: Independent scaling of tiers.
- **Increased Security**: Separation of presentation and data layers.
- **Improved Maintainability**: Easier updates without affecting other tiers.

### ❌ Disadvantages
- **Costly**: High hardware, network, and deployment costs.
- **Complexity**: More complex implementation.
- **Performance Overhead**: Additional layers can lead to performance overhead.
- **Increased Development Time**: Longer development due to multiple tiers.

### 🔧 Realtime Example: Banking System
- **Presentation Tier**: A web or mobile banking app interface for customers to check their balance, transfer funds, or view transaction history.
- **Business Tier**: Processes business rules like validating account details, calculating interest rates, and handling transaction rules.
- **Data Tier**: Stores customer accounts, transaction details, and balance history.
- **Example Flow**: A user initiates a money transfer -> Business tier validates user credentials and account details -> Data tier records the transaction -> Business tier notifies the presentation tier to display a success message.

---

## 🏛️ Model-View-Controller (MVC) Architecture

### 📜 Overview
MVC is a software architecture pattern that divides an application into three components: Model, View, and Controller. This separation provides a structured and organized way to design and develop applications.

### 🗂️ Model
The model represents the business logic and data of the application. It maintains the state and performs operations on the data.

### 🖼️ View
The view is responsible for rendering the user interface. It receives data from the model and presents it to the user.

### 🎮 Controller
The controller handles user input and interactions. It processes requests from the view and sends them to the model, then updates the view with the results.

### ✅ Advantages
- **Separation of Concerns**: Each component has a specific role, keeping the code organized.
- **Reusability**: Components can be reused in other applications.
- **Testability**: Easier to write automated tests for different components.
- **Flexibility**: Allows for different views and controllers for the same model.

### ❌ Disadvantages
- **Complexity**: Can make the application more complex for new developers.
- **Increased Overhead**: Requires more code and components.
- **Extra Layer of Abstraction**: Adds an extra layer between the user and model, which can make the application less intuitive.

### 🔧 Realtime Example: Blog Management System
- **Model**: Manages blog data, such as posts, authors, and comments.
- **View**: Displays the blog interface, showing posts and comments.
- **Controller**: Handles user actions like creating, editing, or deleting posts.
- **Example Flow**: A user edits a blog post -> Controller updates the model -> Model saves the updated data -> View refreshes to display the updated post.

---

## 🏛️ Model-View-ViewModel (MVVM) Architecture

### 📜 Overview
MVVM separates the presentation layer from business logic and data models, enhancing flexibility and maintenance. It consists of three main components: Model, View, and ViewModel.

### 🗂️ Model
The model represents the data and business logic of the application. It manages data and performs actions on it.

### 🖼️ View
The view represents the user interface, displaying data to the user and processing user input.

### 🎮 ViewModel
The view model links the model and the view, presenting data from the model to the view and managing UI logic and events.

### ✅ Advantages
- **Separation of Concerns**: Clear separation between the view and model, making the code easier to understand and maintain.
- **Improved Testability**: Easier to write automated tests for different components.
- **Better Support for Data Binding**: Built-in support for data binding, creating interactive applications.
- **Improved Code Reuse**: Easier to reuse code across different views and platforms.

### ❌ Disadvantages
- **Increased Complexity**: Can make the application more complex, especially for new developers.
- **More Code**: Requires more code, increasing development time and resources.
- **Steep Learning Curve**: Challenging to master, particularly for those unfamiliar with WPF or other XAML-based platforms.

### 🔧 Realtime Example: Weather Forecast Application
- **Model**: Retrieves weather data from APIs.
- **ViewModel**: Processes raw weather data (e.g., converting temperature from Fahrenheit to Celsius) and binds it to the view.
- **View**: Displays the processed weather data to the user.
- **Example Flow**: User opens the app -> ViewModel fetches and processes weather data from the model -> View updates to show the current temperature and weather forecast.

---

## Decision-Making Checklist

### 1. **🔍 Start with Requirements:**

- Is performance or maintainability a priority?
- Are there specific non-functional requirements (e.g., scalability, security)?

### 2. **📚 Consider Team Expertise:**

- Does your team have experience with advanced patterns like MVVM or MVC?
- Are the developers familiar with multi-tier or layered deployment strategies?

### 3. **🎨 Analyze Application Type:**

- **🌐 Web-based**: MVC or Layered.
- **📲 Desktop/Mobile**: MVVM.
- **☁️ Enterprise/Cloud**: N-Tier.

### 4. **🔢 Plan for Future Growth:**

- Will the system scale to more users or require additional features?
- Is it easy to modify and extend the chosen architecture?




