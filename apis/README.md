**Table of Content**
* [REST API Principles](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#rest-api-principles)
* [API Management Platforms](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#api-management-platforms)
  * [Open Source](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#open-source)
* [API Design and Documentation](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#api-design-and-documentation)
* [API Versioning](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#api-versioning)
* [Experience APIs](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#experience-apis)
* [API Security](https://github.com/sandwi/curated-lists/blob/master/apis/README.md#api-security)

# REST API Principles
* Roy Fielding's Phd Dissertation [Architectural Styles and
the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) that defined REST
  * [Chapter 5 Representational State Transfer (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
* [REST on Wikipedia](http://en.wikipedia.org/wiki/Representational_state_transfer)
* [Google API Design Guide](http://apistylebook.com/design/guidelines/google-api-design-guide)
* [Microsoft REST API Guidelines](https://github.com/Microsoft/api-guidelines)
* [Enterprise Integration using REST](https://martinfowler.com/articles/enterpriseREST.html)
* Marty Fowler on [Richardson Maturity Model - steps towards glory of REST](https://martinfowler.com/articles/richardsonMaturityModel.html)
* [5 Basic REST API Design Guidelines](https://blog.restcase.com/5-basic-rest-api-design-guidelines/)

# API Management Platforms
* [List by Nordic APIs](https://nordicapis.com/20-api-management-solutions/)
## Open Source
* [List by Tech Beacon](https://techbeacon.com/app-dev-testing/you-need-api-management-help-11-open-source-tools-consider)

# API Design and Documentation
* [Swagger](https://swagger.io/)
* [Open API Specification](https://swagger.io/specification/)
* [RAML](https://raml.org/)
* [jsonapi](https://jsonapi.org/)
* Tools
  * [Springfox for Java/Spring](https://springfox.github.io/springfox/docs/snapshot/)
  * [Swagger JavaScript Client](https://github.com/swagger-api/swagger-js)
  * [Swagger-JSDoc](https://www.npmjs.com/package/swagger-jsdoc)
  * [Swagger-UI-Express](https://www.npmjs.com/package/swagger-ui-express)
  

# API Versioning
* [Evolving HTTP APIs](https://www.mnot.net/blog/2012/12/04/api-evolution) by Mark Nottingham, argues for versioning using URI with only major numbers, however Mark is open to content negotiation as a good approach
* [Common Misconceptions about API Versioning](https://cloud.google.com/blog/products/api-management/common-misconceptions-about-api-versioning) by Google Cloud (Apigee team), argues for versioning using content negotiation
* [Versioning REST Web Services](http://barelyenough.org/blog/2008/05/versioning-rest-web-services/) by Peter Williams, argues for versioning using content negotiation
* [Your API versioning is wrong, that is why I decided to do it 3 different wrong ways](https://www.troyhunt.com/your-api-versioning-is-wrong-which-is/) by Troy Hunt, prefers content negotiation for versioning
* [Bad HTTP API Smells: Version Headers](https://www.mnot.net/blog/2012/07/11/header_versioning) by Mark Nottingham, argues for custom HTTP header for version is an anti-pattern and associated problems
* [RESTful API Versioning or a Black Hole](https://blog.restcase.com/restful-api-versioning-insights/), lists pros/cons of major API versioning approaches
* [Four REST API Versioning Strategies](https://www.xmatters.com/integrations-blog/blog-four-rest-api-versioning-strategies/), lists pros/cons of 4 major API versioning approaches

# Experience APIs
* [Daniel Jacobson on Ephemeral APIs and Continuous Innovation at Netflix](https://www.infoq.com/news/2015/11/daniel-jacobson-ephemeral-apis) - An excellent interview on APIs
  * Ephemeral APIs vs Experience APIs `Experience APIs are trying to handle an optimized response for a given requesting agent. That's orthogonal to the ephemeral APIs. The experience API is more about the requesting pattern and the payload. Ephemeral API is more about the process of iterating and evolving the experience APIs.`
* [API Mediation: Why You Need an API Experience Layer](https://nordicapis.com/api-mediation-why-you-need-api-experience-layer/)
* Netflix Blogs - Excellent read when thinking about APIs and API evolution
  * [Why REST Keeps Me Up At Night](https://www.programmableweb.com/news/why-rest-keeps-me-night/2012/05/15)
  * [Engineering Trade-Offs and The Netflix API Re-Architecture](https://medium.com/netflix-techblog/engineering-trade-offs-and-the-netflix-api-re-architecture-64f122b277dd)
  * [Embracing the Differences : Inside the Netflix API Redesign](https://medium.com/netflix-techblog/embracing-the-differences-inside-the-netflix-api-redesign-15fd8b3dc49d)


# API Security
* OAuth2: https://oauth.net/2/
  * RFC6749: https://tools.ietf.org/html/rfc6749
  * Diagrams for all OAuth2 Flows: https://medium.com/@darutk/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85
  * RFC6750 OAuth2 Bearer Token Usage: https://tools.ietf.org/html/rfc6750
  * Proof Key for Code Exchange (PKCE)
    * RFC7636: https://oauth.net/2/pkce/
    * High Level information: https://www.authlete.com/documents/article/pkce/authorization_request
  * Draft RFC, OAuth2 for Browser-Based Apps: https://tools.ietf.org/html/draft-parecki-oauth-browser-based-apps-02
* JSON Web Tokens (JWT)
  * RFC7519: https://tools.ietf.org/html/rfc7519
  * JWT: https://jwt.io
* JSON Object Signing and Encryption (JOSE) specifications
  * RFC7516 JSON Web Encryption (JWE): https://tools.ietf.org/html/rfc7516
  * RFC7515 JSON Web Signature (JWS): http://tools.ietf.org/html/rfc7515
  * RFC7516 JSON Web Keys (JWK): https://tools.ietf.org/html/rfc7517
  * RFC7518 JSON Web Algorithms (JWA): https://tools.ietf.org/html/rfc7518
  * JOSE Libraries
    * List of Libraries: https://openid.net/developers/jwt/
    * Java Nimbus Library: https://connect2id.com/products/nimbus-jose-jwt
    * JavaScript Panva Library: https://github.com/panva/jose

* OpenID Connect: https://openid.net/connect/
  * List of OpenID Connect Implementations: https://openid.net/developers/certified/
  
