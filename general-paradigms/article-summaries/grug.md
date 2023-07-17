# Summary of The Grug Brained Developer A layman's guide to thinking like the self-aware smol brained

## Main enemy = complexity 

- Complexity is bad
- Should avoid
- Complexity may not been seen as bad by people who have not experienced it or ignore it
- Complexity can creep up slowly in codebase
- Need to be aware and remove complexity asap

## Say no

- Say no helps in fight with complexity 
- Preventative measure against complexity 
- Will disappoint people
- If asked to build feature or add abstraction, find reason to say no
  - is it needed?
  - Can we do it later?
    - postpone

## Say OK

- When cannot say no, need to compromise
- Can we reduce scope? 
- Do we need to do all of it?
- Can we comproimse?
- Build the bare minimum (80/20 rule)
  - may not be perfect, or does everything, but statisfies needs

## Factoring code (design)

- Dont do too much desing too early
- Dont abstract too early 
- Early in project, it is very fluid, things change fast 
  - wait till more stable before settling on design or abstration
- good cut point has narrow interface with rest of system: small number of functions or abstractions that hide complexity internally
- Avoid getting the abstraction wrong, as requires rework to undo and create new abstraction 
- Some people are too clever, create too many abstraction and leave project and hard to understand or work with
- Use simple UML diagrams
- Have working demo/prototype early, to prevent to much design/refactoring work
- force big brain make something to actually work to talk about and code to look at that do thing, will help big brain see reality on ground more quickly

## Testing 

- Save us time
- Better to write tests after prototype phase
  - especially when domain is not known
- Relying solely on unit (independent class) testing is bad
  - but break as implementation change (much compared api!) and make refactor hard and, frankly, many bugs anyway often due interactions other code. often throw away when code change.
  - write unit test mostly at start of project, help get things going but not get too attached or expect value long time
- End to End tests
  - show whole system work, but! hard to understand when break and drive grug crazy very often
  - End up ignoring
  - Can be very slow
  - small, well curated end-to-end test suite is created to be kept working religiously
  - focus of important end-to-end test on most common UI features and few most important edge cases
- in-between (social) tests or integration tests are better
  - high level enough test correctness of system, low level enough, with good debugger, easy to see what break
  - focus much ferocious integration test effort as cut point emerge and system stabilize! cut point api hopefully stable compared implementation and integration test remain valuable many long time, and easy debug
- Mocking 
  - Not good 
  - only use rarely
  - only when absolute necessary to (rare/never) and coarse grain mocking (cut points/systems) only at that
- when bug found. grug always try first reproduce bug with regression test then fix bug

## Agile 

- not worst way to organize development, maybe better than others grug supposes is fine
- Agile evengalists causes problems
  - See agile as silver bullet 
  - Enforce to many structures (ie meetings)
- prototyping, tools and hiring good coders better key to success software

## Refactoring

- good idea, especially later in project when code firmed up
- But can go wrong, cause more harm than good
- The larger the refactor the higher the chance of problems
- Stick to small refactors
  - ensure everything is still working after (build passes)
- introducing too much abstraction often lead to refactor failure and system failure

## Chesterton's Fence

- not start tearing code out willy nilly, no matter how ugly look
- world is ugly and gronky many times and so also must code be
- Just cause it is ugly does not mean it should be fixed
  - lead many hours pain grug and no better or system worse even
- Before changing code, take time understand system first especially bigger system is and is respect code working today even if not perfect

## Microservice 

- Why split calls between modules and add a network call
- Think hard before splitting a monolith up into microservices

## Tools 

- Have good tools
- Learn to use them well 
- Help with code completion
- Good debugger essential

## Type systems 

- Make coding easier
- Allows for autocompletion and see api is main help
- type correctness also help
- Using generics can lead to  problems
  - limit to container classes
  - Dont use it too early

## Expression Complexity

- minimize lines of code (Esp predicates) sounds good in terms of less lines of code
  - but bad for understanding and debugging

## DRY

- good advice 
- Must have balance
  - Dont dry everything 
- Too DRY code, makes harder to work with
- so long as repeat code simple enough and obvious enough, and grug begin feel repeat/copy paste code with small variation is better than many callback/closures passed arguments or elaborate object model
- Repeated code sometimes often better than complex DRY solution

## Separation of Concerns (SoC)

- idea to separate different aspects of system into distinct sections code
- Can lead to dissapation of logic
  - Have to search and connect the pieces
- Maybe  locality of behavior (LoB) is better
  - Having a procedural script easy to read rather than lots of objects doing parts of the work

## Closures

- usually abstracting operation over collection of objects
- small amount go long way
- Doing too much can lead to complexity

## Logging 

- Always have it and lots of it
  - especially in cloud deployed apps
- log all major logical branches within code (if/for)
- if "request" span multiple machine in cloud infrastructure, include request/tracey ID in all so logs can be grouped
- if possible make log level dynamically controlled
  - can turn on debug mode for more logs 
- if possible make log level per user, so can debug specific user issue

## Concurrency

- complex and feared
- rely on simple concurrency models like stateless web request handlers and simple remote job worker queues where jobs no interdepend and simple api
- optimistic concurrency seem work well for web stuff
- Use thread local variable
  - esp for frameworks
- Use internal concurrent libraries 

## Optimizing

- premature optimization is the root of all evil
- always to have concrete, real world perf profile showing specific perf issue before begin optimizing.
- never know what actual issue might be
- beware only cpu focus
  - may not be the main area of slowness
- hitting network equivalent of many, many millions cpu cycle and always to be minimized if possible

## API

- good apis not make user think much
- hide complexity 
- easy to use
- Bad api have
  - API creators think in terms of implementation or domain of API, rather than in terms of use of API
  - API creators think too abstract and big brained
- Create simple api, to do what you need now, add more features later when needed
- Bad api is needing to use streams to use filter

## Parsing 

- parser generator tool generate code of awful snakes nest: impossible understand, bottom up, what? hide recursive nature of grammar
- production parser almost always recursive descent
- https://craftinginterpreters.com/contents.html

## Visitor patter is bad

## Front End Development

- Lots of complexity 
- back end developers try keep things simple and can work ok, but front end developers make very complex very quickly and introduce lots of code, demon complex spirit
- Add complexity cause others are doing it, but they have valid reason while most just following blindly
- keep complexity low, simple HTML, avoid lots javascript

## Fads

- lots of fads in development, especially front end development today
  - lots of bad ideas
- back end better more boring because all bad ideas have tried at this point maybe 
- taking all revolutionary new approach with grain salt
- much of time wasted on recycled bad ideas

## Fear Of Looking Dumb

- very good if senior dev willing to say publicly: "hmmm, this too complex for me"!
  - very important senior dev say "this too complicated and confuse to me"
  - make it ok for junior dev to admit too complex and not understand as well
- Others might think you dumb or make snide remarks
- Do it even if you understand, but slight confusion

## Impostor Syndrome

- Big thing in coding 
- Mostly live in the dont know what is going on 
- Be comfortable in this state

https://grugbrain.dev/