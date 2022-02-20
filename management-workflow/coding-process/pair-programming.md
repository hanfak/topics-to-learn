# Pair Programming

## What

- A coding technique, two programmers work together at one workstation.
  - One, the driver, writes code
  - while the other, the observer or navigator, reviews each line of code as it is typed in.
    - While reviewing, the observer also considers the "strategic" direction of the work, coming up with ideas for improvements and likely future problems to address.
      - This is intended to free the driver to focus all of their attention on the "tactical" aspects of completing the current task, using the observer as a safety net and guide.
  - The two programmers switch roles frequently
- Comes from agile, and Extreme programming

## Roles

- where are we goign
- what comes next
- is this all coming together
- any errors or mistakes
- suggest ideas

### Driver

- More in the code
  -  whats the syntax
  - should i rename
  - whats the next test

## Benefits

- Code review in real time
  - less disturbing of coworkers for help/review/design discussions
  - more detailed code review when check bit by bit, rather than all the changes
- improved team resilience
- people are less distracted
  - prevent slacking as someone is watching you
- work gets done almost as fast as single person programmer
  - but with higher quality, less bugs
- Can commit more frequently (small changes) without having to get code reviews done all the time
  - Better of CI
- higher quality
  - reduce errors
  - find errors faster
  - simpler solutions
- coding style becomes more standard across the team
- people may find better solutions to problems together
  - evaluate more options than working solo
- knowledge sharing
  - faster onboarding and training of new or junior members
  - No single point of failure
  - No hand offs
  - No silos
  - Introduce new members to codebase faster
  - Coding is an exercise in learning, and this helps facilitates learning
    - learning from people
- Carry out interviews
  - good way of evaluating a candidate on some task
- Involved and brings out the best in
  - refactoring
  - coding Standards
  - testing
  - collective ownership
  - CI
- State of devops report (accelerate book)
  - More effective teams use pairing
- On first day, they work on production code

## Drawbacks

- costs
- Exhausting
  - Driver needs to talk while coding
  - Constant switching (either roles or pairs) is tiring
- Not great for people who are not great at communicating with others
- Not as popular, thus less people with experience
- if 1 pair only worked on the story, then only two people had eyes on the code base
  - might still need a review from outside pair
- Can be hard to get the right chemistry with the team, need to find members who are willing to work with others without turning them off
  - Can lead to poor team dynamics
  - lead to high turnover
- Seniors working with juniors can lead to slow work especially at the beginning and when the junior is the driver
  - Can lead to the senior being driver more often, and the junior not getting as much benefit from pairing
- Being too stringent on pairing, can lead to one person only working when the other pair is present
- You cannot sit back and evaluate your own code
- Can end up having the navigator not being actively engaged, more so during remote pairing
- Can reduce creativity, as a solo you can play around with it, but in a pair you will need to discuss it and convince pair
- fear of judgement, can lead to taking less risks, exploring, etc
- Pairing between two seniors, or two opinionated coders, can lead to arguments, that leave one or both bitter, and reduce morale
  - also lead to discussions with no consensus
  - can lead to one dev, giving up and letting the other continue their own way
- Not treating devs as professionals, or can handle responsibility
- some people cannot work with others
  - personality
  - hygiene
- Can be overbearing, especially when you need to pause and justify it
  - going to toilet, grabbing drink etc
- Noise is generally increased, especially in open planned offices
  - lead to hard to concentrate (for solo or pair)
- Not great for boring or repetitive stuff

## Styles of pairing

- https://stackify.com/pair-programming-styles/

## Etiquette

- https://blog.rapid7.com/2017/01/27/5-rules-of-pair-programming-etiquette/

## Pros and cons

- https://hackernoon.com/the-ultimate-guide-to-pair-programming-b606625bc784

## Implementation

### Full time pairing

- Everything is done with a pair
- Can split work out, especially boring and repetitive stuff, to share workload (parallelism)

### Part time pairing

- used when need to work with some one for the following:
  - stuck on a problem
  - evaluate design or get more ideas
  - code review
  - on boarding
- Otherwise, the dev will working their own

### Mob programming

- Multiple members join together over one screen to solve a problem

### Ping pong

- one writes the test, the other passes it, and constant switching

### one workstation

- Two devs work using one box/computer, which is attached to two monitors, two mice, two keyboards.
- Easy to switch between driver and navigator

### separate workstations

- Each dev codes on their own laptop, but can see each other laptops with shared monitors
- switching pairs is harder, as need to commit or patch work
  - if commiting, might need to do it on branch to avoid breaking CI, or finish a piece of work so it can go on master
    - this can lead to longer time fixed in the driver and navigator roles

### Switching pairs (Pair rotation)

#### Per x days

- Switch pairs when a set number of days have passed
- Can be done every hour, every day or every 2 days etc

#### Story champion

- Sticks on same story through out whole lifecycle, and others come and join

## Remote pairing

- Generally, pairing is done in person, sitting next to each other
- Remote pairing, is done with some software, that allows the two users to share their screen.
  - Being able to work on the other screen is a feature which helps alot and make it feel like in person shared workstation pairing
- Issues
  - Internet issues (lag)
  - cannot see full communication of pair, even having video on does not help


## Links

- https://martinfowler.com/articles/on-pair-programming.html#HowToPair
- https://www.thoughtworks.com/insights/blog/seven-principles-pair-programming-etiquette?utm_source=linkedin&utm_medium=social&utm_campaign=tech
- https://www.codurance.com/publications/2015/03/15/rethinking-pair-programming
- Farley https://youtu.be/t92iupKHo8M
