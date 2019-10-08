# API Naming Conventions
# Capitalization and Delimitation
## URI Path Components: lowercase-hyphen-delimited-words
Examples:  
/credit-card/accounts  
/customers/profiles/risk-assessment  
/partner-card/accounts  

## Custom HTTP Headers: Capitalized-Hyphenated-Words
* Api-Key
* User-Id
* Client-Correlation-Id

## Query Parameters and Body Parameters: camelCaseWithLeadingLowercase
* transactions
* overLimitAmount
* ?customerId=12345

## Enumerated Values: ALL_CAPS_DELIMITED_BY_UNDERSCORE

| Style | Examples |
| ----- | -------- |
| UNDERSCORE | VERIFICATION_REQUIRED, PHONE_CALL |

## Prefixes
Prefixes aren’t treated as separate words.  
  
| Wrong | Right |
| ----- | ----- |
| isMultiCard | isMulticard |
| declinedReasonSubType | declinedReasonSubtype
| inEligibleTransactions | ineligibleTransactions |

## URI Path Components
If a URI path component corresponds to a collection of resources, the path component is plural:  
* /retail-card/accounts is a collection of credit card account instances.
* /retail-card/accounts/{accountId}/offers is a collection of offers that have been extended to a particular credit card account.
  
URI path components that don’t identify a collection are singular.

## Everything else
If an element carries a tuple value (one or more interdependent or ordered values), the element’s name is singular. The most common tuple is the singleton:  
* “overLimitAmount”: 500.00
* “creditCardExpirationDate”: “2018-06-30”
* /deposits/accounts?accountId=12334
  
Higher order tuples should not be mistaken for unordered lists or arrays. The two properties in the following examples carry more than one datum, but the collected values express a single “thing”; thus, the properties names are singular:
* “geolocation”: “-50.234, 83.543”
* “aspectRatio”: [16,9] or 16:9
  
If the value of an element is a list or an array of independent, unordered values, the element’s name is plural:
* transactionIds: “12345, 98765, 56789”

## Abbreviations
In general, names must not be abbreviated or truncated:

| Incorrect | Correct |
| --------  | ------- |
| lob | lineOfBusiness |
| prodNm | productName |
| relTyp | relationshipType|
  
## Acronyms
Acronyms are permitted when the acronym is more widely known than the full form of a word or phrase:  
* Common terms: gif, png, pin, vin, pdf and so on.
* Banking specific terms: aba (American Bankers Association), pan (Primary Account Number) and so on.

An acronym’s capitalization follows the expected camel case style:  
* reportAsPdf 

## Restricted Terms
The following terms should be avoided when composing element name:  
* Request
* Response
* Field
* Element
* Attribute
* Property
* Operation
* Array
* List
* String
* Integer
* Boolean
* Float
