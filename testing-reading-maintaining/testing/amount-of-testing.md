# How Much Testing is Enough?

“How much testing is enough to qualify a software release?”
- A lot depends on the type of software, its purpose, and its target audience
- can be hard to answer in definitive terms.

rules of thumb that can be used to define a qualification process and testing strategy best suited for the case at hand. The following tips provide a helpful rubric:

## Document your process or strategy.
  - If you are already testing your product, document the entire process. 
    - This is essential for being able to both repeat the test for a later release and to analyze it for further improvement. 
  - If this is your first release, it’s a good idea to have a written test plan or strategy. 
  - In fact, having a written test plan or strategy is something that should accompany any product design.
## Have a solid base of unit tests.
  - A great place to start is writing unit tests that accompany the code. Unit tests test the code as it is written at the functional unit level. 
  - Dependencies on external services are either mocked or faked.
  - A mock has the same interface as the production dependency, but only checks that the object is used according to set expectations and/or returns test-controlled values, rather than having a full implementation of its normal functionality.
  - A fake, on the other hand, is a shallow implementation of the dependency but should ideally have no dependencies of it’s own. Fakes provide a wider range of functionality than mocks and should be maintained by the team providing the production version of the dependency. That way, as the dependency evolves so does the fake and the unit-test writer can be confident that the fake mirrors the functionality of the production dependency.
  - there are best practices of requiring any code change to have corresponding unit test cases that pass. As the code base expands, having a body of such tests that is executed before code is submitted is an important part of catching bugs before they creep into the code base. 
    - This saves time later both in writing integration tests, debugging, and verifying fixes to existing code.
## Don’t skimp on integration testing.
  - As the codebase grows and reaches a point where numbers of functional units are available to test as a group, it’s time to have a solid base of integration tests. An integration test takes a small group of units, often only two units, and tests their behavior as a whole, verifying that they coherently work together.
  - Yet, having a comprehensive set of integration tests is just as important as having a solid unit-test base
  - integration tests have less dependencies than full end-to-end tests. As a result, integration tests, with smaller environments to bring up, will be faster and more reliable than the full end-to-end tests with their full set of dependencies
  
## Perform end-to-end testing for Critical User Journeys.
- test the product end to end as a user would use it. This is quite important because it’s not just independent features that should be tested but entire workflows incorporating a variety of features.
- the combination of a critical goal and the journey of tasks a user undertakes to achieve that goal

## Understand and implement the other tiers of testing.

understand the other tiers of testing, including:
- Performance testing 
  - Measuring the latency or throughput of your application or service.
- Load and scalability testing 
  - Testing your application or service under higher and higher load.
- Fault-tolerance testing 
  - Testing your application’s behavior as different dependencies either fail or go down entirely.
- Security testing 
  - Testing for known vulnerabilities in your service or application.
- Accessibility testing 
  - Making sure the product is accessible and usable for everyone, including people with a wide range of disabilities.
- Localization testing 
  - Making sure the product can be used in a particular language or region.
- Globalization testing
  - Making sure the product can be used by people all over the world.
- Privacy testing 
  - Assessing and mitigating privacy risks in the product.
- Usability testing
  - Testing for user friendliness.
- have these testing processes occur as early as possible in your review cycle. Smaller performance tests can detect regressions earlier and save debugging time during the end-to-end tests.

## Understand your coverage of code and functionality.

- Different types of tests were reviewed and the argument made that smaller and earlier is better than larger or later.
- from a quantitative perspective, taking code coverage techniques into account
- provide a summary in percentage terms. For example, 80% code coverage means about 80% of the code is covered and about 20% of the code is uncovered. At the same time, It is important to understand that, 
- **just because you have coverage for a particular area of code, this code can still have bugs.**
- Changelist coverage measures the coverage in changed or added lines. 
  - It is useful for teams that have accumulated technical debt and have low coverage in their entire codebase. 
  - These teams can institute a policy where an increase in their incremental coverage will lead to overall improvement.
- feature coverage, 
  - the emphasis is on identifying the committed features in a particular release and creating tests for their implementation. 
- For behavior coverage, 
  - the emphasis is on identifying the user journerys and creating the appropriate tests to track them. 
- Again, understanding your “uncovered” features and behaviors can be a useful metric in your understanding of the risks.

## Use feedback from the field to improve your process.

- feedback received from the field once the software has been released
  - Having a process that tracks outages and bugs and other issues, in the form of action items to improve qualification, is critical for minimizing the risks of regressions in subsequent releases.
- the action items should be such that they 
  - (1) emphasize filling the testing gap as early as possible in the qualification process and 
  - (2) address strategic issues such as the lack of testing of a particular type such as load or fault tolerance testing.

