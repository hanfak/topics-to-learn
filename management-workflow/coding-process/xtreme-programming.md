# Xtreme Programming (XP)

## what is it?

- methodology for teams that face of vague or rapidly changing requirements.
- only do what you need to do to create value for the customer.
- A way to: Stay aware. Adapt. Change.
- To help in improving the ability to cope with change
- Distinguished by
  - short development cycles.
  - incremental planning approach.
  - ability to be flexible when the business needs change.
  - reliance on automated tests.
  - reliance on oral communication.
  - reliance on an evolutionary design process.
  - reliance on the close collaboration.
  - reliance on practices that work with both the short-term instincts of the team members and the long-term interests of the project.

### Values of XP

- Communication
  - problems within a tema can be caused by lack of Communication.
    - this should be the first place to look at when problems occurs
  - How can your team now communicate in order to solve the problem and ensure that the same issue doesn't arise?
  - helps your team to bond and is a key component to effective cooperation
- Simplicity
  - Focus on working on the simplest thing that could possibly work
  - Eliminate unnecessary complexity
- Feedback
  - Shorten the feedback cycle as best as you can.
  - Too much feedback is counter productive
    - look to find the sweet point
  - Range of forms
    - Getting opinions from colleagues, books, internet
    - Evaluating code produced by yourself, others
    - How did testing feel
    - Did the code pass the tests
    - Does the code work
- Courage
  - Effective action in the face of fear.
  - Courage may manifest itself
    - in a bias to action
    - to be patient to wait for a problem to reveal itself when you feel one approaching
    - to wait for a problem to reveal itself when you feel one approaching
    - to change a course of action can lend itself to finding simpler solutions.
- Respect
  -  contributions of each person on a team has to be respected
  -  Needed for XP to work

### Principles

- Principles guide behaviour
- Principles give you a better idea of what a practice is intended to accomplish
- Main principles
  - Humanity
    - Creating software
      - should meet human needs, maslov
      - acknowledge human fallibility
      - leverage human strength
  - Economics
    - everything you do has business value and serves business needs
    - Think about the 'time value of money' and the 'option value of systems and teams'
    - What you're building is more valuable the more it earns money sooner and spends money later
    - How flexible is your software for being used beyondoriginally intended purpose
    - balance enhancing the option value of the software and the team whilst not wasting money investing in speculative flexibility
  - Mutual benefits
    - Every activity should benefit all concerned
  - Self-Similarity
    - Try copying the structure of one solution into a new context, even at different scales
  - Improvement
    - Aim for excellence through constant improvement
  - Diversity
    -  need to bring together a variety of skills, attitudes, and perspectives
  - Reflection
    - to expose mistakes and learn from them
    - How is your team working and why are they doing what they are doing?
    - Why did you suceed?
    - Why did you fail?
  - Flow
    -  delivering a steady flow of valuable software by engaging in all activities of development simultaneously
  - Opportunity
    - View problems as opportunities to learn, improve, and change
  - Redundancy
    - Keep redundancy where it serves a valid purpose, that is, uncovering defects. You may have many practices that catch the same defects, but the defect problem in general cannot be solved with a single practice
    - Defects corrode trust and trust is the great waste eliminator
  - Failure
    - use it to learn from
    - When you don't know what approach to take, risking failure can be the shortest route to success.
  - Quality
    - Sacrificing quality is not an effective means of control. Aiming for higher quality often results in faster delivery; lowering quality standards results in less predictably delivery later on
  - Baby Steps
    - What's the least you could do that is recognizably in the right direction?
    - ou want to avoid 'wastefully [recoiling] from aborted big changes'.
  - Accepted Responsibility
    - With responsibility comes authority.


### Practices

- Practices need to be underpinned by values, otherwise they become rote.
- Practices are also situation dependent.

## Primary Practices

### Sit together

- sit with client
- allow to communicate fully
- physical proximity enhances communication
- open spaces helps with ease of communication

### Whole team
- The team needs the skills and perspectives necessary for the project to succeed
- cross functional
- People need a sense of team
  - belonging, shared purpose, support
- The team is dynamic, should change members depending on needs

### Informative workspace
- Make workspace about your work

### Energized Work
- Only work for as long as you can be productive
-  prepared, rested, relaxed mind.

### Pair Programming

- PingPong
- Roles
  - Navigator and driver
  - Experienced or junior dev
  - Experienced or junior domain wise
  - These can be any combination. Need to adjust depending on what you are.
- It's a dialog between two people simultaneously programming (and analyzing and designing and testing) and trying to program better.
  - Keep each other on task.
  - Brainstorm refinements to the system.
  - Clarify ideas.
  - Take initiative when their partner is stuck, thus lowering frustration.
  - Hold each other accountable to the team's practices.
- Rotate pairs can be a good idea,
- tiring but satisfying.
- Pairing and personal space
  - Different individuals and cultures are comfortable with different amounts of body space.
  - Personal hygiene and health are important issues when pairing.
  - Ideally, emotions at work will be about work.
  - It is important to respect individual differences when pairing.
  - If you aren't comfortable, the team isn't doing as well as it could.

### Stories
- Write stories around the framework of customer-visible functionality
- As soon as a story is written, try to estimate the development effort necessary to implement it.

### Weekly Cycle
- Plan work a week at a time
- Have a meeting at the beginning of the week where you review progress to date and have your client prioritise a week's worth of stories

### Slack
- Always leave room for tasks to be dropped if you get behind
- You can also structure slack, e.g. hack days

### Ten-Minute Builds

### Continuous Integration
- Integrate and test changes after no more than a couple of hours

### TDD
- It addresses many problems.
  - Scope creep: if you really want to put that other code in, write another test after you've made this one work.
  - Coupling and cohesion: if it's hard to write a test, it's a signal that you have a design problem, not a testing problem. Loosely coupled, highly cohesive code is easy to test.
  - Trust: writing clean code that works and demonstrating your intentions with automated tests, you give your teammates a reason to trust you.
  - Rhythm: it's clearer what to do next: either write another test or make the broken test work. Code, refactor, test, code, refactor.

### Incremental Design
- Make the design of the system an excellent fit for the needs of the system that day
- design done close to when it is used is more efficient.

## Corollory Practices
- Primary practices should be done first before attempting this.

### Real customer involvement
- Make people whose lives/businesses are affected by your system be part of the team
- Aim to reduce wasted effort
- Increase trust with customer -> increased productivity

### Incremental deployment
- Big deployments have a high risk and high human and economic costs.
- Find a little piece of functionality or a limited data set you can handle right away. Deploy it.
- Legacy: Implementing scaffolding between the two systems is the price you pay for insurance against big changes going wrong

### Team Continuity
- Keep effective teams together
- Ignoring the value of relationships and trust just to simplify the scheduling problem is false economy

### Shrinking teams
- As a team grows in capability, keep its workload constant, but gradually reduce the number of team members
  - Strive to improve efficiency until some of the team members are idle — shrink the team and continue
- This frees people to form more teams.
- When the team has too few members, merge it with another too-small team.

### Root-cause analysis
- When a defect is found or a mistake occurs, eliminate its cause such that the team will never make the same mistake again
- Write an automated system-level test and unit test that demonstrates the defect, including the desired behaviour
- Fix the system so the unit test works. This should cause the system test to pass also. If not, return to the previous point.
- Once the defect is resolved, figure out why the defect was created and wasn't caught. Initiate the necessary changes to prevent this kind of defect in the future.
- Use the technique of the 'Five Whys'
- The root cause is almost always a people problem

### Shared Code
- Anyone on the team can improve any part of the system at any time
- Until the team has developed a sense of collective responsibility, no one is responsible and quality will deteriorate.
- People will make changes without regard for the team-wide consequences.
- pair programming and continuous integration are interesting to try to avoid selfish conducts.

### Code and tests
- Maintain only the code and the tests as permanent artifacts.
- Generate other documents from the code and tests
- Rely on social mechanisms to keep alive important history of the project.
- The valuable decisions in software development are:
  - What are we going to do?
  - What aren't we going to do?
  - How are we going to do what we do?

### Single Code Base
- Temporary branches should be short lived
- Multiple code streams are a huge source of waste
- Rather than add more code bases, fix the underlying design problem that is preventing you from running from a single code base.

### Daily Deployment
- Put new software into production every night
- If you are out of sync with what is in production you risk making decisions without accurate feedback. It is a risk
- Prereqs for this:
  - Defect rate is down to a handful per year
  - Build environment is smoothly automated
  - Deployment tools are automated
  - Ability to roll out incrementally and roll back in case of failure
  - Highly developed trust within the team and with customers

### Negotiated Scope Contract
- Write contracts that fix time, costs, and quality, but call of an ongoing negotiation of precise scope of the system
- Sign a series of short contracts instead of one long one
- Negotiated scope contracts are a mechanism for aligning the interests of suppliers and customers to encourage communication and feedback

### Pay-per-use
- Money is the ultimate feedback.
- Connecting money flow directly to software development provides accurate, timely information with which to drive improvement.
- If you can't implement pay-per-use, you might be able to go to a subscription model. Then the team can focus on retention rates
- Pay-per-release isn't a good option: the supplier is motivated to keep shipping releases with new functionality, whilst the customer wants fewer releases with more functionality, in order to avoid the pain of upgrades


## The whole XP team

- The roles and responsibilities of different team members
  - Members can have multiple roles
- The goal is to have everyone contribute the best he has to offer to the team's success
- Everyone on the team can recommend changes, but they should be prepared to back up their concerns with action.
- Roles:
  - Testers
    - catching trivial mistakes is accepted by the programmers
    - Test-first programming results in a suite of tests that help keep the project stable.
    - help defining and specifying what will constitute acceptable functioning of the system before the functionality has been implemented.
    - coach programmers on testing techniques
    - Testers amplify communication by looking at 'happy paths' and asking about scenarios where things go wrong
  - Interaction designers
    -  choose overall metaphors for the system, write stories, and evaluate usage of the deployed system to find opportunities for new stories.
  - Architects
    -  look for and execute large-scale refactorings, write system-level tests that stress the architecture, and implement stories.
    -  help choose the most appropriate fracture lines and then follow the system as a whole
    -  keep the big picture in mind as the groups focus on their smaller section.
  - Project managers
    - facilitate communication inside the team and coordinate communication with customers, suppliers, and the rest of the organization.
    - keeping plans synchronized with reality.
    - facilitate communication within the team, increasing cohesiveness and confidence.
  - Product managers
    - help the team decide priorities by analyzing the differences between actual and assumed requirements
    - adapt the story and theme to what is really happening now.
    - Stories should be sequenced for business, not technical, reasons.
    - goal is a working system from the first week.
    - encourage communication between customers and programmers, making sure the most important customer concerns are heard and acted on by the team.
  - Executives
    - provide an XP team with courage, confidence, and accountability.
    - articulate and maintain large-scale goals.
    - look for good software coming from the team and continuing improvement as well
    - free to ask for explanations about any aspect that dont makes sense.
    - Two metrics to measure the health of XP teams
      - Number of defects found after development. Each is an opportunity for the team to learn and improve.
      - The time lag between the beginning of investment in an idea and when the idea first generates revenue
  - Technical writers
    - provide early feedback about features and to create closer relationships with users
    - create closer relationships with users.
    - help them learn about the product, listening to their feedback, and addressing confusion with further publications or new stories.
  - Users
    - help write and pick stories and make domain decisions during development.
    -  have a good relationships with a large potential user community
    - have knowledge and experience with systems similar to the one being built
  - Programmers
    -  estimate stories and tasks, break stories into tasks, write tests, write code to implement features, automate tedious development process, and gradually improve the design of the system.
    -  Have good social and relationship skills
  - Human resources
    - reviews
    - Hirings
    - XP teams put much more emphasis on teamwork and social skills.
    - best interviewing technique is to have the candidate work with the team for a day
    - Pair programming provides an excellent test of technical and social skills.

## The theory of Constraints

- The Theory of Constraints says that in any system there is one constraint at a time
- To improve throughput in a system you need to first identify the constraint
  - then think about how you can increase its capacity,
  -  offload some of the work to non-constraints,
  -  or eliminate the constraint altogether.
-  How do I identify a constraint? Work piles up in front of one
-  when you eliminate one constraint you create another
  -  avoid micro-optimization and look at the whole situation before starting to make changes.
-  Software development is a human process not a factory.

## Planning: managing scope

- starts with putting the current goals, assumptions, and facts on the table
  - With current, explicit information, you can work toward agreement about what's in scope, what's out of scope, and what to do next.
- Planning is complicated because the estimates of the cost and value of stories are uncertain.
- There is a limit to how much work can be done in a day
  - More time at the desk does not equal increased productivity for creative work.
- Planning also involves deciding what to do next out of all of the possibilities. Plans are not predictions of the future. Rather, they provide you with a starting point and help you to coordinate with other teams.
- Everyone on the team should be involved in planning.
- Be prepared for the plan not to match reality.

## Testing: early, often, and automated
- Defects destroy the trust required for effective software development.
  - Without trust, people spend much of their time defending themselves against the possibility that someone else may have made a mistake.
- Defects are expensive when they occur
  - The direct costs of fixing the defects.
  - The indirect costs because of damaged relationships, lost business, and lost development time
- Acceptable level is to reduce the occurrence of defects to an economically sustainable level.
  -  eliminating software defects is also expensive.
  -  There will always be defects. The key is to learn from them so there are no repeats.
  -  The sooner you find a defect, the cheaper it is to fix it.
- Software testing is double-checking
- Beta testing is a symptom of weak testing practices and poor communication with customers.
- Tests provide a measure of confidence and a measure of progress.

## Designing: the value of time
- If you can generate value without feedback, designing sooner makes more sense
- If experience creates most of the value, designing just enough today to get going and then designing mostly in the light of experience makes more sense.
- Design is deferred until it can be made in the light of experience and the decisions can be used immediately
  - Deploy software sooner.
  - Make decisions with certainty.
  - Avoid living with bad decisions.
  - Maintain the pace of development as the original design assumptions are superseded.
- Design always
- Once and Only Once: DRY
- Simplicity
  - Is it appropriate for the intended audience? The people who need to work with it have to understand it.
  - Is it communicative? Every idea that needs to be communicated should be represented in the system.
  - Is it factored? Duplication of logic and structure make code hard to understand and change.
  - Is it minimal? The system should have the fewest elements possible.


## User stories

## Iteration planning

## Spiking


## Coding standards

## Collective ownerships

- All commits have both pairs name on it
- Any issue with this code, either one of the pair is responsibile for any issues

## Bugs

- New tests are writing for this
  - to expose the bug (red)
  - make sure bug is fixed (green)

## Practises

https://basusourav.wordpress.com/2015/05/18/12-core-practices-of-xp/

## links

- https://en.wikipedia.org/wiki/Extreme_programming
- http://www.extremeprogramming.org/
- https://martinfowler.com/bliki/ExtremeProgramming.html
- https://ronjeffries.com/xprog/what-is-extreme-programming/
- http://www.extremeprogramming.org/rules.html
- https://www.tutorialspoint.com/extreme_programming/extreme_programming_introduction.htm
