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

## Disadvantages

- While creating RESTful services, most of us follow a standard practice of writing client library and all we need to do is update client library whenever there is a change in api contracts.
- Streaming is difficult and its highly impossible in most of the languages.
- Duplex streaming is not possible.
- Hard to get multiple resources in single request.
- Need semantic versioning whenever the api contract needs to be changed.
- REST typically sends everything it has all at once by default – the most complete request


## Links

- http://www.bizcoder.com/rpc-vs-rest-is-not-in-the-url
