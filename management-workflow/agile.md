# Agile

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Agile](#agile)
	- [Overview](#overview)
		- [The agile values](#the-agile-values)
		- [The principles behind agile values:](#the-principles-behind-agile-values)
		- [Links](#links)
	- [Process](#process)
		- [What is agile](#what-is-agile)
	- [Issues](#issues)
	- [Types](#types)
		- [Links](#links)
	- [Team](#team)
	- [Backlog](#backlog)
	- [Iterative development](#iterative-development)
	- [Stand ups](#stand-ups)
	- [Retrospectives](#retrospectives)
	- [Done](#done)
	- [Cardwall](#cardwall)
		- [Links](#links)
	- [User Stories](#user-stories)
	- [Autamated Tests](#autamated-tests)
	- [Showcases](#showcases)
	- [Pace](#pace)
	- [Myths](#myths)
	- [Sprints](#sprints)

<!-- /TOC -->

## Overview

- Waterfall but in shorter time frame (or set of features) repeated
	- a few features produced then all features
	- To get early feedback

### The agile values

- Individuals and interactions over processes and tools
- Working software over comprehensive documentation
- Customer collaboration over contract negotiation
- Responding to change over following a plan

### The principles behind agile values:

- Our highest priority is to satisfy the customer through early and continuous delivery of valuable software.
- Welcome changing requirements, even late in development. Agile processes harness change for the customer’s competitive advantage.
- Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
- Business people and developers must work together daily throughout the project.
- Build projects around motivated individuals. Give them the environment and support they need, and trust them to get the job done.
- The most efficient and effective method of conveying information to and within a development team is face-to-face conversation.
- Working software is the primary measure of progress.
- Agile processes promote sustainable development. The sponsors, developers, and users should be able to maintain a constant pace indefinitely.
- Continuous attention to technical excellence and good design enhances agility.
- Simplicity–the art of maximizing the amount of work not done–is essential.
- The best architectures, requirements, and designs emerge from self-organizing teams.
- At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behavior accordingly.

An organisation is agile, when it responds to threat and opportunity in ways uniquely of the moment. It is informed by history and not shackled to practices encoded in software not likely to be revised soon

Organisations are adaptable.

Prevents fortune telling
- Guess the future of a coorperative task

The manifesto had two issues
- Thinking this applied in general rather than just for writing software
- Led to only being applied to new software projects, and only until they went live

Instead of figuring everything upfront, we design, build and test little bits of software at time.

### Links

- http://agilemanifesto.org/
- https://www.agilealliance.org/agile101/
- https://martinfowler.com/agile.html
- https://pivotal.io/agile

## Process

### What is agile

- Agile is a software development methodology that stems from the idea of breaking up large amounts of work into smaller pieces
	- This gives stakeholders, a better understanding of the work and how long it will take to complete, how much can be done etc
- Was a reaction to old way of doing software development (ie waterfall), where major changes to requirements could put large strains on teams.
	- Thus the smaller chunks of work help teams become more flexible, and dare I say agile. And in the process it helps them deliver features faster and respond to changes quicker.

## Issues

- Agile has led to code first rather than architect first
  - agile can focus on the short term and the user functionality, rather than consider the overall end goal or other requirements
  - led to not thinking about (trade offs) or including the non functional requirements (software requirements)
  - Trying to add, makes it harder, and thus rewrites occur
  - Or constraints (cost, legal/compliance, deadlines, staff capacity, staff exp/knowledge)
  - or principles (how we would like to build it ie styles, standards, tech) which can lead to long issues
- Get too tied down to the methodology
	- becomes box ticking
	- Do not deviate from the rules ie a sprint has 10 stories to do, if all done dont do anything else
- All about the process, rather than the engineering aspect
	- It is not used as a feedback mechanism
- Seen as silver bullet
- Dont want to take the good parts and combine, or experiment with different processes
- Focus on features, can lead to system having software qualities that emerge accidently
	- ie it has set level of latency  rather than aiming for a desired level of latency
	- this can be fine, as we use the feedback from the users which informs the process to create stories to fix this
	- But due to the accidental nature, they can be hard to fix, be cross cutting, may need rewrite or takes long time
- To integrate the software qualites, the definition of done includes this, but then there comes a point where different vairations of done are set so that software can be released (ie done but slow, done but no security etc)
	- this leads to qualities being ignored, and never revisited, or partially implemented 

## Types

- Scrum
- Kanban

### Links

- https://www.freecodecamp.org/news/what-is-agile-and-how-youcan-become-an-epic-storyteller/


## Team

## Backlog

## Iterative development

## Stand ups

## Retrospectives

## Done

## Cardwall

### Links

- https://agileboardhacks.com/

## User Stories

- A story is typically the smallest defined piece of work
	- defining a bite-sized piece of work,
-  in the form of a new ticket that you create
	- ie Jira, trello or Github Issues.
- Used during kickoff and signoffs
- Style
	- explain the work that needs to be done in the form of a story
		- ie if you would like to provide the ability for the people who use your website to share a blog post on Twitter, you may want to write the story as: As a reader, I want to share the post I just read to Twitter.
	- Using that pattern of "as a [person], I want to [action]"
	- Format
		- Title
		- details
		- stakholder, reporter, active worker on story, where in kanban board it is
		- include tools like tags or categorizations
	- Details and requirements
		- a thorough description and a set of acceptance criteria that can help give the developer context and requirements.
- Amount of work or level of difficulty
	- Each story is represented by a number of points.
	- Those points are a way to express how much effort a team of developers expects one story to be.
- Epics
	- a way to group those pieces of work (user stories) together to represent a feature.

## Autamated Tests

## Showcases

## Pace

## Myths

- https://completedeveloperpodcast.com/episode-153/

## Sprints

- a way of planning out how the work will actually get done.
- typically represent a period of time in which a particular chunk of work (an epic or set of stories) will be done.
- Time per sprint
	- A common way of defining a sprint is two weeks of work.
	- During those two weeks, your team will have a particular velocity, or average amount of work you can complete, for an individual sprint.
	- This velocity is represented by a number of points that is a sum of the average velocity of each of the developers working on that sprint.
- Points per sprint
	- points will roughly translates to an average amount of time of work for each developer
		- ie While 1 point for an experienced developer could be 1 hour, that same 1 point could mean 3 hours for a less experienced developer.
	-  once you have this number of points that your team averages in a sprint, you'll know how many story points you can expect to plan to be completed
	- This planning goes sprint to sprint as you spread out a group of stories or an epic so you can predict when a feature will be complete.
