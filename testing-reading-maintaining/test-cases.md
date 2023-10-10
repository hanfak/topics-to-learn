# Test  cases

## For http communication

- successful response for the request sent
  - body returned
    - specific part which is important to your app
  - headers
  - status code
- Internal server error
  - status code 500
- 404 error
- Timeout
  - sockettimeout exception
- Succesful response but corrupted data in body
  - malformed json/xml
- Successful response but no data
  - like graphql, nulls in fields of response  ie not data for that request


## Equals and hashcode

- Reflexive
- Symmetric
- Transitive
- Consistent
- Non-nullity
- missing fields
- specific fields used only in checking equality

## Comparable

## Unmarshalling json/xml

- dont blow up
- optional fields


## Thread safety

- https://dzone.com/articles/how-to-test-if-a-class-is-thread-safe-in-java