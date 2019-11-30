# zuul-examples

1. create a spring boot starter project -> spring-cloud-starter-zuul, spring-cloud-starter-ribbon,
spring-cloud-starter-eureka

2. add @EnableZuulProxy to the spring boot class

3. application.yml

info:
  component: Edge Server
  
zuul:
  prefix: /api
  routes:
    account: 
      path: /sample/**
      serviceId: sample-service
    customer: 
      path: /other/**
      serviceId: other-service    
	  
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
    registerWithEureka: false
      
server:
  port: 8765
	  


Notes :
	  
Fetch Registry
----------------
Eureka clients fetches the registry information from the server and caches it locally. 
After that, the clients use that information to find other services. This information is
updated periodically (every 30 seconds) by getting the delta updates between the 
last fetch cycle and the current one. The delta information is held longer (for about 3 mins) 
in the server, hence the delta fetches may return the same instances again. 
 
The Eureka client automatically handles the duplicate information.
