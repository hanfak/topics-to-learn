# Software Engineering

- It is different to other forms of engineering.
- It is about designing and making something that is soft, not hard.
- Soft is about easily changeable thing.
- SE make products that are soft, and apply principles, techniques, patterns and methodologies to create soft products
- Software development is not a formula to follow to the exact detail but a **recipe** open to creative interpretation of individual engineers (pairs/groups in discussion) to be adjusted according to the specific situation
   - It is not a paint by numbers job.
   - Right approach in on situation may be the wrong approach in another.
 - Generaly work in the unknown.
- Evey task is different
  - Devs think, visualise, model, embody models into code
  - Involes a lot of learning new things
  - Very hard to estimate and assure the managers you are doing the right things.
- Devs are knowledge workers
- Rely on better processes rather than more/better devs
- Devs work in the virtual/abstract domain
  - We cannot use the 5 senses
- Developing software is about making a series of the best trade offs for a given situation.
  - Understanding the implications of trade offs to help make better decisions
  - **There are not right or perfect choices**
- Due to the internet, open source, software dev is not about creating alogorithms for everything. Instead it is about knowing about libraries and using and combining these to create your product.

## Deliver Better Software, Faster

- keep your users happy
- Deliver
  - means taking responsibility for more than just writing and debugging code
  - You’re paid to make it easier for your users to do something they find valuable, and until your code is running in production, they won’t benefit from your hard work
  - Focus should be delivering software, rather than writing code
  - requires understanding the overall process for getting your changes into production
  - **Making sure you aren’t doing things that hinder the process**
    - like guessing the meaning of a vague requirement instead of asking for clarification before implementing it.
  - **Making sure you are doing things that speed up the process**
    - writing and running automated tests to show your code meets the acceptance criteria.
- Better Software
  - **building the right thing**
    - ensuring that what you’ve written meets all the requirements and acceptance criteria.
  - **building the thing right**
    - writing code that is easily understood by another programmer so they can successfully fix bugs or add new features
    - These changes can be made easily
    - Understandability and changeability can be in conflict, with trade offs required
  - Beware things that can result in technical debt, which will increase time to delivery
    - Nonprogrammers might push developers to take shortcuts to deliver new features sooner, with promises to come back and “do it right” later
    - Sometimes programmers who just learned something will try to use it everywhere possible, even if they know a simpler solution would work just as well
- Faster
  - Applies to both delivery software and creating/maintaining better software
  - Speed is affected by the complexity of the task
    - Doing complex things at speed leads to mistakes
  - Solutions
    - TDD to create automated tests, integration, and user acceptance tests to verify the system’s behavior.
    - Building and running an automated process that runs all the tests in multiple environments and, assuming they all pass, deploys the code to production
      - continuous integration and continuous delivery
    - Code reviews and/or pair programming
  - deploy changes to production more often so each deployment has fewer changes and is therefore less likely to have problems, and your users get the benefits of your work sooner

## Software Engineering vs Coding

- Coding is about solving puzzles
  - Making sure you deliver a solution to the problem
  - Focus on correctness
  - Work in one area to fix a problem, with a set of requirements, when met task is done
  - Fixed tech and processes
    - ie language, database etc
  - To complete some goal
  - Dont care whether people liked the feature, or even whether it was in production.
- Engineering is about
  - Focusing on optimizing for change
  - how to improve thing
  - Met with business
    - participate in the negotiation between design and implementation
    - If a particular new feature took the code in an awkward direction, then dicussions with customer over other suggestions to solve the same problem
  -  **Help define the puzzles, as well as solve them**
  - Need to be able to code to be able to engineer
  - To provide a capability to the rest of the organization (or to the world); by operating a useful product
  - The end state is never set, it is a purpose rather than a goal
    - To create and continue to make a product useful
  - Use of already coded solutions (ie libraries/services/hardware) to help continue the lifecycle of the product
  - Focu on **system change**
    - How it interacts with other services/systems internally and externally
    - work with the people who own those systems to help them start using the new feature
      - ie developers, users, technical support, testers
  - Work is about **designing for change**
    - feature flags
    - backward compatibility
    - data migrations
    - progressive deployment
    - documentation
    - helpful error messages
    - social contact with adjacent teams
    - building in observability so can tell who is still using the deprecated feature, and who is getting value from the new one, or where errors occurs to fix them in code or manual process
  - Products don’t have one definition of “correct.” Many things are definitely not correct, so we can be careful about “not broken.” Beyond that, we aim for “better.
  - there is a slog of mushy work, through ambiguity and politics and context
    - it can have a real impact on your company and thereby the world
  - Greater understanding of everything, not just a fixed area
    - A lot to know and understand, can be overwhelming

## Links

- https://www.computersciencedegreehub.com/faq/what-is-the-difference-between-software-engineering-and-software/
- https://medium.com/shakuro/programmer-vs-developer-vs-engineer-91ef374e5033
- https://www.rainerhahnekamp.com/en/modern-software-development/
- https://muldoon.cloud/programming/2020/04/17/programming-rules-thumb.html
- https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/
- https://medium.com/@vgonzalo/why-software-quality-really-matters-daee462e9e7d
