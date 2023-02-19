# 10x devs

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [10x devs](#10x-devs)
	- [Notes from Can Everyone Be a 10x Developer? • Steve Poole • Devoxx Poland 2022](#notes-from-can-everyone-be-a-10x-developer-steve-poole-devoxx-poland-2022)
	- [links](#links)

<!-- /TOC -->

Focusing on efficiency, effectiveness, and productivity
Enabling others to succeed and being a valuable team member
Continuously learning and growing in both technical and soft skills
Creating an environment that fosters the growth and development of all team members
Being a master craftsman, careful in their work and always looking for ways to improve.
Being a problem solver and thinking out of the box
Being humble and not just focusing on individual success but also team success.
Being a good communicator and understanding the importance of communication in the team and organization.
Being productive by connecting their work with everything else.
Being a continuous learner and a lifelong learner.
Focusing on understanding the problem and the goals of the project, rather than just writing code
Being adaptable and able to work with different technologies and tools
Being organized and able to manage time and tasks effectively
Being open to feedback and continuously seeking ways to improve
Being proactive and taking initiative to identify and solve problems
Being a good listener and understanding the needs of the team and the stakeholders
Being able to think strategically and understand the bigger picture
Being able to work well under pressure and handle multiple tasks and priorities
Being a mentor and helping others to improve
Being able to work in a collaborative and open environment.
Embracing new technologies and frameworks and being open to learning new skills
Automating repetitive tasks to save time and increase efficiency
Building a strong understanding of the business domain to make better decisions
Documenting their work and sharing their knowledge with others
Continuously testing and monitoring their code to ensure high quality
Being proactive in identifying and addressing potential issues before they become problems
Being a good leader, who can lead by example and guide the team
Being a good team player, who can work well with others and help to build a cohesive team
Being a good communicator, who can explain complex technical concepts to non-technical stakeholders
Being a good problem solver, who can think critically and creatively to find solutions
Being a good time manager, who can balance multiple tasks and meet deadlines.

## Notes from Can Everyone Be a 10x Developer? • Steve Poole • Devoxx Poland 2022

- https://www.youtube.com/watch?v=eDLFyS2AJyg
- A role model
-  someone who is efficient, effective, enables others to do the right thing, communicates well, and is a master craftsman
  - more humble and less visible than what we may imagine.
  - Get stuff done, at higher quality, fixes bugs, prevent bugs, more pr
  - Understand the tools that they use, use the for the correct purpose, use them well
- not necessarily people with "superpowers" and that the idea of a 10x developer is somewhat fluffy and not well defined.
  - or someone who can write 10 times more code or fix 10 times more bugs than others
  - this idea harms recruitment, for this is the bar for hiring devs
- who help the team achieve success and bring the whole team up.
  - enables others to do the right thing (teaching, implementing stuff to make it easier to do the right thing or prevent the wrong thing)
- have "second thoughts" and are able to look at things from a different perspective.
  - Will step back, will think about it differently, will remember a time this has occurred and had issues  
  - thinks about problems differently, not up all night
- Continually learning
  - learn from others ie books, speakers, blogs, conferences, meetups, other developers, codebase
  - learn from experience
  - learn about the environment, the apis, libraries, tools, processes, systems, the standards/conventions, the code base, the deployments, the monitoring, the people and what they bring/do,
  - Dont code straight away, understand what is going on, then formulate a plan
    - find the facts before starting
  - Use feedback and evidence, rather than guess work
    - write test or debug, instead of guess what happens
    - scientific approach
  - Figure things out and explore
    - create POCs, try it out with a project
    - learnign tests
    - find pros and cons, it's limitations
    - read documentation, find gotchas
    - break it, find out how it goes wrong, what it looks like, how to find info to fix it, how to fix it
  - In new environment, learn enough to get things done
    - How to deliver something
- understands context/problem, what is the need/constraints and applies knowledge
- Focuses on the task
  - not multitasking
  - Know why this is the next thing to do
  - Dont add unneccessary features for just in case scenario
  - prioritises what to do, necessary/nice to have
  - preventing time wasting on things that could be spent on productive work, if find this implement something to avoid it next time
    - using correct tool for correct job
    - Common task either automate it or put in wiki (Easy to find)
    - ie use live templates in ide, use shortcuts in ide, create script to start app
    - Common problems either fix, or put in readme/wiki
    - ie issues in production, add logs next time
  - removing barriers from coding
  - Dealing with issues
    - remove issues/stories that are nice to have or never goign to fix to another place
    - Bugs or problems, need to get evidence, ask for evidence (when, where, flow, logs, what expectations not met)
- Use git
  - Everything goes in there
  - ie Code, notes, deployments, config
  - history, can roll back
  - infrastructure as code
- Use CICD
  - for a lot of things
  - to get fast feedback
- prototype or mvp
  - Writing code and tests
  - keep tests, as this defines the behaviours, can refactor
- Define what they should do and what others should do
  - testing - what should be automated, what should be manual (QA), what should only run in CI
    - devs calling running tests on machine can block -> should be done in CI (aysnc)
    - devs should do easy to automate with short execution time and with little domain knowledge
    - QA should do hard to automate with short excution time but require more domain knowledge
    -  10X will make it easier for those QA and CI to setup, run and get feedback
- Dont be the only one to solve the issue
  - reduce bus factor
  - help others be able to solve it
  - Have documentation
- Manage upwards
  - you become trusted and respected
  - trust your estimates and worries
  - you provide evidence for your reasoning
  - tell them what needs to be worked on now and why
  - show them that what they ask for maybe unrealistic within constraints
- Acts as an engineer
  - wants to create value
    - value that comes from working software that only does what is necessary delivered on time
  - understands and works with the constraints
  -  knows late(time/functional) software reduces values, buggy
  - Value delivered only lasts certain period of time
    - needs to be maintained to maintain it's value
  - Understand the code that is written is not the main value, it is what it does, that value it gives
    - code is ephemeral, it changes, not stuck to it, the solutions are long term
  - Value is delivered as a team
- Thinks in terms of risk
  - How to reduce it
  - All changes are risky, how to get fast feedback
    - tests
    - if goes to production want to reduce the risk as much as possible, but always a risk (should be able prevent ie testing or cure ie toggles)
  - The aim, if after every code saved, run all tests would be brilliant
    - but impossible, so run tests are different stages, which increase feedback loop and cost
- Use dashboards to get feedback
  - build monitors, alerts etc
  - need metrics defined, what is good what is bad
  - Tells you when something broke, why and find out as quick as possible
  - Can automate now (if possible or worth it)
  - not just for the working code in prod
    - but for his own productivity, the teams, code standards, processes Used
- Tooling
  - There are lots of tooling
    - will learn the right tools then everything
  - master them
  - 10X will know a subset that will do the job
  - if in new environment, will use their knowledge of their tooling and learn new tooling
    - may suggest tooling that can help for new use case or replacement
- Have opinion backed by evidence
  - willing to change mind in face of evidence


## more

- 10x engineers do not exist as a person who is 10 times faster at writing software.
- The limiting factor in software development is not typing speed, but the ability to write code correctly on the first try.
- A 10x engineer can be defined as someone whose work is so exceptional that it empowers others or replaces the need for multiple other developers to do the same job.
- Examples of 10x engineers are those who have created solutions that have changed the workflow for everyone else, like those who created web frameworks like React or Angular.
- A 10x engineer may also have excellent technical skills, domain knowledge, and the ability to effectively communicate and align with stakeholders.
- 10x engineers can be seen as a valuable asset in a company as they are often highly sought after for their expertise and ability to unblock team members and make decisions quickly.
## links

- https://www.simplethread.com/the-10x-programmer-myth/
