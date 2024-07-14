# High Level System Design

What is System Design
-----
1. Deciding the architecture, components and modules in each component and interaction between them.

What will we do when we design a system
--------------------------------------
1. break down problem statement into solvable sub-problems.
2. decide on key components and responsibilities
3. decide on boundaries of each component
4. touch upon key challenges in scaling it
5. make our architecture fault tolerant and available

How to approach System Design! 
------------------------------
1. System Design is extremely practical
and there is a structured way to tackle the situations.
Take baby steps, no matter what!
2. understand the problem statement.
   1. Without having a thorough understanding of the problem at hand, we would easily digress.
3. Breakdown the problem
   1. Example: Design Facebook
      1. Think in features
         2. Feed, Auth, Notifications. etc.
   2. Pick subproblem and go deep into it
        ![img.png](img.png)
4. For each subcomponent, look into
   1. Database and Caching
   2. Scaling & Fault Tolerance
   3. Async processing (Delegation)
   4. Communication
5. Dissect each component (if required)
   1. Example: Generator in Feed
      ![img_1.png](img_1.png)


How do you know that you have built a good system?
-------------
1. The System is broken down to subcomponents
2. Every component has a clear exclusive set of responsibilities
   1. Feed Web Server -> serves feed over HTTP
   2. Feed Generator -> Pulls data from multiple services and puts them in DB
   3. Feed Aggregater -> combines candidate items fetch be generator filters out redundant, ranks and creates a final consumable feed.
3. For each subcomponent following is figured out
   1. Database and Caching
   2. Scaling & Fault Tolerance
   3. Async processing (Delegation)
   4. Communication
4. Each component (in isolation) is
   1. Scalable  →  horizontally scalable
   2. fault-tolerant → plan for recovery of data mostly in case of a failure ↳ to a stable state
   3. available → component functions even when some component "fails"


Interview Perceptive
--------------------
![img_2.png](img_2.png)
![img_3.png](img_3.png)

How to define system requirements
--------------------------------
1. Functional Requirements
   1. We need to identify `who` is going to use the system and `how`, What is `input` and `output` for abstract systems
   ![img_4.png](img_4.png)
   2. Define Api for actions
   ![img_5.png](img_5.png)
2. Summary
   ![img_6.png](img_6.png)
   ![img_7.png](img_7.png)
   ![img_8.png](img_8.png)

Infrastructure to achieve the non-functional requirements
---------------------------------------
1. Servers
   1. CPU 
   2. Memory Size
   3. Disk
   4. Network IO
   5. Decision
      1. We decide the server optimized to one or more of the following properties like whether cpu heavy, disk heavy, etc.
   6. Usually CPU is easier to scale and network IO is hard to scale
2. Rack
   1. Servers are physically easier to reach, examine, and manipulate.
   2. Simplifies cooling and increases security.
   3. Has its own network and power source.
   4. To increase availability, we can place servers in different racks.
   5. To reduce latency, we can place servers
      in the same rack.
3. Data Center
   1. Group of racks
   2. Has independent power, cooling, and physical security.
   3. May become unavailable due to power outage, earthquake.
4. Availability Zones
   1. Group of datacenters
   2. Increases availability as hardware is distributed across multiple data centers.
   3. Increases scalability as there are
      multiple places to allocate hardware from.
5. Regions
   1. Group of availability zones
   2. Within a radius of 100 km.
   3. AZS in a region are interconnected with high-bandwidth and low-latency networking.
![img_10.png](img_10.png)
6. Helps in achieving some non-functional requriments
   1. Deploying in multiple regions to tackle world wide traffic
      1. we deploy a copy of the system to every region worldwide
      2.  improves performance—the system is physically closer to users
      3.  increases availability—we can forward requests to other regions 
      4. improves scalability—more hardware is available for allocation
   2. In each availability zone 
      1. increases durability—we can replicate data quickly between zones within each data center
      2. we deploy to servers in different racks 
      3.  we choose the server type based on the workload it expects to run

Fundamentals of reliable, scalable, and fast communication
--------------------------------
1. Synchronous vs asynchronous communication
   1. Synchronous and asynchronous request response
      ![img_11.png](img_11.png)
   2. Asynchronous communication
      ![img_12.png](img_12.png)
2. Messaging solves many problems
   ![img_13.png](img_13.png)
3. Choice is made on client requirement
   ![img_14.png](img_14.png)

   



      

      
