## Spring Cloud Service Discovery with Netflix Eureka

* **We will be using Spring Boot based Spring Cloud API. We will use Netflix Eureka server for building the service registry server and Eureka clients which will register themselves and discover other services to call REST APIs.**

#### What is Netflix Eureka Server and Clients?
* As we know these days, there is a lot of momentum around Microservices. The transition from Monolithic to Microservice based architecture gives many benefits for future in terms of maintainability, scalability, high availability etc. However at the same time, there are many challenges also while doing this migration. One of them is to maintain individual Microservices addresses. This task can be hugely complex – depending on number of services and their dynamic nature. If whole infrastructure is distributed and there is some replication as well, then maintaining this service addresses becomes harder.

* To solve this, in the distributed computing are there is a concept called ‘Service registration and discovery’ where one dedicated server is responsible to maintain the registry of all the Microservice that has been deployed and removed. This will act like a phone book of all other applications/microservices.

* Think of it as a lookup service where microservices (clients) can register themselves and discover other registered microservices. When a client microservice registers with Eureka it provides metadata such as host, port, and health indicator thus allowing for other microservices to discover it. The discovery server expects a regular heartbeat message from each microservice instance. If an instance begins to consistently fail to send a heartbeat, the discovery server will remove the instance from his registry. This way we will have a very stable ecosystem of Microservices collaborating among each other, and on top of it we don’t have to manually maintain address of other Microservice, which is a next to impossible task if the scale up/down is very frequent, on demand and we use virtual host to host the services specially in the cloud environment.


* We will create three microservices for this Netflix Eureka example.

* **Eureka Service Registry Server** – This microservice will provide the service registry and discovery server.
* **Student Microservice** – Which will give some functionality based on Student entity. It will be a rest based service and most importantly it will be a eureka client service, which will talk with eureka service to register itself in the service registry.
* **School Microservice** – Same type as of Student service – only added feature is that it will invoke Student service with service look up mechanism. We will not use absolute URL of student service to interact with that service.


* **Eureka URL :**  http://localhost:8761/
* **Student Service URL :**  http://localhost:8098/getStudentDetailsForSchool/abcschool
* **School Service URL :**  http://localhost:9098//getSchoolDetails/abcschool


#### Things to check if facing any error
* Annotations @EnableEurekaServer and @EnableEurekaClient are the heart of the application ecosystem. Without those two things will not work at all.
* Make sure at the time of starting the config client service, eureka server service is running already, otherwise it might take some time to register, which might create confusion while testing.
