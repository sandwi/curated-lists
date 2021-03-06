**Table of Content**
* [Microservices Architecture Introduction & Definitions](https://github.com/sandwi/curated-lists/tree/master/microservices#microservices-architecture-introduction--definitions)
* [Cloud Native Architecture](https://github.com/sandwi/curated-lists/tree/master/microservices#cloud-native-architecture)
* [Domain Driven Design](https://github.com/sandwi/curated-lists/tree/master/microservices#domain-driven-design)
* [Reactive Microservices with Command Query Responsibility Segregation (CQRS) & Event Sourcing](https://github.com/sandwi/curated-lists/tree/master/microservices#command-query-responsibility-segregation-cqrs--event-sourcing)
* [Microservices & APIs](https://github.com/sandwi/curated-lists/tree/master/microservices#microservices--apis)
* [Distributed Tracing](https://github.com/sandwi/curated-lists/tree/master/microservices#distributed-tracing)

# Microservices Architecture Introduction & Definitions
* Martin Fowler's Bliki write on microservices, [Microservices - A definitions of this new architectural term](https://martinfowler.com/articles/microservices.html)
* Adrian Cockroft [Software Architecture Conference - Monitoring Microservices - A Challenge](https://www.slideshare.net/adriancockcroft/software-architecture-monitoring-microservices-a-challenge) - see slides 8-10 for definition
   * [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html) - Adrian defines Microservices using DDD term Bounded Context
* Sam Newman's book [Building Microservices: Designing Fine-Grained Systems](https://www.amazon.com/Building-Microservices-Designing-Fine-Grained-Systems/dp/1491950358)
* Werner Vogel on Amazon's use of services: [The 2006 ACM Queue interview with Werner Vogels](https://queue.acm.org/detail.cfm?id=1142065)
* Chris Richardson [Microservices Architecture Site](http://microservices.io/patterns/microservices.html)
* Irakli Nadareishvili, Ronnie Mitra, Matt McLarty & Mike Amundsen [Microservice Architecture: Aligning Principles, Practices, and Culture](https://www.amazon.com/Microservice-Architecture-Aligning-Principles-Practices/dp/1491956259)

# Cloud Native Architecture
* [The Twelve Factor Application Architecture](https://12factor.net/)
* [Pivotal on Cloud Native Application Architecture](https://pivotal.io/cloud-native)
* Sam Newman's book [Building Microservices: Designing Fine-Grained Systems](https://www.amazon.com/Building-Microservices-Designing-Fine-Grained-Systems/dp/1491950358)
* Neal Ford & Rebecca Parsons (ThoughtWorks): [Microservices as an Evolutionary Architecture](https://www.thoughtworks.com/insights/blog/microservices-evolutionary-architecture)
* [Fallacies of Distributed Computing](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing)
  * [Fallacies of Distributed Computing Explained](http://www.rgoarchitects.com/Files/fallacies.pdf)
* Martin Fowler on [Microservices Pre-requisities](https://martinfowler.com/bliki/MicroservicePrerequisites.html)
* Martin Fowler on [DevOps Culture](https://martinfowler.com/bliki/DevOpsCulture.html)
* [Semantic Versioning](https://semver.org/)

# Domain Driven Design
* [Domain Driven Design: Tackling Complexity in the heart of Software , 1st Edition](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215) by Eric Evans
* Martin Fowler on [Domain Driven Design](https://martinfowler.com/tags/domain%20driven%20design.html)
* [Implementing Domain Driven Design](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577) by Vaughn Vernon
* [Domain Driven Design Community](https://dddcommunity.org/)
* [Domain Driven Design Reference](https://domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf) by Eric Evans
* [DDD and Microservices: At Last, Some Boundaries!](https://www.youtube.com/watch?v=yPvef9R3k-M) by Eric Evans 
* [Domain Driven Design for Services Architecture](https://www.thoughtworks.com/insights/blog/domain-driven-design-services-architecture)
* [Domain-Driven Design – What is it and how do you use it?](https://airbrake.io/blog/software-design/domain-driven-design)
* Bounded Context and Aggregates play a major role in Microservices Architecture as these concepts are used for defining Microservices boundary and right sizing Microservices
  * Martin Fowler on [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html)
  * [Bounded Context Explained](https://blog.sapiensworks.com/post/2012/04/17/DDD-The-Bounded-Context-Explained.aspx)
  * Adrian Cockroft, Bounded Content on Twitter: https://twitter.com/adrianco/status/871367419813429249
  * Martin Fowler on [Aggregates](https://martinfowler.com/bliki/DDD_Aggregate.html)
  * [DDD Decoded - The Aggregate and Aggregate Root Explained](https://blog.sapiensworks.com/post/2016/07/14/DDD-Aggregate-Decoded-1)
  * [Aggregates and Entities in Domain-Driven Design](http://thepaulrayner.com/blog/aggregates-and-entities-in-domain-driven-design/)

# Reactive Microservices with Command Query Responsibility Segregation (CQRS) & Event Sourcing
* Martin Fowler on [CQRS](https://martinfowler.com/bliki/CQRS.html)
* Martin Fowler on [Event Sourcing](https://martinfowler.com/eaaDev/EventSourcing.html)
* CQRS Frameworks
  * Axon Framework
    * [Axon Framework](https://axoniq.io/)
    * [Axon Framework Github](https://github.com/AxonFramework/AxonFramework)
    * [A Guide to the Axon Framework](https://www.baeldung.com/axon-cqrs-event-sourcing)
  * [Lagom Framework](https://www.lagomframework.com/)
    * [Lagom Github](https://github.com/lagom/lagom)
    * [How the Lagom Framework Enables Scalable Reactive Microservices](https://medium.com/@jgwest/how-the-lagom-framework-enables-scalable-reactive-microservices-in-java-and-scala-cd8b15c0a3ad)
    * [Guide to Reactive Microservices Using Lagom Framework](https://www.baeldung.com/lagom-reactive-microservices)

# Microservices & APIs
Its important to emphasize that microservices are not APIs and vice versa.  
Microservices are full systems in their own right and their capabilities are accessed via their public APIs.  
Public APIs can be REST, gRPC or message based as in Reactive Microservices or any other protocol, REST happens to be the most popular.

## Experience APIs
* [Daniel Jacobson on Ephemeral APIs and Continuous Innovation at Netflix](https://www.infoq.com/news/2015/11/daniel-jacobson-ephemeral-apis) - An excellent interview on APIs
  * Ephemeral APIs vs Experience APIs `Experience APIs are trying to handle an optimized response for a given requesting agent. That's orthogonal to the ephemeral APIs. The experience API is more about the requesting pattern and the payload. Ephemeral API is more about the process of iterating and evolving the experience APIs.`
* [API Mediation: Why You Need an API Experience Layer](https://nordicapis.com/api-mediation-why-you-need-api-experience-layer/)
* Netflix Blogs - Excellent read when thinking about APIs and microservices
  * [Why REST Keeps Me Up At Night](https://www.programmableweb.com/news/why-rest-keeps-me-night/2012/05/15)
  * [Engineering Trade-Offs and The Netflix API Re-Architecture](https://medium.com/netflix-techblog/engineering-trade-offs-and-the-netflix-api-re-architecture-64f122b277dd)
  * [Embracing the Differences : Inside the Netflix API Redesign](https://medium.com/netflix-techblog/embracing-the-differences-inside-the-netflix-api-redesign-15fd8b3dc49d)

# Distributed Tracing
Observability is an important operational requirement in microservices architecture. 
* Google Dapper Paper on Distributed Tracing, [Dapper, a Large-Scale Distributed Systems Tracing Infrastructure](https://ai.google/research/pubs/pub36356)
* [Open Tracing](https://opentracing.io/) - An open specification
* [Open Zipkin](https://zipkin.io/) - Originally created by Twitter based on Google Dapper paper
* CNCF [Jaeger](https://www.jaegertracing.io/) - Originally created by Uber, again inspired by Google Dapper paper
* New Relic [Distributed Tracing](https://docs.newrelic.com/docs/understand-dependencies/distributed-tracing/get-started/introduction-distributed-tracing)
