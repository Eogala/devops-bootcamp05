# Setup Service Discovery Using Nginx & Consul
In DevOps, service discovery is all about automating how services find each other on a network. It's especially important in modern architectures with microservices, where applications are built from many small, independent services.

Traditionally, services were hardcoded with the locations of other services (like IP addresses). This becomes a nightmare to manage as things change and services are dynamically scaled up or down.
Introduction
Before we start, let's go over the basics of service discovery and introduce the service discovery tool we'll be using for this project.

## Key Concepts of Service Discovery
Service Registration: This involves adding a new service instance to the service registry so that it can be discovered by other services. Each service instance must provide its network location (e.g., IP address and port) and other metadata.

Service Registry: This is a database of available service instances. It acts as a central repository where all the service instances are registered and their statuses are monitored. Examples include Consul, Eureka, and etcd.

Service Lookup/Discovery: This is the process by which a service finds the network locations of other services it needs to communicate with. Discovery can be done in several ways:

Client-Side Discovery: The client is responsible for querying the service registry to find an available service instance and then makes a request directly to that instance.

Server-Side Discovery: The client makes a request to a load balancer or API gateway, which queries the service registry and forwards the request to an available service instance.

Health Checks: These are used to monitor the health and availability of service instances. Services that fail health checks can be removed from the service registry to ensure that clients do not attempt to communicate with unavailable services.

## Benefits of Service Discovery
* Dynamic Scalability: As services scale up and down, service discovery ensures that the correct instances are always available.

* Fault Tolerance: By continually monitoring service health and availability, service discovery helps maintain robust communication between services.

* Simplified Configuration: Instead of hardcoding service locations, developers can use the service registry, making configuration simpler and more maintainable.
Implementations
* Consul: A service mesh solution that provides service discovery, health checking, and a distributed key-value store.

* Eureka: A REST-based service used for locating services for the purpose of load balancing and failover in the cloud, often used with Spring Cloud.

* etcd: A distributed key-value store that can be used for service discovery, among other things.

* ZooKeeper: a powerful tool used to implement service discovery in distributed systems, providing essential coordination features such as centralized configuration management, naming services, and distributed synchronization.

## Example Workflow
* Service Registration: When a new service instance starts, it registers itself with the service registry, providing its address and metadata.

* Health Checks: The service registry periodically checks the health of registered services.

* Service Discovery: When a service needs to communicate with another service, it queries the service registry to find available instances.

* Load Balancing: If multiple instances of a service are available, the client or a load balancer can distribute requests among them.

## Use Cases
* Microservices: Ensuring that microservices can find each other dynamically as they scale and move across different nodes in a cluster.

* Dynamic Environments: In environments where services are frequently added, removed, or updated, service discovery helps maintain seamless communication.

* Service discovery is an essential part of modern DevOps practices, enabling the efficient and reliable communication of services in dynamic and scalable environments.

## Consul
Consul is an open-source tool by HashiCorp for service discovery, configuration management, and network automation in distributed systems. It allows services to register and discover each other, performs health checks, and provides a distributed key/value store for configuration data. Consul supports secure service-to-service communication, multi-datacenter setups, and advanced service mesh capabilities, making it ideal for managing microservices and dynamic cloud environments.

S/N	Project Tasks
1	Deploy 4 Ubuntu Server
2	Allow required ports in the security group
3	Set up architecture
4	Setup Consul Server
5	Setup Backend Servers
6	Setup Load-Balancer
7	Validate Service Discovery Setup

## Key Concepts Covered
* AWS (EC2 and Route 53)
* Linux(Ubuntu)
* Nginx
* Consul
* Environment Setup
* Service Registration with Consul
*Health Checks and Failover
* Load Balancing
* Monitoring and Logging
* Testing and Validation

## Checklist
 Task 1: Deploy 4 Ubuntu Server
 Task 2: Allow required ports in the security group
 Task 3: Set up architecture
 Task 4: Setup Consul Server
 Task 5: Setup Backend Servers
 Task 6: Setup Load-Balancer
 Task 7: Validate Service Discovery Setup

# Documentation
Please reference Project1 for guidance on spinning up an Ubuntu server.

Rename your EC2 instances to prevent any confusion during your project.

Click on the edit icon.

![pic](img/img1.png)

* Name your server and click the checkmark icon

![pic](img/img2.png)

* Name your Consul server, LoadBalancer server, and the two backend servers for easy identification

![pic](img/img3.png)


## Allow Required Ports In The Security Group
To ensure the proper functioning of the Consul service, please open the following ports in your security group and apply the same security group to all instances.

Consul Servers
S/N	Port Name	Protocol	Default Port
1	DNS	TCP and UDP	8600
2	HTTP API	TCP	8500
3	HTTPS API	TCP	8501
4	gRPC	TCP	8502
5	gRPC TLS	TCP	8503
6	Server RPC	TCP	8300
7	LAN Serf	TCP and UDP	8301
8	WAN Serf	TCP and UDP	8302

* Select the checkbox① next to your instance, click on Security②, and then click on the security group ID③.

![pic](img/img4.png)

Click on Edit inbound rules.

![pic](img)

* Click on Add rule,Enter the Port range
* Choose the appropriate CIDR block.
* Click on the Type field and choose Custom UDP from the dropdown menu.
* Verify that all the necessary ports are open.The processare repeated until you've opened up all necessary ports

![pic](img)

![pic](img)

![pic](img)

* Click on Save rules to apply the updated security group settings