# Communications between apps

## Inter app communications

### Http

#### REST

##### Contents

- XML
- Json

#### GraphQL

#### Webservice/SOAP

- Envelopes

### Files

#### FTP/SFTP

### Messaging

- ActivMq
  -
- jms
  - https://dzone.com/articles/java-message-service-jms
- Hessian

## how it gets the data

- pulling from the app/intermediary(message broker)
  - Making a request
    - on demand
    - scheduled (quartz)
  - https://en.wikipedia.org/wiki/Pull_technology
- Pushed from app/intermediary(message broker)
  - subscribed to it and when updates occurs (ie to database  or event or in flow) it will send a request to who needs it
    - Can do this on a schdule
    - if receiving app  is down, then it will not lose the request as it will still be on message broker. So when back up it can start to get these messages/data and process them. This prevents lost messages/data.
      - If app has high availability (ie via kubernetes), then can expect all messages to be sent and received, without losing any. Thus can rely on http as a means to communciate.
  - https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern
  - observer pattern
- Sockets

## sync or async

- request - response
- async req-response
- fire and forget
- publish subscribe
- message routing

-3 Message Exchange Patterns in Application Integration To Know About
## Intra app communications

- Sending messages to objects
  - Delegating to dependencies
