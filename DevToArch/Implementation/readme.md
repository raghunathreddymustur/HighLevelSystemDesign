# Implementation Details

# Before Docker

## Web Server Architecture
1. Exceptation on Web server
   1. Handling slow and fast connections—comes out of the box
   2. Handing static content—comes out of the box
   3. Serving Dynamic Content
2. Available Choices
      1. Taken Choice: Django + Python (Due  to development is faster, can handle large projects, and resources are expertise in python)
      ![img.png](img.png)
3. Django Arch 
   ![img_1.png](img_1.png)
4. In Development mode , we had hosted static content on same web server instead of reverse proxy
   1. Advantages of Hosting Static Content on a Web Server in Development
      1. **Simplicity**: Reduces the complexity of your setup by avoiding the need for a separate reverse proxy.
      2. **Performance**: For development purposes, the performance difference is often negligible, making it efficient enough to serve static files directly from the web server.
      3. **Ease of Use**: Simplifies the development workflow, as there is no need to manage multiple services or configurations.
## Services Arch
1. Non Functional Requirements 
   ![img_5.png](img_5.png)
2. Business logic requirements to choose (Language + Frameworks)
   1. Reasons for Java
      1. OOPS language: For effective code structure of large code base
      2. Garbage Collection
      3. Compiled Languages for better performance
      4. High speed execution of business logic
      ![img_4.png](img_4.png)
   2. Framework : Spring
      1. We are not using ORM because we want to have control on queries and ability to change the database choice - We will use Spring Data
         ![img_6.png](img_6.png)
      2. Spring Core: DI features
3. Database
   1. Choices
      ![img_7.png](img_7.png)
   2. Schema
      ![img_8.png](img_8.png)
4. Single Page Application
   1. Choices
      ![img_9.png](img_9.png)


# Reasons for Dockerized components
1. Problems without docker
   ![img_10.png](img_10.png)
2. After Democratization
   ![img_11.png](img_11.png)

## Web Application Democratization
1. Create a docker [file](scripts/docker/Dockerfile-web) to build an image
2. Create an Image
3. Run the image in container
![img_12.png](img_12.png)


## Using Docker Compose to create, run, stop 
1. create a docker compose file.yml to each component
2. build it `docker-compose -f docker-compose.yml build web`
3. run it `docker-compose -f docker-compose.yml up -d web`
4. Similarly, for other components

## Docker Network and Volumes
![img_13.png](img_13.png)
![img_14.png](img_14.png)

## Docker Commands
1. Docker ps
   1. to list all running containers
2. docker logs -f web
   1. To see the logs of app
3. curl http:localhost:8080
   1. to ping the app running on server
4. remove a specific container
   1. docker rm -f <container_name>
5. Remove all containers
   1. docker rm -v -f $(docker ps -qa)


   
   
# GateWay Service
1. Right now our web server, single page application is having routing logic of all services, changes to services IP results in affecting its clients
![img_15.png](img_15.png)
2. Introduction of Gateway Service with Netflix Gateway
![img_17.png](img_17.png)
3. Reasons Netflix Zuul Gateway
   1. Provides authentication features
   2. provides centralized logging
   3. Provides Routing
   4. all java services tech stack

## Configuring gateway service - Static Routing config
1. In Gateways service project, have a config.properties files stating all routes
   ```yaml
server.port=8080
server.threadPool.threads.minimum=1
server.threadPool.threads.maximum=10
server.threadPool.threads.idleTime=60000
# Application Config
spring.application.name=GatewaySvc

# Service mapping
zuul.routes.authsvc.path=/auth/**
zuul.routes.authsvc.serviceId=AuthSvc
zuul.routes.authsvc.stripPrefix=false

zuul.routes.productsvc.path=/products/**
zuul.routes.productsvc.serviceId=ProductSvc
zuul.routes.productsvc.stripPrefix=false

zuul.routes.cartsvc.path=/carts/**
zuul.routes.cartsvc.serviceId=OrderSvc
zuul.routes.cartsvc.stripPrefix=false

zuul.routes.ordersvc.path=/orders/**
zuul.routes.ordersvc.serviceId=OrderSvc
zuul.routes.ordersvc.stripPrefix=false

zuul.routes.inventorysvc.path=/inventory/**
zuul.routes.inventorysvc.serviceId=InventorySvc
zuul.routes.inventorysvc.stripPrefix=false

zuul.routes.userprofilesvc.path=/users-profile/**
zuul.routes.userprofilesvc.serviceId=AuthSvc
zuul.routes.userprofilesvc.stripPrefix=false

zuul.routes.adminsvc.path=/admin/**
zuul.routes.adminsvc.serviceId=AdminSvc
zuul.routes.adminsvc.stripPrefix=false

zuul.routes.gatewaysvc.path=/**
zuul.routes.gatewaysvc.url=forward:/


AdminSvc.ribbon.listOfServers=http://localhost:8081
AdminSvc.ribbon.ServerListRefreshInterval=10000
AuthSvc.ribbon.listOfServers=http://localhost:8082
AuthSvc.ribbon.ServerListRefreshInterval=10000
ProductSvc.ribbon.listOfServers=http://localhost:8083
ProductSvc.ribbon.ServerListRefreshInterval=10000
OrderSvc.ribbon.listOfServers=http://localhost:8084
OrderSvc.ribbon.ServerListRefreshInterval=10000
InventorySvc.ribbon.listOfServers=http://localhost:8085
InventorySvc.ribbon.ServerListRefreshInterval=10000

     ```

## Challenges with static Routing
1. Static Routing is good for smaller applications with limited services.
2. if number of services along with their duplicates will become difficult to handle
3. If services want communicated between themselves then it becomes a problem
![img_18.png](img_18.png)
## Discovery Service - to overcome static routing
1. Add service for Netflix Eureka Discovery Server
   1. @EnableEurekaServer in main class
2. add the discovery client in other services to register themselves to discovery service
   1. @EnableDiscoveryClient in main class of services
   2. add properties related to discovery server in config
      ```yaml
# Eureka Config
eureka.instance.hostname=localhost
#eureka.client.eureka-server-port=9090
eureka.client.registerWithEureka=false
eureka.client.fetchRegistry=false
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.instance.preferIpAddress=false
eureka.instance.leaseRenewalIntervalInSeconds=10
eureka.instance.leaseExpirationDurationInSeconds=30
eureka.client.registryFetchIntervalSeconds=10
    ```
![img_19.png](img_19.png)


# Loadblancing of services
1. Having load balancers at web server, gateway and for each services
2. Types of Load Balancers
   1. Server side load balancer
      1. Client does that is loadbalancer (load balancer will redirect to actual server by dividing the load)
   2. Client side load balancer
      1. load balancer is present as part existing service
      2. No Extra server is required
![img_21.png](img_21.png)
3. Netflix Ribbon
   1. In Discovery Service( same nextflix tech stack makes it easier)
      1. add the property `ribbon.eureka.enabled=true`
   2. In Other Services - we have to write some logic
      1. @LoadBalancerClient to find instance from available instances
4. Ngnix Server Side load balancer and to server static content
   1. Created a ngnix.conf file which will have information about all instaces of gateway service
   2. Automated the adding of instances of a particular service to conf file automatically. Whenever ngnix server is started via dockers it will read the env variables and add the instances to conf file
   



## Scripts used to manage and deploy the services
1. [Dealing with staring of services](scripts/start-service.sh)
2. Directly Running web server from web project root directory
   `python manage.py runserver 0.0.0.0:8000`


## Challenges Faced
1. Splitting of Monolith to individual microservices
   1. How do clients (web server, single page) with multiple IP's of individual microservices
      1. Web server: We had [setting.py](scripts/settings.py) file defined having all the mapping of Ports
      2. SPA : we had IP mappings of services in .env file
2. 

## Error Faced

1. Indentation error in docker compose
2. Wrong mapping of port of server in docker file
   curl: (7) Failed to connect to localhost port 8000 after 0 ms:





# Cloud Config
1. Configure fire rules to allow ingress traffic for external facing services
2. Taking back of VM
   1. take backup(snapshot backup instead of dishbackup(takes times)) of VM before running the application so that we will not loose the steps done till now.
3. 

