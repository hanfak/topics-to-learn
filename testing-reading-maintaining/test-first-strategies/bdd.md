# Behaviour Driven Development/Design - BDD

- https://dannorth.net/introducing-bdd/
- BDD is an outside-in style and approach to TDD.
- BDD is not just about coding acceptance-style tests. First and foremost it requires stakeholders, QA, and developers to work together in order to define requirements (often in the form of very small stories).
- Stories along with their scenarios (if any) ensure that developers test drive the implementation based on the behavior that was asked for, and helps developers determine when they are truly done implementing a specific story (set of behaviors).
- In BDD, tests are mainly based on systems behavior
- In most cases, the Given-When-Then approach is used for writing test cases
  - the behavior is illustrated in a very simple English language, also known as a shared language. This helps everyone in the team responsible for development to understand the feature behavior.
- Typical flow
  - Describe behaviour
  - Write tests
  - run and fail
  - write code to pass test
  - Run and pass test
  - repeat
- At its core, BDD is about having conversations to help teams overcome misinterpreted requirements and delivery issues
  - it’s about promoting a shared understanding between team members as early as possible in a user stories lifecycle.
- BDD leverages the ATDD along with other techniques around conversations, collaboration and automation to ensure that a team delivers what the business wants this first time around.

## Benefits

- Helps reach a wider audience by the usage of non-technical language
  - Allowing the requirements to be defined in a standard approach using simple English
- Focuses on how the system should behave from the customer’s and the developer’s perspective
- BDD Is a cost-effective technique
- Reduces efforts needed to verify any post-deployment defects
- Providing several ways to illustrate real-world scenarios for understanding requirements
- Providing a platform that enables the tech and non-tech teams to collaborate and understand the requirements

## How

- Test names (methods) should be written in English sentences
- language is in  the form of documentation
  ```
  Given some initial context (the givens),  
  When an event occurs,  
  Then ensure some outcomes.
  ```
- when adopting BDD it’s important to focus on solving the problems of delivering the right thing and not on the automation technique
- Once the collaborative sessions are flowing a team may choose to capture examples from those conversations using the Gherkin syntax
- and then use the captured examples with automated tools to help guide what developers deliver, in what is known as outside in development.

- https://lizkeogh.com/behaviour-driven-development/
- https://medium.com/ft-product-technology/behaviour-driven-development-at-the-ft-46dc2991471d

## Issues

- Just as with ATDD, in gerneal it is not the devs who write the tests, but th testers/BAs who do it
  - This can lead to issues as described in [/libraries/yatspec.md]
  - You lose the ability to think of the design when the test and prod code are separated
  - test code written, can become a nightmare to work with after a while
  - Long feedback cycles, to add code to parse user tests, and to go from test to code
