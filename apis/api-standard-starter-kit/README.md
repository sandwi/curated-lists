# REST API Standard
**Table of Content**
1. [Guiding Principles](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/README.md#Guiding-Principles)
2. [HTTP: REST API Building-Block](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/HTTP-REST-API-Building-Block.md)  
3. [API Resources: URIs and the Hierarchy](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/API-Resources-URIs-and-the-Hierarchy.md)  
4. [API Versioning](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/API-Versioning.md)
5. [API Naming Conventions](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/API-Naming-Conventions.md)
6. [API Security](https://github.com/sandwi/curated-lists/blob/master/apis/api-standard-starter-kit/API-Security.md)

# Guiding Principles
   
* Minimalist: An API should contain only as many components (query parameters, body properties, HTTP headers and so on) as are needed to satisfy the target use cases. As an example, it’s not necessary to expose, in the response body, all of the fields that may be available from underlying services that the API uses.  
  
* Intuitive: An API should be easy to understand learn.  

* Documentation and Discoverability: Information about the APIs should be accurate, clear and complete, and it should be easy to find on the API Portal.   
   * On an API Portal: The application developers should be able to quickly navigate the Portal in order to find the information they need. This means the organization of the Portal, and the documentation library within, must be clean and intuitive. The information that the developers discover must be complete; the developers should not have to reach out to the API producers to understand how to use an API.  
   * Test & Learn: The application developers should be able to quickly try out the API with sample request and responses on the API Portal itself. 

* Conform to the HTTP design standards: APIs that leverage the semantics of the HTTP protocol have built-in advantages. Most important, application developers don’t need to read as much documentation or learn new standards in order to get up and running quickly. In addition, by conforming to HTTP semantics, the APIs will have a baseline consistency that will lower the learning curve for our internal API producers.

* Design APIs for use across clients and channels: APIs should not be built for the needs of a specific client or channel. API should be client agnostic, allowing any client application to take advantage of an API. This will increase re-use as well as reduce future work and allow more productive experimentation and testing of new and innovative applications built on a strong base of APIs.
  * [Experience API](https://www.infoq.com/news/2015/11/daniel-jacobson-ephemeral-apis) pattern can be used to provide client specific interfaces. The leaves the task of shaping request/response messages and traffic shaping to consumers of APIs who are driving a specific experiences.
