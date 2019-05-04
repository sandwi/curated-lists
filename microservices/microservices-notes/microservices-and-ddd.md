# Microservices and Domain-Driven Design
Domain-Driven Design (DDD for short) and design patterns accompyning it has been used in the industry for over a decade to tackle complexity of enterprise software development.
Domain-Driven concepts were introduced by Eric Evans in the seminal work in his book Domain-Driven Design: Tackling Complexity in the heart of Software , published in 2003. 
DDD principles are particular for Microservices Architrcture style, the DDD principles provide an approach to decomposing an application and identify or right size a microservice.

DDD is an approach to software development for complex needs by connecting the implementation to an evolving model [2][5]. The premise of domain-driven design is the following:  
placing the project's primary focus on the core domain and domain logic; basing complex designs on a model of the domain; initiating a creative collaboration between technical and domain experts to iteratively refine a conceptual model that addresses particular domain problems.

Domain-driven design is not a technology or a methodology. DDD provides a structure of practices and terminology for making design decisions that focus and accelerate software projects dealing eith complicated domains [2][5].
Let's define term domain before we look at DDD design patterns that help in building an application using Microservices Architecture.  

**Domain:** It is a sphere of knowledge and activity around which the application logic revolves. It is what an organization does and the world it does it in.
DDD includes a set of design patterns that enable domain experts and software development teams to tackle complexity. 

The key patterns that apply to Microservices Architecture style are:  
* Bounded Context: Bounded Context is a central pattern in Domain-Driven Design. It is the focus of DDD's strategic design section which is all about dealing with large models and team with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.
* Ubiquitos Language: It is the practice of building up a common, rigorous language between developers and users, to connect all the activities of the team with the software. Every term and unambiguous definition . This language should be based on the Domain Model used in the software. It it used consistently in speech, documentation, diagrams and code.
* Aggregate: It is a cluster of domain objects that can be treated as a single unit. An aggregate will have one of its component objects be the aggregate root. Any references from outside should only go to the aggregate root. The root can thus ensure the integrity of the aggregate as a whole. Aggregates are the basic element of transfer of data storage ­ you request to loa whole aggregates. Transactions should not cross aggregate boundaries.
* Entitities : are objects which have an identity which remains the same throughout the states of the software. Entities must be distinguished from other similar objects having the same at unique Identity (e.g. Joe's Bank Account). Entities in DDD have behavior (think of them as Business Objects with attributes and behavior in a domain).

## Bounded Context, Aggregates and Microservices
