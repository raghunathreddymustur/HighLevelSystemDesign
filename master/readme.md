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
3. 
      

      
