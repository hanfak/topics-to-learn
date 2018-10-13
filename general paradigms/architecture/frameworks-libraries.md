## Differences

- https://www.programcreek.com/2011/09/what-is-the-difference-between-a-java-library-and-a-framework/
- https://medium.com/datafire-io/libraries-vs-frameworks-626cdde799a7
- http://danielemargutti.com/2017/12/13/applications-vs-frameworks-vs-libraries/

## Principles

- https://kukuruku.co/post/do-not-learn-frameworks-learn-the-architecture/

## Libraries

- https://www.oracle.com/corporate/features/library-in-java-best-practices.html
- https://www.baeldung.com/design-a-user-friendly-java-library

## framworks disadvantages

- http://tomasp.net/blog/2015/library-frameworks/
- https://medium.com/@john_doherty/why-i-dont-like-javascript-frameworks-7714d1fd34b7
- https://medium.com/@kevincennis/you-re-thinking-about-frameworks-the-wrong-way-83544a337a27
- http://www.catonmat.net/blog/frameworks-dont-make-sense/
- http://samatkinson.com/why-i-hate-spring/

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
