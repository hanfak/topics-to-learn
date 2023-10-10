# REST

- REST by its very nature is stateless, and is built in such a way that any web service that is compliant with REST can interact in a stateless manner with textual resource representations.
- REST is the fact that it is hypermedia rich. This ultimately means that in a REST API, the client and server are loosely coupled, which grants both clients and servers extreme amounts of freedom in resource manipulation.
- REST defines its interactions through terms standardized in its requests,

## Difference between rest and soap

- https://examples.javacodegeeks.com/enterprise-java/differences-between-rest-soap-apis/

## Performance

- when creating a web service that expects several client-calls at the same time, and uses a small payload as input and output, REST might be the better choice

## Advantage

- REST can be used cross-language which makes these web services flexible and scalable.
- REST is also widely used. A lot of people have experience with it and a lot of other web services (and clients) use REST. Having a REST web service makes it easier for other people to interact with your web service.
- Communication often happens using a JSON, which is human readable. This makes it easier for developers to determine if the client input is send correctly to the server, and back.
- But one of the main advantages of REST is that it does not need to setup a client. You just make a call to a server address .This even works if you just copy a REST server address (of a GET method) in your web browser. Other techniques, like gRPC, often require you to setup a client.
- Tools for in inspection, modification, testing are readily available
- Loose coupling between client and server makes changes relatively easy.
- Http status codes are well defined and helps in identifying cause of problems
- Using content negotiation and media types to communicate the format of requests and responses
- Using standard (DNS) naming and discovery network mechanisms
- Is a stateless protocol (between requests) that specifically expects that the client and server will exchange their states as part of each individual request. Being stateless, it accommodates network errors and the definitions of idempotency and limits on the number and types of verbs and reasonably strict definitions of their use also provide standard mechanisms for recovery.
- Specifically defines and accomodates naming, discovery, caching, chunking requests/replies, streaming, middleware cache and content distribution, network boundaries, security authentication and authorization etc.

## Disadvantages

- While creating RESTful services, most of us follow a standard practice of writing client library and all we need to do is update client library whenever there is a change in api contracts.
- Streaming is difficult and its highly impossible in most of the languages.
- Duplex streaming is not possible.
- Hard to get multiple resources in single request.
- Need semantic versioning whenever the api contract needs to be changed.
- REST typically sends everything it has all at once by default – the most complete request

## Good Practice

### Zalendo

- https://opensource.zalando.com/restful-api-guidelines/
1. General guidelines
- MUST follow API first principle
- MUST provide API specification using OpenAPI
- SHOULD provide API user manual
- MUST write APIs using U.S. English
- MUST only use durable and immutable remote references

2. REST Basics - Meta information
- MUST contain API meta information
- MUST use semantic versioning
- MUST provide API identifiers
- MUST provide API audience
- MUST/SHOULD use functional naming schema
- MUST follow naming convention for hostnames
3. REST Basics - Security
- MUST secure endpoints
- MUST define and assign permissions (scopes)
- MUST follow naming convention for permissions (scopes)
4. REST Basics - Data formats
- MUST use standard data formats
- MUST define a format for number and integer types
- MUST use standard formats for date and time properties
- SHOULD use standard formats for time duration and interval properties
- MUST use standard formats for country, language and currency properties
- SHOULD use content negotiation, if clients may choose from different resource representations
- SHOULD only use UUIDs if necessary
5. REST Basics - URLs
- SHOULD not use /api as base path
- MUST pluralize resource names
- MUST use URL-friendly resource identifiers
- MUST use kebab-case for path segments
- MUST use normalized paths without empty path segments and trailing slashes
- MUST keep URLs verb-free
- MUST avoid actions — think about resources
- SHOULD define useful resources
- MUST use domain-specific resource names
- SHOULD model complete business processes
- MUST identify resources and sub-resources via path segments
- MAY expose compound keys as resource identifiers
- MAY consider using (non-) nested URLs
- SHOULD limit number of resource types
- SHOULD limit number of sub-resource levels
- MUST use snake_case (never camelCase) for query parameters
- MUST stick to conventional query parameters
6. REST Basics - JSON payload
- MUST use JSON as payload data interchange format
- MAY pass non-JSON media types using data specific standard formats
- SHOULD use standard media types
- SHOULD pluralize array names
- MUST property names must be snake_case (and never camelCase)
- SHOULD declare enum values using UPPER_SNAKE_CASE string
- SHOULD name date/time properties with _at suffix
- SHOULD define maps using additionalProperties
- MUST use same semantics for null and absent properties
- MUST not use null for boolean properties
- SHOULD not use null for empty arrays
- MUST use common field names and semantics
- MUST use the common address fields
- MUST use the common money object
7. REST Basics - HTTP requests
- MUST use HTTP methods correctly
- MUST fulfill common method properties
- SHOULD consider to design POST and PATCH idempotent
- SHOULD use secondary key for idempotent POST design
- MUST define collection format of header and query parameters
- SHOULD design simple query languages using query parameters
- SHOULD design complex query languages using JSON
- MUST document implicit response filtering
8. REST Basics - HTTP status codes
- MUST use official HTTP status codes
- MUST specify success and error responses
- SHOULD only use most common HTTP status codes
- MUST use most specific HTTP status codes
- MUST use code 207 for batch or bulk requests
- MUST use code 429 with headers for rate limits
- MUST support problem JSON
- MUST not expose stack traces
9. REST Basics - HTTP headers
- MAY use standard headers
- SHOULD use kebab-case with uppercase separate words for HTTP headers
- MUST use Content-* headers correctly
- SHOULD use Location header instead of Content-Location header
- MAY use Content-Location header
- MAY consider to support Prefer header to handle processing preferences
- MAY consider to support ETag together with If-Match/If-None-Match header
- MAY consider to support Idempotency-Key header
- SHOULD use only the specified proprietary Zalando headers
- MUST propagate proprietary headers
- MUST support X-Flow-ID
10. REST Design - Hypermedia
- MUST use REST maturity level 2
- MAY use REST maturity level 3 - HATEOAS
- MUST use common hypertext controls
- SHOULD use simple hypertext controls for pagination and self-references
- MUST use full, absolute URI for resource identification
- MUST not use link headers with JSON entities
11. REST Design - Performance
- SHOULD reduce bandwidth needs and improve responsiveness
- SHOULD use gzip compression
- SHOULD support partial responses via filtering
- SHOULD allow optional embedding of sub-resources
- MUST document cacheable GET, HEAD, and POST endpoints
12. REST Design - Pagination
- MUST support pagination
- SHOULD prefer cursor-based pagination, avoid offset-based pagination
- SHOULD use pagination response page object
- SHOULD use pagination links where applicable
13. REST Design - Compatibility
- MUST not break backward compatibility
- SHOULD prefer compatible extensions
- SHOULD design APIs conservatively
- MUST prepare clients to accept compatible API extensions
- MUST treat OpenAPI specification as open for extension by default
- SHOULD avoid versioning
- MUST use media type versioning
- MUST not use URL versioning
- MUST always return JSON objects as top-level data structures
- SHOULD used open-ended list of values (x-extensible-enum) for enumerations
14. REST Design - Deprecation
- MUST reflect deprecation in API specifications
- MUST obtain approval of clients before API shut down
- MUST collect external partner consent on deprecation time span
- MUST monitor usage of deprecated API scheduled for sunset
- SHOULD add Deprecation and Sunset header to responses
- SHOULD add monitoring for Deprecation and Sunset header
- MUST not start using deprecated APIs
15. REST Operation
- MUST publish OpenAPI specification
- SHOULD monitor API usage
16. EVENT Basics - Event Types
- MUST define events compliant with overall API guidelines
- MUST treat events as part of the service interface
- MUST make event schema available for review
- MUST specify and register events as event types
- MUST follow naming convention for event type names
- MUST indicate ownership of event types
- MUST carefully define the compatibility mode
- MUST ensure event schema conforms to OpenAPI schema object
- SHOULD avoid additionalProperties in event type schemas
- MUST use semantic versioning of event type schemas
17. EVENT Basics - Event Categories
- MUST ensure that events conform to an event category
- MUST provide mandatory event metadata
- MUST use unique event identifiers
- MUST use general events to signal steps in business processes
- SHOULD provide explicit event ordering for general events
- MUST use data change events to signal mutations
- MUST provide explicit event ordering for data change events
- SHOULD use the hash partition strategy for data change events
18. EVENT Design
- SHOULD avoid writing sensitive data to events
- MUST prepare event consumers for duplicate events
- SHOULD design for idempotent out-of-order processing
- MUST ensure that events define useful business resources
- SHOULD ensure that data change events match the APIs resources
- MUST maintain backwards compatibility for events

## Links

- http://www.bizcoder.com/rpc-vs-rest-is-not-in-the-url
- https://www.guru99.com/restful-web-services.html
- https://medium.com/nerd-for-tech/designing-a-rest-api-3a070398750f
