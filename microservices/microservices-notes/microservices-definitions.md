# What is a Microservice?
We start with stating that all industry definitions think of Microservices as an Application Architecture Pattern or Architecture Style, 
that is, it is an architecture pattern used to construct an application with well-defined software architecture principles. Thus the term Microservices means Microservices Architecture Style or Microservices Architecture Pattern or Microservices Architecture 
and are used interchangeably.

## Martin Fowler's definition of Microservices [1]
The microservice architectural style is an approach to developing a single application:   
  
* As a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API
* These services are built around business capabilities
* These services are independently deployable by fully automated deployment machinery
* There is a bare minimum of centralized management of these services
* These services may be written in different programming languages
* These services use different data storage technologies

## Adrian Cockroft's definition of Microservices [2]
Adrian Cockroft, who was Chief Cloud Architect at Netflix and now is VP of Cloud Architecture Strategy at AWS defined Microservices as [2]:  
“Loosely coupled service oriented architecture with bounded contexts"  

Adrian further clarifies two terms:
* Loosely Couple means “If every service has to be updated in concert, it's not loosely coupled!"
* Bounded Context [3] means “If you have to know about surrounding services you don't have a bounded context."  
  
Here bounded context is a reference to Bounded Context design pattern defined in Domain-Driven Design by Eric Evans [8] . Included in the definition of Bounded Context is use of different data store in each bounded context.

## Sam Neuman's definition of Microservices[4]
Sam Newman, an ex Googler and who worked at Thoughtworks, is author of _Building Microservices: Designing Fine Grained Systems_, in this book he defines Microservices as:  
"Microservices are small, autonomous services that work together."
  
Sam Newman further clarifies two terms in his definition:  
* Small is a reference to Rober C. Martin's Single Responsibility Principle, which states “Gather together those things that change for the same reason, and separate those things that change for different reasons.”
* Autonomous means "microservice is a separate entity. It might be deployed as an isolated service on a platform as a service (PAAS), or it might be its own operating system process" & "All communication between the services themselves are via network calls, to enforce separation between the services and avoid the perils of tight coupling. "
  
It is important to note if not already clear so far is that an Application built using Microservices Architecture style is a Distributed System.

## Amazon's Use of Services [5]
Although Amazon has generally not used the term “microservices", those in the industry who are part of microservices movement draw a lot of inspiration from their experience. The 2006 ACM Queue interview with Werner Vogels, remains the best source for information on what they did:  

“For us service orientation means encapsulating the data with the business logic that operates on the data, with the only access through a published service interface. No direct database access is allowed from outside the service, and there's no data sharing among the services."  

## Chris Richardson's Microservices Architecture Pattern[6]
Chris Richardson, who was an architect at Netflix and a prominent author, trainer and a very prominent advocate of lightweight architectures, maintains a web site on Microservices Architecture where he has captured several software architecture patterns that are commonly used in Microservices Architecture Style.   

The site uses famous Gang of Four (GoF) Architecture Pattern documentation template to document Microservices Architecture Pattern. The pattern has concepts very close to one defined by Martin Fowler that we covered earlier. We will not reproduce that pattern here but direct the reader to read the pattern on the [microsercices.io](https://microservices.io/) website.

## Final Thoughts
Martin Fowler's definition is often used as an industry reference point. Real world pragmatism, particularly when migrating from legacy applications will relax a few constraints from the definition to meet needs in a given context. For example it may not be possible to have a database server per microservice.

## What Microservices are not!
Just as important it is to understand what microservices architecture is, it is equally important to understand what it is not. There is a common misunderstanding that microservices are APIs. The fact is they are not APIs. A second misunderstanding is that the architecture requires use of RESTful API, it doesn't.

Irakli Nadareishvili co-author of the book “Microservice Architecture: Aligning Principles, Practices, and Culture" [7] states that:   
“Microservice architecture is the implementation of your system, it is not public API Interface of your system that external or most internal client should depend directly on"  

The following diagram illustrates the relationship between an API and a Microservice:
![Microservices are not APIs](https://github.com/sandwi/curated-lists/blob/master/microservices/microservices-notes/microservices-are-not-apis.png)  
  
**Figure 1** Microservices are not APIs - they are implementation of a system (i.e a bounded context in DDD terms), APIs are public view and interface to the microservice

It is here the definitions provided by Martin Fowler [1] or Adrian Cockcroft [2] become important: a microservice is an application built using Microservices Architecture style, that is, it:   
* encapsulates the data with the business logic that operates on the data which provide a well-defined business capability i.e. the service is synonymous with a bounded context
* ensures only access to service is through a published service interface i.e. public API
* ensures no direct database access is allowed from outside the service, and there's no data sharing among the services i.e. each microservices has it's own database
* ensures it does not directly depend on any other service or database outside of its bounded context, i.e. loosely coupled, thus it can be independently deployed.

The public API can be RESTful or RPC based (such as using gRPC) or message based (reactive microservices, using RabbitMQ or Kafka for example).

## Microservices Architecture Characteristics
The table below shows charateristics of Microservices Architecture Style from Martin Fowler [1].  

| Characteristic | Notes | 
| -------------- | ----- | 
| Componentization via Services | A component is a unit of software that is independently replaceable and upgradeable Main reason for using services as components (rather than libraries) is that services are independently deployable |
| Decentralized Data Management | Bounded Context Master & Metadata Management becomes important |
| Organized around Business Capabilities | Conway’s Law of system design & communication | 
| Products not Projects | A team should own a product over its full lifetime Amazon's notion of "you build, you run it" |
| Design for Failure | Highly distributed in nature and failure is expected, so design for failure |
| Smart endpoints and dump pipes | Anti-ESB & SOA where pipes are complex, and intelligent |   |
| Evolutionary Architecture & Design |   | 
| Decentralized Governance | Independent microservice capability evolution with forward compatible service contracts |
| Stateless & Immutable | Services are designed to be stateless processes which enables fast starts and restarts and fast scaling (i.e. adding processes to scala horizontally) |
| Infrastructure Automation | DevOps Culture is mandatory |

## Does a Microservice Need its own Database Server?
As we stated earlier, the microservice's database is effectively part of the implementation of that service. It cannot be accessed directly by other services.  A common question in microservices architecture discussion is: does each microservice in an application comprising of one or more microservices need its own database server to host its database?  A purist answer is yes to support independent evolution, deployment and scaling of microservices. However, the pragmatic and practical answer is no. Because of licensing cost, infrastructure cost, operational & management cost, it may not be feasible to have a separate database server for each microservice. It should be noted that the use of public cloud and cloud architecture makes it cheap and easy to spin up database servers.  

There are a few different ways to keep a service's persistent data private. For example, if you are using a relational database then the options are:  
* Private-tables-per-service – each service owns a set of tables that must only be accessed by that service Schema-per-service – each service has a database schema that's private to that service Database-server-per-service – each service has it's own database server.
* Private-tables-per-service and schema-per-service have the lowest overhead. Using a schema per service is appealing since it makes ownership clearer. Some high throughput services might need their own database server.  
  
It is a good idea to create barriers that enforce this modularity. You could, for example, assign a different database user id to each service and use a database access control mechanism such as grants. Without some kind of barrier to enforce encapsulation, developers will always be tempted to bypass a service's API and access it's data directly.

See [Database per service](https://microservices.io/patterns/data/database-per-service.html), [Shared database](https://microservices.io/patterns/data/shared-database.html) and [Sagas](https://microservices.io/patterns/data/saga.html) for database patterns.

# References
1. Marty Fowler Bliki: [Microservices – a definition of this new architectural term](https://martinfowler.com/articles/microservices.html)
2. Adrian Cockcroft:  [Software Architecture Conference - Monitoring Microservices - A Challenge](https://www.slideshare.net/adriancockcroft/software-architecture-monitoring-microservices-a-challenge) - see slides 8-10 for definition
3. [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html) comes from Domain-Driven Design
4. Sam Newman's Book [Building Microservices: Designing Fine Grained Systems](https://www.amazon.com/Building-Microservices-Designing-Fine-Grained-Systems/dp/1491950358), 1st Edition
5. Werner Vogel on Amazon's use of services: [The 2006 ACM Queue interview with Werner Vogels](https://queue.acm.org/detail.cfm?id=1142065)
6. Chris Richardson's [Microservices Architecture Site](http://microservices.io/patterns/microservices.html)
7. Irakli Nadareishvili, Ronnie Mitra, Matt McLarty & Mike Amundsen: [Microservice Architecture: Aligning Principles, Practices, and Culture](https://www.amazon.com/Microservice-Architecture-Aligning-Principles-Practices/dp/1491956259)
8. [Domain-Driven Design: Tackling Complexity in the heart of Software](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215) , 1st Edition by Eric Evans
