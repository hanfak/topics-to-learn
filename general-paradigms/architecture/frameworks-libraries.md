# Framework and Libraries

- You should prefer core-language solutions to small abstractions to small helper internal libraries to general libraries to frameworks
- When you use a library, you are in charge of the flow of the application. You are choosing when and where to call the library.
- When you use a framework, the framework is in charge of the flow. It provides some places for you to plug in your code, but it calls the code you plugged in as needed. You write code for the framework to be able to use it, you are beholden to the framework, to get it's benefits

## NOTE: With any library,
- be sure to understand it's pros and cons (esp around secruity and legal), does it meet cost benefit for usage
- Does it fit in with your organisation, team, codebase, when used in production?
- Is it well maintained, number of contributors, passing tests, good test coverage, usages in production code
- Good documentation, good example tests, easy to follow source code
  - Should be able to follow code in library, esp during dubugging.
  - Need to rely on documentation, and if poor, then rely on stack overflow
- test it
- write poc (proof of concept), investigate using it
  - best to do this with similar libraries to make a choice between
- try it out but be able to make it easy to remove if not working out
  - The only way it can be found as useful is in production
- avoid having to build lots of hacks or engineer solutions to bugs or needed features which are not suited to library
- Avoid having to have comments or readme/faqs to help user deal with problem
- using a library, means adding new stuff to learn, new api etc.
  - This can lead to misuse, need to place checks and balances
    - automated tests to write to avoid issues
    - plugins for IDEs
    - extra time on code reviews/pairing needing to look out for these issues instead of focusing on business features or important techenical issues
    - more time debugging, having to go through library, or decomplied classes etc
  - This can be avoiding, practicing good design ie least astonishment, ease of use, fluent api, etc
- Coupling problems, when a new version is out, then consumers will need to upgrade
  - but if there are breaking chagnes in the new version, this can lead to some consumers using different versions (esp with open source libraries)
  - Eventually they will need to move to new version
    - security updates, deprecation of functions
    - which means more work which is not of business value

### Choosing

We often have two choices when implementing some logic. Either:
- Build it ourselves
  - This involves a cost of time, maintaining
  - But in charge of fixing, being custom built
- Get it from someone else
  - Which can entail:
    - Some one else builds it for you, thus it becomes custom to your needs, and likely improved upon or bug fixed quickly
    - Use something that is already out there, ie a library (private or open source), but beholden to the creator(s) to decide when to fix bugs or improve.
      - This is built with general user in mind, so may not fully meet your needs

When choosing a library or service to use, despite being free or paid, we must take it upon ourselves as engineers and for the well being of the business to evaluate it properly.

Areas to consider:
- If the code is small, poorly implemented, not well tested, no maintained, few users (forks/clones/downloads) then should not use
- If code has had issues in terms bugs, poor defaults, doing more than it should
- If it brings in the world
- If the license will cause problems
- If compatibility with future upgrades may cause problems
- Design choices - easy to use

There are ways of mitigating these issues, is too put libraries on edge of your applications, using dependency inversion, adapters, so that the may logic of the app is not tied to the library. The user of a library, should not be beholden to a library (or be very careful in what libraries you choose to couple/tie yourself to).

https://jaxenter.com/choose-right-java-library-159386.html


## Differences

- https://www.programcreek.com/2011/09/what-is-the-difference-between-a-java-library-and-a-framework/
- https://medium.com/datafire-io/libraries-vs-frameworks-626cdde799a7
- http://danielemargutti.com/2017/12/13/applications-vs-frameworks-vs-libraries/
- https://www.tonymarston.net/php-mysql/what-is-a-framework.html

## Principles

- https://kukuruku.co/post/do-not-learn-frameworks-learn-the-architecture/

## frameworkless

- https://frameworkless.js.org/
- https://dev.to/misomir/frameworkless-web-development-3n2h
- https://github.com/frameworkless-movement/awesome-frameworkless

## Libraries

- https://www.oracle.com/corporate/features/library-in-java-best-practices.html
- https://www.baeldung.com/design-a-user-friendly-java-library

## framework coupling

- https://dzone.com/articles/framework-coupling-revisited

## Frameworks advantages

## frameworks disadvantages

- Frameworks can be seen as one of the hugest anti-patterns in software development.
- They're hard to learn and this knowledge is generally useless
  - Where as learning fundamental tools, core computer science concepts, and programming techniques which are useful and timeless
  - The core stuff learned will help in being able to use frameworks and how it works
  - frameworks though can be a lot of magic
- people use frameworks or latest shiny thing due to peer pressure, without thinking about the consequences, cost/benefit, is this the solution for the situatoin at hand
- They limit your creativity
  - Frameworks make you dumb. Whenever you're faced with a problem you can't just invent a solution; you're limited by what the framework lets you do
  - You have to seek experts, waste your time and energy to find a solution to a problem you shouldn't have had in the first place if you hadn't used a framework
    - Spending time engineering a solution to get around a frameworks issue instead of business requirements
  - You can't let framework authors control what you can or can't do. You should be in total control over your product.
    - you can use clean architecture to invert dependencies on framework/libraries
- They increase your project's complexity and dependencies
  - Complexity and dependencies are bad. You should keep both your project's complexity and dependencies at minimum
  - If not controlled will lead to dependency hell
  - There should be strict rules what you can and can't use in your project, and someone has to make that call.
  - Without rules you might save time at the beginning and sound cool using all the latest frameworks, but now your software is so complex that no one understands how or why it works
    - It's also become unmaintainable. You may not notice it in the first few months as things are moving along quickly, but as your project progresses, your team's productivity will drop because of all the complexity and dependencies. You'll need more people to maintain it, and more people with specific knowledge to maintain it. If your lead developers leave, you're dead.
  - Every added framework, and even library, makes your project more difficult to maintain. Avoid unnecessary frameworks and libraries from day one.
- They go out of business and get abandoned.
  - you need to trust the authors of this framework
  - You have to learn the new frameworks again. It takes a lot of effort, energy and resources. You just spent all that time earlier learning the old framework and now it's out of business. All the skills you accumulated are now useless.
  - All tooling that was created are useless
- You have to maintain and upgrade your code to match the latest framework versions for no good reason.
  - If you wait too long between updates, frameworks have changed dramatically, and you have to spend days adjusting your code and learning the new interfaces. You don't need all the extra functionality the framework developers added. Most likely you don't need anything at all from the new version.
  - Framework developers can't stop evolving their projects for no good reason. Often software is just done. It does what it's supposed to do and doesn't need any changes ever again. You don't need the latest version of every software. Some of the best software was written 10 or 20 years ago. Use it!
  - Upgrading versions for no reason is another huge anti-pattern. If software works at version X, then it should stay at version X and should never be touched unless absolutely necessary.
  - Upgrading is hell
- You have to search for help and ask others for advice when you're stuck.
  - When something goes wrong with the framework or you get stuck, you can't just come up with a solution because you're limited by what the framework lets you do. You have to ask for expert help, wait until someone helps you or pay an expert framework consultant.
  - If you keep your dependencies to bare minimum, then you're the expert and you can quickly get things done and come up with the solutions without ever asking for anyone's help or advice.
- And you probably only need a small percentage of features that the framework offers anyway.
  - "Which frameworks shall we use?" is the wrong question to start you new project with. Start your project with an empty file and use programming and a few helper libraries and core tools to get it going.
-

- http://tomasp.net/blog/2015/library-frameworks/
- https://medium.com/@john_doherty/why-i-dont-like-javascript-frameworks-7714d1fd34b7
- https://medium.com/@kevincennis/you-re-thinking-about-frameworks-the-wrong-way-83544a337a27
- http://www.catonmat.net/blog/frameworks-dont-make-sense/
- http://samatkinson.com/why-i-hate-spring/
- http://tomasp.net/blog/2015/library-frameworks/
- https://timperrett.com/2016/11/12/frameworks-are-fundimentally-broken/

## Framework v library

- https://dzone.com/articles/programming-without-a-framework
- https://dzone.com/articles/discussion-recap-to-framework-or-not-to-framework

> The whole article really doesn't apply to any mainstream programming languages like ruby, python, java, javascript etc.
Why? I use JavaScript solely, and I agree with the author 100%. The frameworks solve a lot of problems, but by bundling those solutions together they introduce a new problem.

> How do you organise the interaction of libraries?

This is what coding is. Asking this question over and over. You can't escape it. You can make a promise to yourself: "I'll just do it the Rails way" but that doesn't get you off the hook. Now you need to learn what the Rails way is. And that itself is never done. You will need to ask over and over "What is the Rails way?"

> You can do it yourself but you will have to follow some sort of pattern to organise the code in order to make it easy to work with.

Again, that's is what coding is. Patterns. Which pattern do we need now? How about now? How about now? The Rails pattern only takes you so far. And for many problems it will steer you wrong. You can't avoid learning patterns and when to use them, it's part of your job.

> What happens when another coder joins your project?

Part of why this is scary, is because if you use a framework that coder REALLY needs to understand the framework. The framework itself is a big domain of code that you generally don't want to have to debug, and you don't want to have to wonder how it works. You kind of need to know how it works before you start.

But idiomatic code is different. If I write a system in pure, idiomatic Java, with no framework, a new programmer doesn't have to understand any kind of underlying system. They don't need to understand a framework, because there is no framework. All of the code is right there in the repo. They can just go read it. They can place a debugger and walk step by step through the whole interaction, without ever leading their codebase.

> Are you going to tell them the pattern you have already been using?

Yes, usually if they're new we pair program until they get a sense of the layout. But again, they don't need to learn the pattern in the same way that you need to learn the Rails routing pattern, or the Rails ActiveRecord pattern. You don't need to learn the pattern of a bespoke codebase, because you can just go read the code. There's not some separate system which is doing it's own thing in parallel to your application, there's just your application.

> What if they dont follow it as expected or disagree with it?

Great! That's their job too. They should disagree with the architecture, find better ways of doing things, and talk about that with their coworkers.

> Frameworks standardise this. Yes you might not always like certain aspects of the framework you're using but its the price you pay for not having a project full of developers who each have their own way of doing things and are constantly argueing over how to organise the codebase.

Sometimes that standardization is a worthwhile tradeoff for sure. If you need to get up and running quickly, and you want to start with a big team who already has some alignment, you definitely need some standards.

You also probably want a framework if you're building lots of apps that will mostly not be maintained. So, like special event apps for NFL playoffs, or marketing campaigns or something.

But if you're starting with a couple of developers and growing organically, and if you're trying to build a product that you will be actively adapting to your business needs for many years, a framework might get in your way in the long run.
