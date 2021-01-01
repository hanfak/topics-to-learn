# Feedback Loops

- With feedback, we learn what went wrong, and make appropriate changes
- We all make mistakes, false assumptions, and we need ways to catch this early on
- Examples places to seek feedback
  - Because our product managers don’t know what they want, they find out from the customers. But customers get things wrong
  - Because our product managers don’t know everything about systems, they invite other experts to become stakeholders in the project. Stakeholders can be wrong
  - Because developers don’t know what to code, they find out from the product managers. What is coded can be wrong
  - Mistakes made during code occur, the IDE will pick these up, not all of them
  - Because developers make mistakes in understanding the existing code, developers use a statically typed language. The compiler corrects developer when they are  wrong.
  - Because developers make mistakes while thinking, they work with a pair. The pair corrects their pair
    - The same is true for code reviews on pull requests
  - Because both pairs are human and also makes mistakes, they write unit tests. The unit tests correct the pair when wrong.
  - Because there is a team that is also coding, code is integrated with other code. The code won’t compile or test's pass if wrong
  - Because the team makes mistakes, acceptance tests are written that exercise the whole system. Acceptance tests fail then wrong
  - Running acceptance tests is not manual process as this can be forgotten to be triggered. Instead the build will automatically run the tests
  - Because we didn’t think of every scenario, we get testers to explore the system. Testers will tell us if it’s wrong
  - Because we only made it work on one person's laptop, we deploy the system to a realistic environment. The tests will tell us if it’s wrong.
  - Because we sometimes misunderstand our product manager and other stakeholders, we showcase the system. Our stakeholders will tell us if we’re wrong.
  - Because our product manager sometimes misunderstands the people that want the system, we put the system in production. The people who want it tell us if we’re wrong
  - Because people notice things going wrong more than things going right, we don’t just rely on opinions. We use analytics and data. The data will tell us if we’re wrong
  - Because the market keeps changing, even if we were right before, eventually we’ll be wrong. Use data, to find this out
  - Because it costs money to get it wrong, we do all these things as often as we can. That way we are only ever a little bit wrong.
  - Don’t worry about getting it right. Worry about how you’ll know it’s wrong, and how easy it will be to fix when you find out. Because it’s probably wrong

## Risk

- Frequent releases reduce risk
- Risk is a factor of the likelihood of a failure happening combined with
the worst-case impact of that failure
  - Risk = Likelihood of failure × Worst-case impact of failure
  - an extremely low-risk activity is when failure is incredibly unlikely to happen and the impact of the failure is negligible
  - High-risk activities are when both sides of the product are high—a high likelihood of failure and high impact.
  - Large, Infrequent Releases Are Riskier
    - Risks include
      - outage
      - data loss
- Solution of testing everything is impossible
  -  We can test for the known scenarios, but we can’t test for scenarios we don’t know about until they are encountered (the “unknown unknowns”).
  - No matter how much you test, production is the only place where success counts
