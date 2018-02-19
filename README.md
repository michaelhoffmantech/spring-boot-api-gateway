# spring-boot-api-gateway

API Gateway using Spring Cloud's Gateway Starter for Getting Started with Spring Boot demo

# 1 - Spring Intializr Creation

I used the following at http://start.spring.io to create the Gateway Server application.

* Build tool - Gradle 
* Language - Java
* Spring Boot Version - 2.0.0.RC1 
* Group = com.scmc
* Artifact = boot-demo-gateway-server
* Name = boot-demo-gateway-server
* Package Name = com.scmc.bootdemo.gateway
* Packaging = JAR
* Java Version = 1.8
* Dependencies = Actuator, Gateway, Redis, Hystrix, Eureka Discovery, Reactive Web

# 2 - Config Server Updates

## 2.1 - Update Application Class

In the class BootDemoGatewayServerApplication, I added the following annotation to enable discovery:

```
@EnableDiscoveryClient
```

Then, I defined the following bean to allow for automatic discovery of routes via Eureka. 

```
@Bean
	DiscoveryClientRouteDefinitionLocator discoveryRoutes(DiscoveryClient discoveryClient) {
		return new DiscoveryClientRouteDefinitionLocator(discoveryClient);
	}
```

## 2.2 - Update Application Properties

I added the following application properties:

server.port=9001
spring.application.name=gateway-service
spring.cloud.gateway.discovery.locator.enabled=true
spring.jackson.serialization.indent_output=true
management.endpoints.web.expose=*

* This changes the port where the gateway server will be running on.
* I've specified the name of the gateway service application.
* I'm enabling this application for discovery services.
* I'm indenting JSON for pretty print in actuator output
* I'm enabling all management endpoints.

# 3 - Running the Server

To run the gateway server, simply use the command:

.\gradlew bootRun


# 4 - More Information

* Spring's page on Spring Cloud Gateway is found here: https://cloud.spring.io/spring-cloud-gateway/