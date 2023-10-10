# Fixity

If you want to change something, hold it in place.

We write tests to hold down behavior. If behavior changes counter to our expectations, they fail.

Tests provide fixity. They allow us to change only what we want to change.

We use them as documentation and we run them before deployment to make sure everything is ok. Our tests also describe our intentions. In most development organizations, they are like load-bearing structure in a building. We depend upon them. Deleting a test is nearly unthinkable.

The tests we write and the names we use in our code describe our intentions. They tell the story of what we intended when we are programming. How long is this information useful?

Our hope is is that it is useful for the system's entire lifetime. And, in the best cases, it is. Unfortunately, team churn and business changes can decrease the value of that information over time. Intentions Fade. Reading code that was written more than 5 years ago by a different team involves a lot of guessing. We ask ourselves questions like: "Why did they want to do that?" or "What was the business context that led to this code?" Often it is very hard or impossible to get answers

Intention Fade is is another form of technical debt, a way that systems can become less understandable. We can refactor to keep it at bay, but we have more tools than we may think.

code has fixity also. If we hold our code constant, we are free to change our tests however we like.

We think that tests cover code, but in actuality tests cover behavior. They cover it through code. This means that code "covers" behavior as well. In fact, if we are lucky, code determines most of our system's behavior. It also fixes it; it holds it in place

t we can fix behavior through our tests or we can fix it through our code.

code is really the ground truth of a system. It describes what the system actually does rather than how it was intended to behave.

If intentions fade, we can hold behavior in place by not changing the code while we rewrite tests

We can also hold behavior in place with tests as we change names in the code to make today's intention clear.

we can interrogate the behavior of the system any time what we want to and record it as a description of ground truth.

Ground truth - information that is known to be real or true, provided by direct observation and measurement (i.e. empirical evidence as opposed to information provided by inference

When I characterize existing code, I look at it as a process of discovery. I start with an empty test and name it 'x.' Then I type a scenario, using existing methods that I am curious about and compare its result against some dummy value like 0 or the empty string. The test usually fails. When it does, I take the actual value that the test discovers and make it the expected value so that it passes. Then I change the name of the test from ‘x’ to a phrase that describes the behavior I've learned. It’s often right at that moment that I can discern an intention and run it past others for validation.

In short, I like approval tests to fix behavior in place for quick refactoring and framework-less characterization testing when I want to discover and document. They are two avenues toward the same goodness.