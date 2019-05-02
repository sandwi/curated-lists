# API Resources: URI and Hierarchy
URIs play a critical role in communicating the capabilities of REST APIs. 

URIs are only those parts of the URL that appear after the HTTP scheme and domain i.e. everything after https://api.MyCo.com.

# URL Elements
The elements that make up an API URL are:

* The first element in the URL is accessibility i.e. private (only for private APIs) and the business domain or service. The business domain identifies the fundamental business area or capability or service.

* A resource represents a class of business objects. There are two type of resources:
  * An instance is an instantiation of a resource.
  * A collection is a resource that acts as a container for instances.
* A folder provides a way to organize resources (typically collections) that are related to each other.
* A query parameter is an additional piece of data that acts as an argument to the operation that the URL represents. Not all of these elements will be present in every API URL.

## Example
Here is a hypothetical URL that contains each of the elements:  
/retail-card/accounts/12345/statement-credit/offers?type=new&select=id
  
The URL elements that appear in the URL are listed and briefly described below.  
**Business Domain**  
* retail-card

**Resource**  
There are there resources in the URL:  
* accounts is a collection of retail credit card account instances.
* 12345 is the ID of an individual account instance.
* Offers is a collection of offers for accounts #12345.
  
**Collection**  
There are two collections, _accounts_ and _offers_.  

**Instance**
The account ID 12345, is used as a resource that identifies an instance of a credit card account.  
  
**Folder**   
The statement-credit folder contains a set of collections that pertain to account #12345. In the URL, we see the offers collection is contained within the statement-credit folder.

**Query Parameter**  
Query parameters are specified after the ? symbol; the & symbol is used to concatenate multiple query parameters. If the example, these are two query parameters: type & select.

## General Practices
### Approval Process for new business domains/services and resources
The names and meanings of a new URL business domains or services and resources are generally reviewed and approved by an API Management Platform or API Governance team.

### The order of elements in the URL path must echo the resource ontology

**ontology**  
The sequence of business domains and resources in the URL path must match ontology. Specifically, elements that are “further down” the path (to the right) are within the scope of the “higher up” elements.

Example:  
* A customer’s accounts: /customers/{customerID}/accounts
* An account’s transactions: /retail-card/accounts/{accountID}/transactions
  
### Abbreviations may not be used
Always use the full form of a word.  
* Correct: /deposits/accounts/{accountId}/transactions
* Incorrect: /deposits/accounts/{accountId}/txns

### Express resource as a thing rather than an action
Resource names are best expressed as noun phrases rather than verbs.  
Examples  
* Correct: /customers/{customerId}/accounts
* Incorrect: /customers/{customerId}/get-accounts

### Use a verb if the resource is truly functional
If the API that you are designing is truly functional – if it does something rather than act as a “thing” – then use a verb as the resource name. We refer to these ‘verb-like’ resources as functional resources. A functional resource may only use POST as the HTTP verb. If the resource requires other HTTP verbs, then it isn’t a functional resource and so shouldn’t use a verb phrase as its name.  
  
Example  
* Correct: POST /retail-card/validate-account-number
* Incorrect:  GET /retail-card/ account-number-validation

### Lowercase, hyphen-separated words for business domains and resources
If the name of a business domain or resource contains multiple words, the individual words must be hyphen-separated.
  
Examples  
* Correct: /customers/{customerId}/transfer-accounts
* Incorrect: /customers/{customerId}/transferaccounts

### camelCase words (query parameters)
The names of the query parameters are given in camelCase with a leading lowercase letter.

Example  
* Correct: /retail-card/accounts/{accountId}/tranactions?minAmount=100
* Incorrect: /retail-card/accounts/{accountId}/tranactions?min-amount=100

### File extensions are not allowed
Some data-retrieval web APIs allow the consumer to include a file extension at the end of the URL as way to specify the MIME type of the data that’s returned. Instead, you must use an Accept or Content-Type header to perform content negotiation.

Examples  
* Incorrect: /customers/{customerId}/customer-activity-log.json  
* Incorrect: /customers/{customerId}/customer-activity-log.pdf

## Business Domains
A URL’s business domain does two things:
* Ontological Scope: It places the API in a part of the ontology that’s either generally consumable by any client app, that’s private a particular app (or set of apps), or that’s provided by a third-party.
* Business Intent: For public APIs, it identifies the fundamental business area or capability.

### The business domain as it denotes ontological scope
There are 2 types ontological scope: Private and Public.

#### Private APIs (/private/{APPNAME})
API URLs that begin with /private/{APPNAME} are in the private business domain. These APIs aren’t published on the MyCo Developer Portal (API Catalog) and they aren’t accessible to API consumers. In order for a client app to invoke a private API, the app needs to “just know” where the API lives.

Example  
/private/paymentportal/debit-recon
/private/acquisition/retail-card/features/applicant-attributes
/private/BANKFRAUD/deposits/fraud/p2p

##### Reason for private APIs
The primary reasons for creating a private API are:
* These are primarily for internal use and never exposed publicly.
* You are creating an “integration API” that is meant to be called by other APIs only and never by actual clients.
* You are creating an API that orchestrates the invocation of other Public APIs as a convenience or performance enhancement for a client.
* You are creating a temporary API that will be replaced by a more polished version later, and the API doesn’t need to be widely broadcast.

#### Public APIs
If an API doesn’t start with /private, it is considered public. Public APIs are published on API Developer Portal and must conform to API Standards.

### The business domains as a line of business
Examples could (using banking industry):  
* Mortgage
* Investing
* Retail Banking
* Commercial Banking
* Credit-Cards
* Auto Loans

## Resources
Resources form the core of modern APIs. When you interact with an API, you are interacting with resources being exposed by that. An API resource may be thought of as an asset, a noun, or just a “thing”.

Examples  
* A collection of customers
* An individual account
* A customer’s address
* Permissions on an account
* A customer’s alert preferences

## The Collection/Instance Pattern
The collection/instance pattern denotes the representation of a collection of things i.e. instances, where all of the instances have the same structure. The pattern lets you interact with either the collection as a whole, or with individual items within the collection. The collection/instance pattern has these rules:
* Collection names are plural
* Instances are represented by URL path parameters, where te value of a parameter is typically an alphanumeric ID that is unique within the collection.
* The element following a collection in the URL must be an instance – you can’t follow a collection with folder, for example.

Examples  
* /users/{userId}
* /customers/{customerId}

## Folders
A folder is a resource that contains a set of collections or other folders.  
Examples  
money-movement is a folder.
* /customers/{customerId}/money-movement/transfers
* /customers/{customerId}/money-movement/transfer-accounts
* /customers/{customerId}/accounts/{accountId}/payments

## Query Parameters
Query parameters act as arguments to the operation that a URL represents.  

The most common use of a query parameter is to apply it as a filter criteria that refines the set of records that are returned in the response body of a GET method, either by quality (“give me posted transactions that took place between Jan 1st and March 31st), by quantity (“give me the top 50 transactions”), or by response body definition (“I only need customer names in alphabetical order”).

### Filter Criteria Query Parameters
#### Value Range Filtering
To create value range filter, use two query parameters, one that expresses the lower bound and another that expresses the upper bound of the values that are found in a specified property. The names are in one of these forms:  
  
from=<property>&to=<property>  
Or  
min=<property>&max=<property>  
  
which form you use depends on the type of data:  
* For continuous values use from and to. This includes all time values.
* For discrete values such as monetary amounts, use min & max.
  
Default  
If one of a pair of the range parameters is missing, the “missing” limit is unbounded.

Examples  
Retrieve transactions from Jan 1, 2018 throuh March 31 2018.  
* /credit-card/accounts/12345/transactions?fromDate=2018-01-01&toDate=2018-03-31
  
Retrieve all transactions greater than $100 or more:
* /retail-card/accounts/12345/transactions?minAmount=100

#### Pagination
If an API returns multiple records in array, it should define a pair of query parameters (limit and offset) that lets the consumer specify the subset (or “page”) of records that will be returned in the response:  
* limit is an integer that specifies the maximum number of records that will be returned.
* offset is the zero-based index of the first record that will be returned.
  
The parameters are applied after the records are filtered and sorted.  
Defaults  
* limit: The response should contain a reasonable number of records, as determined by the API. .
* offset: 0

Examples  
* /retail-card/accounts/12345/transactions?limit=50&offset=25
  
Pagination method 2: nextRecordKey  
For some APIs, it is not possible or practical to implement the limit & offset pagination method. In these cases its acceptable to implement nextRecordKey query parameter. The value of the parameter is a magic cookie (a string token) that is generated by the data source, and is passed back to the caller in a previous response.  

Default  
None

Example  
/retail-card/accounts/12345/transactions?nextRecordKey=ioe23e45

#### Sorting
This parameter applies to APIs that return multiple records, sort tells the API how to sort the records in the response. Sorting is applied before pagination.

The value of the sort parameter is a comma-separated list of sort directives in the form:
property	directive

where  
* property is the name of a response property given in dot-notation  
* direction is an optional token that gives the direction of the sort, either ASC (ascending) or DESC (descending). If the direction token is omitted, ASC is used.  
  
If the parameter contains multiple directives, later directives are used as tie-breaker for earlier directive (last one wins).
  
Default  
Each API must identify a single default sort directive.

Example  
Sort by merchant name first, and then by descending monetary amount:  
* /retail-card/accounts/12345/transactions?sort=merchant,amount|DESC

#### Total Record Count: count
The count parameter applies to APIs that return multiple records in an array. It’s a Boolean parameter that when to set to true tells the API to include count property in the response body. The count property gives the total number of records that the API has fund after filtering has been applied.

count is typically only used in conjunction with the pagination parameters.
  
Default false
  
Example  
/retail-card/accounts/12345/transactions?offset=50&limit=10&count=true

#### Response Property Inclusion: select
Select lists the properties that will be returned in the response body. The parameter’s value is a comma-separated list of properties given in dot-notation as they appear in the response.
  
**NOTE** select is a bandwidth reduction parameter and need only be used in operations that, by default, deliver sizable response bodies.  
  
Default  
If select is null, the response body should contain the full set of response properties as defined by the API.
  
Example  
/retail-card/accounts/12345/transactions?select=transactionId,amount,merchantName
