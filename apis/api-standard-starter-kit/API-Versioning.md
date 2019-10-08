# API Versioning
# API Version Increment
API Versioning is a necessity and yet a complex part of API evolution.
In general every effort should be made to keep APIs backward compatible. Hence API versioning consists of MAJOR version only.  
The Major version should be incremented when changes are made in a backward-incompatible way (breaking change), the change may negatively impact existing clients, such as:  
* Adding new required fields
* Changing the type of a field
* Removing fields
* Renaming fields or pathnames i.e. changing the URL format in the HTTP definition
* Changing an HTTP binding
* Changing payload structures
* Changing visible behavior of existing requests

Backward compatible i.e. non-breaking changes to API do not require a change in the API version number.         
These changes do not negatively impact existing clients, such as:  
* Adding optional fields to the request
* Adding fields to the response (an output-only resource field)
* Adding a value to an enum
* Adding new endpoints (e.g. adding a new method for an existing path)
* Adding an HTTP binding to a method

See [Semantic Versioning](https://semver.org/) & [Google Cloud API Versioning](https://cloud.google.com/apis/design/versioning).

# API Versioning Approaches
## API Versioning Using URI Path
In this approach API is part of the URI Path.
API versions apply to the API basepath, where basepath is the API base folder.
`<API-base-folder-name>/v<MajorVersion>/`    
Apply for credit card: URLs like: https://api.myco.com/credid-card/v1/apply  

Rationale:
* All resources under the API group in a business domain. When single resource changes, only that group version is incremented.
* Asserts mandatory version number
* Easy to use
  * Immediately visible
  * Browser friendly

### Who Uses It
* Google
* Facebook
* Twitter

### Pros
* Most popular approach to API versioning
* Version explicitly stated in the URI
* Enables version navigation and discover-ability
* Easy to share URL where user can easily consume API via browser
* Book-markable
### Cons
* Leads to multiple URIs for the same resource with different formatting (i.e. versions), which is against REST architecture principles (resource and hence resource identifier is one of the foundational building blocks of Web & REST)
  * New versions change resource name and location (even though underlying resource is same - same customer or same product)
* New versions break existing hyperlinks (book-markable but many bookmarks for same underlying resource!)
* Proliferation of URIs
* This approach has a pretty big footprint in the code base as introducing breaking changes implies branching the entire API i.e. a whole new tree of representations for the entire API.
* Version identifiers in the URI are also very inflexible. There is no way to simply evolve the API of a single Resource.

## API Versioning Using Content Negotiation
In this approach standard HTTP header `Accept` is used to specify API version by the client in the request. E.g.:  
* curl -X POST -H "Accept: application/vnd.myco.api+json; version=1.0" https://xxx/api/customers
* curl -X GET -H "Accept: application/vnd.myco.api+json; version=2.1" https://xxx/api/products

### Who Uses It
* [Github APIs](https://developer.github.com/v3/media/)
* [Capital One](https://developer.capitalone.com/)

### Pros
* Standard HTTP protocol semantics of [HATEOS](https://en.wikipedia.org/wiki/HATEOAS)
* Server advertises the resources and formats they support, and the client can pick and choose from them
* Keeps resource URI clean free of versioning - URI never changes i.e. resource name and location never changes
* Book-markable (but not easily testable - see cons)

### Cons
* Difficult to share URL where user can easily consume API via browser
* Version is hidden in header, not explicit
* Difficult to test (via browsers without plugins like postman or similar)
* HTTP caching can provide wrong/stale content

## API Versioning Using Custom HTTP Header
Versioning using Custom Version Header, e.g.:
* curl -H "Accepts-version: 1.0" https://xxx/api/customers
* curl -H "Accepts-version: 2.0" https://xxx/api/products

### Who Uses It
* [Yodlee](https://developer.yodlee.com/docs/api/1.1/getting-started)

### Pros
* Keeps resource URI clean free of versioning - URI never changes i.e. resource name and location never changes
* Book-markable (but not easily testable - see cons)

### Cons
* An attempt to re-invent content negotiation when its already defined using standard HTTP header with well understood semantics
* Being a non-standard header, intervening network devices (routers, firewalls etc.) can drop custom header or reject request entirely
* HTTP caching can provide wrong/stale content
* Difficult to share URL where user can easily consume API via browser
* If custom version header is not present, semantics of default version has to be well thought through
* Version is hidden in header, not explicit
* Difficult to test (via browsers without plugins like postman or similar)
* Leads to RPC style of interaction (like SOAP)

## API Versioning Using Query Parameter
Versioning using Query Parameters, e.g.:
/api/customers?version=1
/api/products?version=2

### Who Uses It
* Amazon
* Google
* Netflix

### Pros
* Book-markable
* URI doesn't change with new versions of the API, hence doesn't break hyperlinks
* Version explicitly stated in the Query Parameter
* Easy to share URL where user can easily consume API via browser
### Cons
* The service has to parse the version query parameter and then route request to correct version implementation
* Makes it harder to route requests to correct version of API
* If version query parameter is not present, semantics of default version has to be well thought through

## Recommendation
Versioning Strategy based on `Versioning Using Content Negotiation` is recommended because of standard HTTP protocol semantics of [HATEOS](https://en.wikipedia.org/wiki/HATEOAS). Server advertises the resources and formats they support, and the client can pick and choose from them.

* RESTful architecture purists prefer and recommend this approach because it adheres to [HATEOS](https://en.wikipedia.org/wiki/HATEOAS) principle where content is negotiated using HTTP standard headers "Accept" and "Content-Type" with no prior knowledge.
* Clearly separates resource (as expressed via URI) from format (as expressed via media type)
* The format of resource, as expressed by Accept header in request and Content-Type header in response is semantically clean, keeping resource same, just the format (version different) different
  * E.g. Specifying mp3 or mp4 for video is a good example of content negotiation
* Server must use HTTP [cache-control headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) in responses to indicate no caching where caching is not desired
  * Cache-Control: no-cache
  * Cache-Control: no-store

# Default Version
If an API consumer doesn't specify the version number then the the default version is the highest version number i.e. current version. This is needed for the following Versioning Strategies:
* Versioning Using Content Negotiation
* Versioning Using Custom Header
* Versioning Using Query Parameter

# API Version Support & Retirement
When a new version is created, the next-oldest version should continue to be supported for some time (at least 6-12 months) to give time for developers to update their applications.  As retirement deadlines approach, frequent notice to developers should be given so that they are aware of the upcoming change.  Once an API is retired, requests to that API should return a 404 Not Found status (if the API is completely gone) or 400 Bad Request (if new, required parameters were introduced, or old parameters removed).

