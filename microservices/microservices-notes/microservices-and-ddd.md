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
* **Bounded Context:** Bounded Context is a central pattern in Domain-Driven Design. It is the focus of DDD's strategic design section which is all about dealing with large models and team with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.
* **Ubiquitos Language:** It is the practice of building up a common, rigorous language between developers and users, to connect all the activities of the team with the software. Every term and unambiguous definition . This language should be based on the Domain Model used in the software. It it used consistently in speech, documentation, diagrams and code.
* **Aggregate:** It is a cluster of domain objects that can be treated as a single unit. An aggregate will have one of its component objects be the aggregate root. Any references from outside should only go to the aggregate root. The root can thus ensure the integrity of the aggregate as a whole. Aggregates are the basic element of transfer of data storage ­ you request to loa whole aggregates. Transactions should not cross aggregate boundaries.
* **Entitities:** are objects which have an identity which remains the same throughout the states of the software. Entities must be distinguished from other similar objects having the same at unique Identity (e.g. Joe's Bank Account). Entities in DDD have behavior (think of them as Business Objects with attributes and behavior in a domain).

## Bounded Context, Aggregates and Microservices
**Context:** A context means a specific responsibility.  

**Bounded Context:** A bounded context means that responsibility is enforced with explicit boundaries.

The core idea of Bounded Context is that any given domain consists of multiple bounded contexts, and residing within each are things (doman model & business logic/capability/functionality) that needs to be communicated outside as well as things (domain model) that are shared externally with other bounded contexts. 

Given, a Bounded Context is “a specific responsibility enforced by explicit boundaries.”, if you want information from a bounded context, or want to make requests of functionality within bounded context, you must communicate with its explicit boundary using published interfaces.

Bounded Context is widely considered to be a starting point and prime candidate for a microservice in microservice architecture:  

* “One microservice should cover one bounded context” - Vaughn Vernon. 
* Sam Newman in [7] in chapter 3 "How to Model Services" uses a Bounded Context as the starting point for modeling a microservice
  
Key DDD principles of Ubiquitos Language, Aggregates, Aggregate Root and Entities - all reside and have a specific meaning within a Bounded Context.

Given microservices are organized around business capability, a Bounded Context is an excellent approach to modeling a microservice. 
   
While Bounded Context decouples domain logic, microservice decouples the technical decisions, performance, scalability, availability, robustness, security and so on. Since a Bounded Context has well-defined responsibility and explicit interface, it requires coordination and synchronization between teams.

Bounded contexts contain clusters of different data entities and processes that can control a significant area of functionality such as order fulfilment or inventory in an online ecommerce store.  Depending on the domain, they can actually be quite large. Hence another approach to defining microservice boundary and right sizing a microservices is needed in these domains. A more finely grained DDD unit is the aggregate which describes a cluster of objects and behaviors that can be treated as a single unit. An aggregate is regarded as the basic unit of data transfer – a classic example is an order that contains a bunch of line items.  

Aggregates [2][4] have following properties:  
* An Aggregate is a cluster of Entities and Value objects i.e. an Object Graph.
* Each aggregate is treated as one single unit.
* Aggregate boundary is transactional boundary i.e. Entities in an Aggregate are updated in one transaction.
* Each Aggregate has one root entity know as the Aggregate Root.
* The root identity is global, the identities of entities inside are local.
* External objects may have references only to root entity. Internal objects cannot be changed outside the Aggregate. 

An Aggregate can be modified from outside **only** via an Aggregate Root. In distributed environment, an aggregate is kept together on one server. And different aggregates can be distributed among nodes.

Given that an aggregate is a cohesive unit, it can be a reasonable indicator of the smallest meaningful scope for a microservice. It will be difficult to split an aggregate across service boundaries compromising service autonomy. Thus Aggregates also serve as an excellent boundary for a microservice.

However, choosing Aggregate as boundary of a microservice can lead to a very granular microservice and result in following problems:  
* Tends to give rise to anaemic services that do little more than expose CRUD-style methods
* degenerates to grouping data entities together rather than encapsulating business capabilities
* Can lead to a very “chatty” service infrastructure where the majority of processing time is spent on remote calls between services
  
Aggregate as a boundary for a microservice is useful in domains where a bounded context is large or anytime you find a bounded context that is very large and there is a need to find a smaller microservice.

Thus:  

```A microservice i.e. single deployable unit or service should be no bigger than a bounded context, but no smaller than an aggregate.```

Start with relatively broad service boundaries to begin with, refactoring to smaller ones as time goes on.

## Right Sizing a Microservice
Identifying and right sizing microservices is a challenging exercise. However there are software engineering and infrastructure engineering tools available that help in decomposing an application microservices. DDD is one such software engineering approach we discussed in the previous section. Building on DDD, the sections below provide criteria and guidlines for identifying and right sizing microservices.

### Domain Model / Business Logic
A microservice i.e. single deployable unit or service should be no bigger than a bounded context, but no smaller than an aggregate.  

Start with relatively broad service boundaries to begin with, refactoring to smaller ones as time goes on. Analyze the building blocks: Aggregate, Entities, Business Logic. Decompose Bounded Context, and hence microservice as Bounded Context grows over time and maintain Single Responsibility Principle.
  
DDD principles provide a logical and systematic way to model microservices. Microservices are not static, overtime they grow or shrink. Microservices is an example of Evolutionary Architecture [10]. It is important to continously monitor the and size of a microservice ensuring it is consistent with Single Responsibility Principle. Splitting microservices to enforce Single Resposibility Principle may be needed overtime.

### Technical, Deployment, Management & Operational 
Evaluate and consider following key technical aspects:   
* Deployment: Need for independent deployments to support Rate of Evolution & Change of business capabilities
* Scalability & Peformance: Ability to meet performance & scalability requirements without dependency on any other external system Microservices, following stateless process model can be scaled efificently.
* Reliability (Availabilty & Resiliency): Cloud Native & microservices architecture enables higher resiliency if platform and infrastructure is architected using cloud native/12 factor app architecture principles.
* Operational & Management Overhead: Ready for DevOps and Operational automation to overcome operational & management overhead that is natural with microservices architecture. This includes centralzed logging, monitoring and alerting.

### Team Size
Follow 2 Pizza Rule (teams shouldn’t be larger than what two pizzas can feed). A microservice can be reasonably developed, implemented and supported by a team of 5-8 engineers ("you build it, you run it") If you need larger team then the microservice is too big.
   
This is also consistent with Agile practices (scr SAFe) of smaller teams
