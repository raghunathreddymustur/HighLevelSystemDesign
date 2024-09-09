# E-commerce System

## Functional Requirements

### Inventory Side—Administers adding products to the site

### Customer Facing Site
1. Render Site based on location
2. Product Service
   1. List the products on pages
   2. Search-based on text
      1. Search Product string completion
      2. name 
      3. serial Id
      4. number
   3. Filter the products
   4. How to store the images
      1. Products have
         1. Images 
         2. Tiny videos
      2. Storage Options
         1. S3 blob storage
            1. Advantage is cost
      3. Store Metadata of images and videos in a separate database
   
3. Cart & Order Service
   1. Add to the cart
      1. Increase or decrease number of items in the cart
      2. Current Updates
4. Delivery 
   1. Notifications
   2. Order Tracking
5. Payments
   1. Failures in payments
      1. Intermediate Failures
6. Monitoring
   1. metrics on failed requests
7. No Recommendation engine
8. 




## Product Service1
1. Usage of Elasticsearch
   1. Let the users search with strings


## Modules from Monolith

1. Admin Page
   1. Have Control Panel
      1. Users
      2. Categories
      3. Brands
      4. Products
      5. Questions
      6. Reviews
      7. Customers
      8. Shipping Rates
      9. Orders
      10. Articles
      11. Menu Items
      12. Section & Settings
2. User Management
   1. Admin User
      1. Manage Users
         1. All Curd operations on users
         2. Pagination
         3. Creation of Users
   2. Authentication
      1. Displaying of username on UI
      2. login 
      3. logout
      4. Update account details
   3. Authorization
      1. Each Role has different roles assigned to them
      2. Based on roles UI will change
   4. Category Module
      1. All crud Operations on Categories and subcategories
   5. Brand Management Module
      1. Manage different brands and different categories of products they are allowing
   6. Product Management
      1. All crud operations on Product
      2. Filters by category
   7. End Users
      1. Visitor
      2. End User
      3. BFor both users have products and different features
   8. Enabling user interface by admin
   9. Site Settings
      1. General
      2. Mail Server
      3. Allowed countries and States for registration
      4. Payments
   10. Customer Registration
       1. verification on email after registration
   11. Manage Customers
   12. Customer Authentication
       1. user and password
       2. google or facebook
       3. User features
         ![img.png](img.png)
       4. Resetting password
   13. Cart
       1. increase or decrease the quantity of product
       2. removal of products
   14. Snipping Rates
       1. All crud operation on all countries rates
   15. Manage Address Book
       1. Manage multiple address
   16. Order Management
       1. crud on orders
       2. filters on search
   17. Checkout 
       1. Payment
       2. checkout
          1. change address
       3. location
   18. Order Module
       1. Tracking
       2. View Order information
   19. Order Management for Shipper
       1. view all orders info
       2. update of tracking info
   20. Order Management of Users
       1. View order details and search
   21. Sales Report
   22. Product Reviews
       1. Ratings and Voting
   23. Questions on Answers for a product
   24. Articles
       1. on Payments
       2. one Customer care
   25. Manu Management Module
   26. Landing Page
   27. Tech Up gradation
       
   
   
   
      
2. Custom Error Handling and pages
3. 



# Need to Explore

1. About datastores
2. Thinking about possible problems of a system
3. Ability to provide rationale behind a decision
4. Ability to choose existing solutions instead of staring from scratch
5. Capacity estimates
6. Api Design of each service
7. Database Schema of each service
8. Exception Handling
9. Is there an automation of testing products?
10. 
