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
   1. Created a [ngnix.conf](scripts/docker/LoadBalancer/nginx/nginx.conf) file which will have information about all instaces of gateway service
   2. [Automated](scripts/docker/LoadBalancer/nginx/docker-entrypoint.sh) the adding of instances of a particular service to conf file automatically. Whenever ngnix server is started via dockers it will read the env variables and add the instances to conf file
   3. Instances of services are added to conf file based on environment variable set in [docker](scripts/docker/LoadBalancer/docker-compose.yml) file

   
# Observability of System
1. As part of Observability we will add Logs, Trace, Metrics
2. Errors: able to find which part of system is having issue
2. Audit: able to check user claims(missing info) through logs
3. Analytics: Tracking time taken by requests
![img_22.png](img_22.png)

## Centralized Logging
![img_23.png](img_23.png)

1. We have docker [compose](scripts/docker/obserability/DockerCompose.yaml) file having the configuration about Log Collector(FluentD)
```yaml
fluentd:
build:
context: ../../fluentd
dockerfile: Dockerfile
image: ntw/fluentd
container_name: fluentd
hostname: fluentd
networks:
- mynet1
ports:
- "24224:24224"
volumes:
- ${PWD}/fluent.conf:/fluentd/etc/fluent.conf
- fluentd-logs:/fluentd/log
depends_on:
- "elasticsearch"
restart: unless-stopped
```
1. Have [docker](scripts/docker/obserability/fluentd-docker) file to create fluent D image and it a [file](scripts/docker/obserability/fluentD.conf) configure it
   1. How does services know about log collector?
      1. Docker log driver will be out log agent
      2. In docker-compose file for each service we will specify the log collector( fluent d) location
         ```yaml
         web:
         build:
         context: ../../web
         dockerfile: Dockerfile
         image: ntw/web
         container_name: web
         hostname: web
         networks:
         - mynet1
           ports:
           - "8000:8000"
             command: python3 manage.py runserver 0.0.0.0:8000
             env_file: .env
             volumes:
           - app-logs:/var/log/oms
             logging:
             `driver: "fluentd"
             options:
             fluentd-address: "127.0.0.1:24224"`
             tag: web
             depends_on:
           - "fluentd"
           ```
   2. Add the Elasticsearch for storing logs
      ```yaml
      elasticsearch:
      image: elasticsearch:7.13.2
      container_name: elasticsearch
      hostname: elasticsearch
      environment:
      - "discovery.type=single-node"
        - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
        - "xpack.security.enabled=false"
        expose:
        - "9200"
        ports:
        - "9200:9200"
        networks:
        - mynet1
        volumes:
        - elasticsearch-data:/usr/share/elasticsearch/data
        restart: unless-stopped

        ```
   3. Add the Kibana for Visulization
      ```yaml
      kibana:
      image: kibana:7.13.2
      container_name: kibana
      hostname: kibana
      ports:
      - "5601:5601"
      networks:
        - mynet1
        environment:
        - ELASTICSEARCH_HOSTS="http://elasticsearch:9200"
        restart: unless-stopped
        depends_on:
        - "elasticsearch"

        ```
   5. Analyze the logs in elsatic search dashboard
      1. Create an index or map to an index
      2. Filter logs based filters like container-name, logs...etc
      3. Still have to explore
   

# Tracing for monitoring performance 
1. Distributed tracing will help in pinpointing the which component is having performance problems
   ![img_24.png](img_24.png)
2. Add the required arch to trace in each component
   ![img_25.png](img_25.png)
3. We use jager for tracing
   1. Add the Trace Agent( which will collect all required logs) in each component
   2. Add the collector(Jaeger) to collect all individual traces from each component
   3. Store all collected traces in storage( elastic search)
   ![img_26.png](img_26.png)
4. Concept of distributed tracing
   ![img_27.png](img_27.png)
5. How to deal with services which are calling other services or async flows
   1. We explicitly extract the span from headers and pass to other services
6. Made some configurations in .env file
7. Jaeger Instrumentation in code
   1. In Web
      1. ![img_28.png](img_28.png)
      2. Instrument required API's with tracing
         ![img_29.png](img_29.png)
   2. In Web Services
      1. Add the dependency to common project
      2. Add the required properties in config(properties) file
      ![img_30.png](img_30.png)
      3. Add the instrumentation if your service is calling other service - to trace that call
      ![img_31.png](img_31.png)
      4. Similarly if you have async processing, instrument that as well
      ![img_32.png](img_32.png)
         8. Dockering the jaeger
            1. Create images and run it
               ```yaml


                        jaeger-agent:
                        image: jaegertracing/jaeger-agent
                        container_name: jaeger-agent
                        hostname: jaegar-agent
                        networks:
                        - mynet1
                          ports:
                           - "6831:6831/udp"
                           - "14271:14271"
                             environment:
                           - SPAN_STORAGE_TYPE=elasticsearch
                             command: ["--reporter.grpc.host-port=jaeger-collector:14250"]
                             restart: unless-stopped
                             depends_on:
                           - "jaeger-collector"
               
                        jaeger-collector:
                        image: jaegertracing/jaeger-collector
                        container_name: jaeger-collector
                        hostname: jaegar-collector
                        networks:
                        - mynet1
                          ports:
                           - "14250:14250"
                           - "14269:14269"
                             environment:
                           - SPAN_STORAGE_TYPE=elasticsearch
                        #      - ES_SERVER_URLS="elasticsearch:9200"
                            command: [
                              "--es.server-urls=http://elasticsearch:9200",
                              "--es.num-shards=1",
                              "--es.num-replicas=0",
                              "--log-level=error"
                            ]
                            restart: unless-stopped
               
                        jaeger-query:
                        image: jaegertracing/jaeger-query
                        container_name: jaeger-query
                        hostname: jaeger-query
                        networks:
                        - mynet1
                          ports:
                           - "16685:16685"
                           - "16686:16686"
                           - "16687:16687"
                             environment:
                           - SPAN_STORAGE_TYPE=elasticsearch
                             command: [
                             "--es.server-urls=http://elasticsearch:9200",
                             "--span-storage.type=elasticsearch",
                             "--log-level=debug"
                             ]
                             restart: unless-stopped
                             depends_on:
                           - "jaeger-collector"
               ```
         2. Start the services
         3. Trace the call with Jaeger UI
         
# Obserability - Monitoring the services Metrics
1. ![img_33.png](img_33.png)
2. ![img_34.png](img_34.png)
3. Add the required properties in each service
4. Add to docker-compose file with required configuration( which metrics to monitor)
   ```yaml

   prometheus:
   image: prom/prometheus
   container_name: prometheus
   hostname: prometheus
   networks:
   - mynet1
   ports:
     - "9090:9090"
     command:
     - '--config.file=/etc/prometheus/prometheus.yml'
     volumes:
     - ${PWD}/prometheus.yml:/etc/prometheus/prometheus.yml
     - ${PWD}/rules.yml:/etc/prometheus/rules.yml
     restart: unless-stopped
   
   es-exporter:
   image: prometheuscommunity/elasticsearch-exporter
   container_name: es-exporter
   hostname: es-exporter
   networks:
   - mynet1
   ports:
     - "9114:9114"
     command:
     - '--es.uri=http://elasticsearch:9200'
     restart: unless-stopped
   
   pg-exporter:
   image: prometheuscommunity/postgres-exporter
   container_name: pg-exporter
   hostname: pg-exporter
   networks:
   - mynet1
   ports:
     - "9187:9187"
     environment:
     - DATA_SOURCE_NAME=postgresql://postgres:postgres@postgres:5432/oms?sslmode=disable
     restart: unless-stopped
       global:
       scrape_interval:     15s # Default is every 1 minute.
       evaluation_interval: 15s # Default is every 1 minute.
     # scrape_timeout is set to the global default (10s).
   
   scrape_configs:
   - job_name: 'web-app-metrics'
     metrics_path: '/metrics'
     scrape_interval: 5s
     static_configs:
      - targets:
         - web:8000
     - job_name: 'services-metrics'
       metrics_path: '/actuator/prometheus'
       scrape_interval: 5s
       eureka_sd_configs:
        - server: http://eureka:8761/eureka
          static_configs:
        - targets:
           - eureka:8761
   #        - auth-svc:8080
   #        - product-svc:8080
   #        - order-svc:8080
   #        - inventory-svc:8080
   #        - user-profile-svc:8080
   #        - gateway-svc:8080
   #        - admin-svc:8080
   - job_name: 'jaeger-metrics'
     metrics_path: '/metrics'
     scrape_interval: 5s
     static_configs:
      - targets:
         - jaeger-agent:14271
         - jaeger-collector:14269
         - jaeger-query:16687
     - job_name: 'database-metrics'
       metrics_path: '/metrics'
       scrape_interval: 5s
       static_configs:
        - targets:
           - es-exporter:9114
           - pg-exporter:9187
   
   rule_files:
   - rules.yml
   
   groups:
   - name: example
     rules:
   
     # Alert for any instance that is unreachable for >5 minutes.
      - alert: InstanceDown
        expr: up == 0
        for: 5s
        labels:
        severity: page
        annotations:
        summary: "Instance {{ $labels.instance }} down"
        description: "{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 5 seconds."
   
     # Alert for any instance that has a median request latency >1s.
      - alert: APIHighRequestLatency
        expr: api_http_request_latencies_second{quantile="0.5"} > 0.1
        for: 10m
        annotations:
        summary: "High request latency on {{ $labels.instance }}"
        description: "{{ $labels.instance }} has a median request latency above 1s (current value: {{ $value }}s)"


    ```
5. Start the services & Monitor the metrics
6. Metrics are exposed by spring boot actutor

## Managing Read Load - Caching
1. Advantages and Challenges with cache
   ![img_35.png](img_35.png)
2. Choosing Redis as Cache
   ![img_36.png](img_36.png)
3. Make [changes](redis/javaConfig/configandService.md) in required services to hit cache instead of database
   1. Add the Cache Configuration in java code and properties.yml
   2. Make Changes in services
4. Add the Redis to Docker Compose
   ```yaml
   redis:
   image: redis
   container_name: redis
   hostname: redis
   networks:
   - mynet1
   ports:
     - "6379:6379"
   
   
   redis-exporter:
   image: oliver006/redis_exporter
   container_name: redis-exporter
   hostname: redis-exporter
   networks:
   - mynet1
   ports:
     - "9121:9121"
     environment:
     - REDIS_ADDR=redis://redis:6379
     restart: unless-stopped
     ```
5. Run the service
6. Test the API using Jaeger Trace - Check the time taken

# Async Processing - Managing Write Load
1. Advantages
   ![img_37.png](img_37.png)
2. 
3. Identify the API which are write oriented at can be processed in Async
   1. Order(Processing the order in Async) and Inventory services(Updation of inventory) can be in Aysc

   


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

