# The 5 Ideals

## Ideal 1: Locality and Simplicity

- The organizational environment must support DevOps. We can measure it with the “Lunch Factor”: how many people do we have to talk to over lunch to get things done? Reduce the lunch factor to a minimum.
  - Have fewer teams that can deploy more often independently.
  - Have an architecture that allows a fast turnaround time.
  - Developers must be empowered to work independently including that most integration tests must be run without an integrated staging environment (note: done right, contract testing might be a means to achieve that).
  - Developers should not have to understand a big codebase.
  - Developers must have the authority to deploy code to production.
  - Developers must not have to wait for other business units to get things done for them (like enterprise architecture review, database schemas, …).

## Ideal 2: Focus, Flow, and Joy

- Developers should solve the business problem and not spend most of their time on configuration and infrastructure tasks.
  - Put the infrastructure into a platform.
  - Reduce the lead time between code check-in and feedback to a minimum to connect the cause to the effect; ideally, know within seconds if a feature works or not.
  - Do trunk-based development to reduce the PR review and merge overhead.

## Ideal 3: Improvement of Daily Work

- We can only improve if we get feedback, so we should put as much feedback into our daily work as possible to get a little better each day.
  - Toyota had a cord along the assembly line that is expected to be pulled by any worker that sees a problem (the Andon Cord. If it’s pulled, they have 55 seconds to fix the problem, otherwise, the assembly line stops. The cord is pulled something like 3500 times a day (talk about feedback).
  - Big companies like Microsoft, Google, and Amazon only survived their technical debts because at some point they froze feature development.
  - The build time of Nokia’s own operating system Symbian was 48 hours before they “pulled the cord” and went with another OS (didn’t help them in the long run, though…).
  - Always take 20% off the development cycle to fix (or avoid) tech debt.
  - Enable greatness by having some engineers solely concentrate on dev productivity.
  - Have a virtual Andon Cord to fix things right when they happen.

## Ideal 4: Psychological Safety

- Only a psychologically safe environment allows for new ideas, innovation, and to learn from errors. An environment where you get bullied for each production error does not support a fast DevOps cycle, because everyone wants to be 100% certain that it works, which results in big deployments with slow processes and more things that can go wrong per deployment.

## Ideal 5: Customer Focus

- focus on the things that bring value to the customers instead of building functional silos and long internal decision chains within the organization.
