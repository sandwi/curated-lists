[API Management](https://github.com/sandwi/curated-lists/wiki/API-Management)

**Table of Content**
* [REST API Principles](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#rest-api-principles)
* [API Management Platforms](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#api-management-platforms)
  * [Open Source](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#open-source)
  * [Commercial](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#commercial)
* [API Versionong](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#api-versioning)
* [API Security](https://github.com/sandwi/curated-lists/edit/master/apis/README.md#api-security)

# REST API Principles
<TBD>

# API Management Platforms
## Open Source

## Commercial

# API Versioning
* [Evolving HTTP APIs](https://www.mnot.net/blog/2012/12/04/api-evolution) by Mark Nottingham, argues for versioning using URI with only major numbers, however Mark is open to content negotiation as a good approach
* [Common Misconceptions about API Versioning](https://cloud.google.com/blog/products/api-management/common-misconceptions-about-api-versioning) by Google Cloud (Apigee team), argues for versioning using content negotiation
* [Versioning REST Web Services](http://barelyenough.org/blog/2008/05/versioning-rest-web-services/) by Peter Williams, argues for versioning using content negotiation
* [Your API versioning is wrong, that is why I decided to do it 3 different wrong ways](https://www.troyhunt.com/your-api-versioning-is-wrong-which-is/) by Troy Hunt, prefers content negotiation for versioning
* [Bad HTTP API Smells: Version Headers](https://www.mnot.net/blog/2012/07/11/header_versioning) by Mark Nottingham, argues for custom HTTP header for version is an anti-pattern and associated problems
* [RESTful API Versioning or a Black Hole](https://blog.restcase.com/restful-api-versioning-insights/), lists pros/cons of major API versioning approaches
* [Four REST API Versioning Strategies](https://www.xmatters.com/integrations-blog/blog-four-rest-api-versioning-strategies/), lists pros/cons of 4 major API versioning approaches

# API Security
* OAuth2: https://oauth.net/2/
  * RFC6749: https://tools.ietf.org/html/rfc6749
  * Diagrams for all OAuth2 Flows: https://medium.com/@darutk/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85
  * RFC6750 OAuth2 Bearer Token Usage: https://tools.ietf.org/html/rfc6750
* Proof Key for Code Exchange (PKCE)
  * RFC7636: https://oauth.net/2/pkce/
  * High Level information: https://www.authlete.com/documents/article/pkce/authorization_request
* JSON Web Tokens (JWT)
  * RFC7519: https://tools.ietf.org/html/rfc7519
  * JWT: https://www.jwt.io
* JSON Object Signing and Encryption (JOSE) specifications
  * RFC7516 JSON Web Encryption (JWE): https://tools.ietf.org/html/rfc7516
  * RFC7515 JSON Web Signature (JWS): http://tools.ietf.org/html/rfc7515
  * RFC7516 JSON Web Keys (JWK): https://tools.ietf.org/html/rfc7517
  * RFC7516 JSON Web Algorithms (JWA): https://tools.ietf.org/html/rfc7518
  * JOSE Libraries
    * List of Libraries: https://openid.net/developers/jwt/
    * Java Nimbus Library: https://connect2id.com/products/nimbus-jose-jwt
    * JavaScript Panva Library: https://github.com/panva/jose

* OpenID Connect: https://openid.net/connect/
  * List of OpenID Connect Implementations: https://openid.net/developers/certified/
  
