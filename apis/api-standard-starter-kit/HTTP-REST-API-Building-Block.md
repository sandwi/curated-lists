# HTTP - REST API Building Block  
The HTTP is the protocol all Web APIs and World Wide Web. Understanding of HTTP and REST semantics is vital to the API design and management. REST paper by Roy Fielding defines a number of architecture principles that underpin the World Wide Web architecture. One of the keys to REST API design is concept of resource. Having a resource orientation as you dive into the topic of HTTP semantics will help clarify the purpose and usage of these items, and bring the light the reasons why these semantics are so important to follow.  
  
## HTTP Methods (Verbs) 
The HTTP methods are: 
* GET: retrieves the resource specified by the request URI  
* PUT: replaces an entire existing resource instance with a new instance  
* DELETE: deletes a resource  
* PATCH: updates resource  
* POST: simply does something with the data that is passed. Typically, the thing it does is create an instance of the resource by the URI  
* OPTIONS: The HTTP OPTIONS method is used to describe the communication options for the target resource. It is required for support CORS and modern browsers enforce CORS via Pre-Flight flow before consuming a REST API endpoint
  
The following section looks at these HTTP methods. Please read HTTP RFC2616, RFC5789 and RFC7396 for details.

The implementation of an API operation (HTTP method or verb) is assessed as needing to be safe and idempotent.
* Safe means that the operation won’t modify the requested resource or any other resource  
* Idempotency means that any single invocation of the operation doesn’t generate side-effects that cause the subsequent invocations to return a different result. This doesn’t mean that successive invocations must return the same result, rather it only means that the invocation itself doesn’t cause the results to be different.

### GET
GET indicates a request to retrieve one or more resources. The request URI and query parameters identity the resource(s) that the server should return. If the server deems the request is valid (i.e. authenticated, authorized, acceptable), it responds with a representation of the resource(s) in either JSON or XML format depending on the content-type.

GET requests should be used to retrieve information about any type of addressable resource. Two important use cases are:
    • Retrieve a specific resource instance. The instance is usually identified by ID in the request URI.
    • Retrieve a list of instances of the same resource. The resource is identified by the name in the request URI. The se of instances that are returned may be filtered by using query parameters. 
#### HTTP Status Code
A successful GET request returns one for the following status codes: 
* 200: The requested information was successfully retrieved and can be found in the response body. Also used when a GET is issued for a collection and no matching items are returned in the response array.
* 203: The information that was retrieved was incomplete.
* 204: The information was successful; the response doesn’t contain body.
* 304: This is used if the If-Modified-Since header was included in the request. The 304 code means that the requested resource hasn’t been modified since the date given in the header, and so it isn’t returned in the body.

#### Safety and Idempotency
* The implementation of a GET method must be safe.
* The implementation of a GET method must be idempotent.

### POST
POST method has multiple uses:  
* To create a new resource instance. The request URI identifies the resource that the new instance is subordinate to. The new instance is populated with the data that’s provided in the message body. This is the most common use of POST.  
* For functional resources. This is an API that performs an action without acting on a true resource, hence it is known as a functional resource. For these cases, the resource name is modeled as a /verb-noun phrase, and must be called with a POST. APIs that validate data fall into this category. For example, to validate ABA routing number, POST /appname/validate-aba-number.  
* As a “secure GET”. There are cases where a resource that would be retrieved normally via a GET defines query parameters that contain sensitive data. However, the request URI that transmits these parameters is by nature unsecure. In these cases, the query parameters can be transmitted in the body of a POST method, and hence ensure security. Note that a GET request doesn’t allow a body. As with “functional” resources described earlier, the resource name is typically modeled as a /verb-noun phrase, e.e., /retrieve-account.  
* For partial updates of a resource. As with “functional” resources, described above, the resource name is modeled as a /verb-noun phrase, e.g. /update-account. Alternatively, partial updates can be implemented with a PATCH verb as well.
#### HTTP Status Code
A successful POST request returns one of the following status codes:
* 200: Used for validation, “secure GETs”, and partial updates.
* 201: Used for synchronous resource creation. The URI of the new resource must be returned in the Location header.
* 202: Used for asynchronous resource creation. The request was successfully received an validated by the server, but the requested resource hasn’t yet been created.
#### Safety and Idempotency
The implementation of a POST method that creates a resource:
* Cannot be Safe
* Cannot be idempotent

The implementation of a POST method that modifies a resource:
* Cannot be Safe
* Must be idempotent

### PUT
A PUT method has two use cases:
* To replace the resource identified by the request URI.
* To create a resource, where the ID of the new resource is known and specified by the client in the request URI.

#### HTTP Status Code
The most common success status for PUT requests are:
* 200: In cases where an exist resource has been replaced.
* 201: For cases where a resource has been created.
* 202: For cases when the request is successful, but the subsequent resource has not yet been created. This indicates that the server has accepted the request, and for the client to check back later to see if it has been created.

#### Safety and Idempotency
* The implementation of a PUT method cannot be safe.
* The implementation of a PUT method must be idempotent.

### PATCH
PATCH may be used to partially update a resource instance.  
* If an API supports PATCH, the body of the PATCH request must conform to the JSON Merge Patch specification described in RFC7396.  
* PATCH and POST are both acceptable for partial updates. With POST it is a “functional” resource use case that was mentioned with POST. 

#### HTTP Status Code
The most common success status for PATCH requests are:
* 200: For successful partial updates.
* 202: For cases when the request is successful, but the subsequent resource has not yet been updated. This indicates that the server has accepted the request, and for the client to check back later to see if it has been updated.
* 204: The update was successful; the response doesn’t contain a body.

#### Safety and Idempotency
* The implementation of a PATCH method cannot be safe.
* The implementation of a PATCH method cannot be idempotent.

### DELETE
A DELETE request deletes the resource identified by URI.  
Some resources support a “soft-delete”, where the resource is not completely removed, but instead is put into a state of restricted access or capability. For example, an account may be deactivated or a reservation may be cancelled, even though the underlying resources may still reside on the server. In such cases, it is best to consider the use case from the client’s perspective:
* If the client can no longer access the resource, such that a corresponding GET would return a 404, then this a deletion, and modeling a DELETE is appropriate.
* If a client can access the resource, and perhaps even re-instate the resource, then this is not deletion, so model a PATCH instead, which the client can use to alter a status parameter through a set of enumerated states.

#### HTTP Status Code
The most common success status codes for DELETE requests are:
* 200: In cases where a response body is needed (which should be rare). Note that once a resource has been deleted, a subsequent call to the same DELETE endpoint should result in a 404 Not Found error, not a 2xx, since the request to delete the resource cannot be fulfilled.
* 204: If the response doesn’t have a body.

#### Safety and Idempotency
* The implementation of a DELETE method cannot be safe.
* The implementation of a DELETE method cannot be idempotent.

### OPTIONS
The OPTIONS method is a somewhat obscure part of the HTTP standard that could be used today with a strong impact on the interconnectedness of the interwebs while requiring minimal effort. It’s role is well defined in RFC2616.  
To quote the spec:  
`This method allows the client to determine the options and/or requirements associated with a resource, or the capabilities of a server, without implying a resource action or initiating a resource retrieval.`

OPTIONS is used to implement [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) and its [pre-flight](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#Preflighted_requests) step.

`
Modern browsers (e.g Chrome, Firefox, Microsoft Edge, Safari etc.) implement CORS "preflighted" requests first, they send an HTTP request by the OPTIONS method to the resource on the other domain, in order to determine whether the actual request is safe to send. Cross-site requests are preflighted like this since they may have implications to user data.
`

#### HTTP Status Code
The most common success status codes for OPTIONS requests are:
* 200: The response usually is 200 OK with standard CORS headers. The CORS headers can be:
   * Access-Control-Allow-Origin: * or list of domains that are allowed to send requests
   * Access-Control-Allow-Methods: POST, PUT, DELETE, PATCH, GET, OPTIONS (list of HTTP methods that are allowed)
   * Access-Control-Allow-Headers: Content-Type, Accept, <Custom-Headers> (list of headers that are allowed)
   * Access-Control-Max-Age: 86400

#### Safety and Idempotency
* The implementation of an OPTIONS method is safe.
* The implementation of an OPTIONS method is idempotent.

## HTTP Status Codes
The HTTP specification defines a wide variety of acceptable status codes. However, we recognize a subset. The following sections provide
###  2xx Status Codes
#### 200 OK
Used as a catch-all response for successful operations. 200 is used for a success response to most GET requests. It is also used as the correct response for successful updates, or creates where a new resource does not have an accompanying URI.

#### 201 Created
Always used in conjunction with a successful POST or PUT that created a resource. A 201 must include a Location header that gives the URI address of the newly created resource.

#### 202 Accepted
The request has been accepted for processing, but the processing has not be completed. The entity returned with this response should include an indication of the request’s current status and either a pointer to a status monitor or some estimate of when the user can expect the request to be fulfilled.

#### 203 Non-Authoritative Information
203 HTTP status code is used to indicate partial success i.e. it means that the response is incomplete. The two most scenarios are:
    • The definition of a resource is spread across multiple servers, and one of these servers is down.
    • The complete list of resources that is supposed to be returned is compiled from multiple servers, and one or more of these servers are down. However, use of 203 is strongly discouraged. If a server is down, an API should return 500.

#### 204 No Content
The server has fulfilled the request but does not need to return an entity-body, and might want to return updated header information. The 204 response must not include a message body.

#### 207 Multi-Status
A multi-Status response conveys information about multiple resources in situations where multiple status codes might be appropriate.  

See https://httpstatuses.com/207 for more information on 207.

### 3xx Status Codes
The 3xx series of HTTP status codes would be used to redirect client to where the resource is available. The client will need to take additional action to access the resource.

#### 301 Moved Permanently
The requested resource has been assigned a new permanent URI and nay future references to this resource should use one of the returned URIs.   
  
The new permanent URI should be given by the Location field in the response. Unless the request method of HEAD, the entity response contain a short hypertext note with a hyperlink to the new URI(s).

If the 301 status code is received in response to a reqyest other than GET or HEAD, the user agent MUST NOT automatically redirect the request unless it can be confirmed by the user, since this might change to conditions under which the request was issued.

**Note:** When automatically redirecting a POST request after receiving a 301 status code, some existing HTTP/1.0 user agents will erroneously change it into a GET request.

(http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

#### 302 Found
The requested resource resides temporarily under a different URI. Since the redirection might be altered on occasion, the client SHOULD continue to use the Request-URI for future requests. This response is only cacheable if indicated by a Cache-Control or Expires header field.
The temporary URI SHOULD be given by the Location field in the response.
(http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

#### 304 Not Modified
The 304 response is used in cases of a GET request, where details from a previous request (cache information) are sent via request headers. If the requested resource has not been modified since previous request, the server may send back 304 response.  

### 4xx Status Codes
The 4xx status codes represent client-side errors.

#### 400 Bad Request
There was a syntax violation in the request. The most common instances are:  
* A required element is missing (could be a property or a query parameter).
* The wrong type of data was passed as the value of an element.

#### 401 Unauthorized
This response is given when a client request either lacks uer authentication information, or the authenticated user does not access to the requested resources.
  
#### 403 Forbidden
The server understood the request, but is refusing to fulfill it. Authorization will not help and the request SHOULD NOT be repeated. If the request method was not HEAD and the server wishes to make public why the request has not been fulfilled, it SHOULD describe the reason for the refusal in the entity. If the server does not wish to make this information available to the client, the status code 404 (Not Found) can be used instead.
(http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

#### 404 Not Found
Used when a parameter in the request URI cannot be mapped to a resource. This could be due to invalid URI or query parameter in the request (such as a customer id that doesn’t exist).

The server has not found anything matching the Request-URI. No indication is given of whether the condition is temporary or permanent.  The 410 (Gone) status code SHOULD be used if the server knows, through some internally configurable mechanism, that an old resource is permanently unavailable and has no forwarding address. This status code is commonly used when the server does not wish to reveal exactly why the request has been refused, or when no other response is app.
(http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

#### 405 Method Not Allowed
This response is sent when a client attempts to make a request with an HTTP method that not allowed for the resource specified by the request URI.

#### 406 Not Acceptable
The requested media type cannot be served. For example, if a client calls an API with Accept header set to application/pdf, the server may respond with 406 as the service supports only application/json and application/xml media types.

#### 409 Conflict
The request violates a business rule. For example, let’s say a widget object can only be deleted if its status is inactive. If the caller attempts to delete an active widget, the API should return a 409 error.

#### 415 Unsupported Media Type
This response is sent in cases where the client sends in a message body in a format that is not supported by the server. For example, if the server only accepts messages with a content type application/json and client sends in a message with a content-type of application/xml, a 415 may be returned.

#### 429 Too Many Requests
The API management/proxy layer issues this response when the requesting client has exceeded rate limits. Rate limits are specified at the management layer, and my differ based on requesting client, resource, HTTP verb, time of day, or other variable.

### 5xx Status Codes
The 5xx series of status codes are returned when the server is unable to service the request or an unexpected error has occurred on the server (such as exceptions, database errors, network errors etc.). The client can repeat the request at a later time.

#### 500 Internal Server Error
500 status code is returned when something has gone wrong on the server side. It is not necessary to indicate exact point of failure in the response to the client.

#### 503 Service Unavailable
The server is currently unable to handle the request due to a temporary overloading or maintenance of the server. The implication is that this is a temporary condition which will be alleviated after some delay. If known, the length of the delay MAY be indicated in a Retry-After header. If no Retry-After is given, the client SHOULD handle the response as it would for a 500 response.

(http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

## HTTP Headers
HTTP headers carry metadata about the message that is being sent or received by the client. This includes information such the desired and actual format of the payload, “correlation” identifiers that are used for logging and auditing. Headers shouldn’t be used to transmit be used to transmit information about the resource that is being addressed, such information can be found in the HTTP message body. The exception to this is the use of headers to convey identifiers for authenticated users (such Authorization header may include JWT that has has user info).

### Standard Request Headers
#### Accept (Request Only)
Lists the data formats, given as MIME types, that the client can accept in the body of the response, e.g. application/json.

#### Content-Type
Specifies the MIME type of the data that is in the message body.

#### Location (Response Only)
This Location header indicates the location, represented as a URI, of. Newly created resurce. APIs that return 201 status code are expected to return the location of the resource.

Example:  
  
HTTP/1.1 201 Created
Location: http://api.MyCo.com/users/1234567890

In the above example, the server has created a new resource, indicated by the 201 status code. This Location header provides the URI of the new resource.

### Custom Headers
New custom headers should be formatted as Title-Case-With-Hyphens.

#### Channel-Type
Channel-Type identifies the channel through which a customer invoked the API. Some examples:  
* Web
* MobileWeb (mobile browser)
* Mobile
* CSR
* IVR
* PartnerXXX

It’s the responsibility of each API that uses the Channel-Type header to list and describe the values the header takes.

#### X-Correlation-Id
Correlates HTTP requests between a client and server. Alternative names are X-Request-ID and Client-Correlation-ID.

## HTTP Message Body
Message bodies are the actual content of requests and responses. These bodies are usually transferred in JSON, although any content type is technically allowed as along as the server accepts it (XML, HTML, plain text etc.). The way the messages are sent and received over HTTP is called content negotiation.

