# Software Engineering

- The primary goal of engineering is to produce working systems (meet functional and non functional requirements)
  - beauty/elegance is not the main goal
  - ease of use, correctness, adoptability are higher goals
  - deliver customer deliverables (creating/maintaining/changing features) with:
    - the least amount of resources (money/time/constraints/regulations)
    - the highest possible quality within those resources
  - Engineering is an economic endeavour  
- Software engineering is the **application of an empirical, scientific approach to finding efficient, economic solutions to practical problems in software**.
  - must manage the complexity of the systems that we create in ways that maintain our ability to learn new things and adapt to them.

## Software

- software controls what computers do.
- Since there are an unlimited number of things that computers can do, there are an unlimited number of software programs developed for various kinds of computing tasks.
-  all software programs share some commonalities in how they are created and how they run on computers

## What?
- Managing complexity
- It is different to other forms of engineering.
- Knowing the requirements/aims and deciding on the best technologies/methodologies to use within the constraints used, for different timeframes within the area of software
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
- Understanding how software is developed inside out and deployed, allows us to design/engineer it better for functional and non functional requirements
  - Poorly designed and implemented software will not run fast on fast hardware.
  - Even well-designed software may not perform and scale optimally on fast hardware

## Layers

- Deals with levels of code to produce some product that solves a problem
- levels/abstraction
  1. System
  2. Subsystem
  3. Layers
  4. Components
  5. Classes
  6. Data and methods
- There is a separation between layers and components.
  - 3 and above is concerned with architecture
  - 4 and below is concerned with code

## Fundamental Concepts

- These are the building blocks of what many technologies/patterns/architectures that are used in software.
- All new software is built on these ideas either
  - to improve upon it
  - Fix Issues
  - Make it easier to use
- Any list will be different, esp in terms of grouping
- List
  - Knowledge & Approach
    - Domain specific, logical, problem solving, scientific approach, abstract thinking
  - How a computer works
  - Making a computer hardware or software do something via software
    - programming languages, operating systems etc, sync, async, parallel actions
  - Running software on hardware
    - deploying, maintaining, cloud
  - Communication via different modules
    - interfaces, api, protocols( http, tcp, jms), sync, async
  - Networking
    - internet, osi, tcp/ip, load balancing, proxy, tls, hardware
  - Creating software
    - version control, agile/waterfall, requirements, algorithms/rules
  - Data
    - persisting and querying data, database, files, caching
  - Constraints
    - speed, memory, -ilities, secruity
  - Works
    - tested, documented, used, can be fixed
  - People
    - communication

### Links

- https://readwrite.com/2008/07/22/top_10_concepts_that_every_software_engineer_should_know/
- https://medium.com/software-alchemy/basic-concepts-of-software-design-and-architecture-e302697a8e51

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

## Difficulty of software engineering

We cannot engineer a perfect solution or a solution that has everything
  - one, there are things we want that compete against each other, so need to make **trade offs**, and prioritise what we want
  - There are constraints
    - physical - hardware software works on
    - law/regulation
    - contracts - must use this software/service
    - time
    - money
    - number of developers, or number of good developers
    - non functional requirements
    - etc

Coding isn’t hard - if you are left alone to code what you want, when you want, how you want and keep the option to just give up when it gets too hard.

That’s the really hard bit: we can’t do that.

Write code is simple, but the more things it needs to do or add it becomes more difficult

Simple amateur coding is trivial and most people can do it. Making an Excel spreadsheet or script, probably making ten or twenty lines of code in a programming language is something most people could do or learn to do.

As a professional, two factors mess that up:
  - Figuring out what to code.
    - You just get asked, say, ‘Can you make it email me if more than five expense claims get rejected on the same day for the same person?’. How do you code that?
  - Fitting it in to existing code.
    - You have to figure out how to fit your new code in to the existing code without breaking it. It might be millions of lines you have never seen. it might be very badly constructed and might break on small changes.

And then, we want to do better as professionals.

We want our code to have automated tests, which changes how you design it a bit.

We want it to be easy to deploy to computers, so you have to design that in.

We want it free from security holes, to keep data safe.

We want to never corrupt any data.

We want our colleagues to easily read and easily change our code, which needs designing in.

We want our code to be robust and correctly handle bad data, bad user input and anything else ‘unexpected’. We have to learn to expect that.

We want our code to be maintainable and extendable, without rewriting or making lots of changes or getting lost or taking lots of time

We want documentation for different people (developers, business, testers)

We need to communicate with others, using different language for other parties to understand us, what we are doing, what we need, how the app works or doesn't etc

We might need to work with other people (ie pairing) and this can be challenging

Then, our bosses want to know when all that is going to be ready, so they can plan around it. Once the TV advert goes live, that software better be running. Deadlines add pressure, so all these tricky bits need to be done under pressure

We have to juggle competing priorities of adding features, managing tech debt and fixing bugs. There’s no right answer for that. Somebody is always disappointed.

We have to cope with floods of new users and feature requests that are difficult to build. The whole ‘scalability’ piece is hard.

The code needs to stay running 24/7 or close to it - even if half the computers, disk drives, cooling systems, internet switches and electrical power fails.

We need to use existing libraries wherever we can, so we need to understand code we’ve not written. Tricky. But trickier still, we need to be part-time lawyers, because we have to check we are legally allowed to use that code without it affecting the business.

We have to solve bugs in production or while coding, we need to be a detective, but also plan ways of making it easy for us to spot issues or even better find or alert us to the problem or causes of the problems before they occur, we have to be able to quick fix things to make the client happy then find a better way (automated or manual) to deal with this

We need to remember somebody pays for all the computing our code runs on, so we have to make it play nice.

We have to work for and with people who range from fantastic humans to the sort you’d rather not spend time with. And with all ranges of skill levels.

We have to know so much about computing, engineering, the problem area (domain, business) we are creating requirements, solving, testing.

We can spend hours, failing and not getting it to work, we cannot give up. Sometimes there are no instant results, there are no clear path to a solution, there is no great feedback

We have to deal with people, politics, lack of motivation

We have to always be learning, new technologies, new patterns, languages, new domains, different conventions at different workplaces etc. The skill can grow weak with out practice

## Links

- https://www.computersciencedegreehub.com/faq/what-is-the-difference-between-software-engineering-and-software/
- https://medium.com/shakuro/programmer-vs-developer-vs-engineer-91ef374e5033
- https://www.rainerhahnekamp.com/en/modern-software-development/
- https://muldoon.cloud/programming/2020/04/17/programming-rules-thumb.html
- https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/
- https://medium.com/@vgonzalo/why-software-quality-really-matters-daee462e9e7d
- https://www.sivaprasadreddy.com/posts/2019/06/the-ugly-truth/
