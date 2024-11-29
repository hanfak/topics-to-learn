# Quality Engineering

- Risk and Quality
- Releasing software is decided on risk
  - Risk: the probability of something going wrong which will affect the business in an adverse way (ie sales, reputation, unsubscriptions)
  - Risk Management: is handling and planning ways of preventing risk which is economic (time/money/resources) to the business
    - What is the impact of that risk happening and the probability of it happening
    - Focus on handling different types of risks (ie critical to non critical)
  - For example, 
    - Releasing software which has lots of bugs leads to poor sales, bad reviews. 
      - Reducing the risk can be done by testing and fixing bugs, to prevent bugs reaching customers
        - trying to find all bugs can take too long and cost too much
      - alternatively, can release wiht some bugs tested and a patch released later
      - alternatively, can live with some bugs cause they cost too much and not much of an issue
      - alternatively, can fix on demand
    - Some of these have different cost to benefit values, decisions need to be made 
- No matter how much you test, figure out scenarios there could be cases where some bug or somethign will break
- How to manage risk to ensure that a release of a product has quality and makes money
  - Quality: 
    - Usefulness: Meeting user needs and providing value.
        - Does what it is supposed to do
    - Correctness: Functioning as intended without errors.
      - Does what it was doing before release
    - Goodness: Delivering a positive, enjoyable user experience.
      - Does it in the expected way, does not break, not too slow, can handle failures
- 4 areas to handle the risk (risk management in quality)
  - prevent
  - Accept
  - Transfer
  - Observe and React

## prevent
- Where most of the testing happens
- Lowering the risk of something happening (issues) in production
- Not everything can be tested, so must be accepted and see in use, then fixed if needs to
  - either too costly, too hard
  - not thought about
- automated or manual
  - if testing or fixing the issue is too hard or costly, and not critical can leave the it in
## Accept
- Allowing certain risks based on analysis.
## Transfer
- Using third-party tools or insurance to mitigate risk.
## Observe and React
- Monitoring and responding to issues as they arise in production
- Done manually or automated
- Can be obversed by 
  - notified by user
    - directly - hotline, email
    - indirectly - reviews, social media
  - the software itself
  - anotther software monitoring (metrics/logs/probes) then alerting
- The information is ready to find and fix issue quickly
- Can be handled by
  - customer themselves
  - operations team (person/chatbot)
    - helping the customer fix it
    - fixing it themselves
    - or passing it on to others to fix (call out, engineers etc)
  - The software notices itself and applies some fix 
    - ie retry when http call fails
    - This invovles building this into the software (more risk)
  - Alerting based on some logic around some metric that goes wrong
    - this can be manually fixed
    - or automated 