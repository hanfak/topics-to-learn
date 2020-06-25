Universal Principle: The only code that must be changed is code that is wrong.

You can act two ways on this:

Option 1: Don't get the code wrong to start with.
Option 2: Make it so that changing the code is easier.

## Option 1

How do you not get the code wrong? So far as an industry we have tried:

Type systems
CASE and other high level diagramming tools
Business Analysts
Databases
New Languages
Static Analysis tools
Unit Testing
Use Cases/Stories/Epics/Conversations
Quality Assurance
Running three or more separately and differently coded versions of the same algorithm
BDD, DDD, TDD
Cross Functional Teams
To name a few...

Was it successful? No.

Was it a failure? No, we found and fixed a lot of issues.

So what really happened? We had to change a lot of code.

Sounds like option 2 would have been awfully useful! sheepish industry looks askance

## Option 2

How do you make code easy to change? ... by at least not making it harder to change.

There are three sorts of code:

No Code
Understood Code
Legacy Code

### No Code

Beautiful Verdant fields of blissful nothingness... Not really.

Before there is code, there already exist processes, people, resources, questions, curiosity, and all sorts of other stuff. Writing code is often proclaimed as the solution to the woes this stuff is already experiencing. All code does it make the woe happen faster. So before coding anything straighten up the mess.

Once the mess is straightened up, now comes the really hard part: resisting the urge to go and start writing something.

Why? Because any code you do write, necessarily makes it harder to change. So if you do write code, make sure it is code that absolutely must be written. Draft it, edit, re-edit, and so forth until the code reads well. Pass it to other developers for critical review.

### Understood code

There are some problems that are so well understood that we have documented hundreds of precise ways to solve them. The Pythagorean Theorem is one such problem. Sorting is another.

These problems are so well understood that codifying them follows a very preset proscribed pattern. In these situations following that pattern makes the code very easy to read, and very easy to change. Attempting to elaborate them further, or be terser in their expression only hurts legibility, which makes it harder to change them.

### Legacy Code

Legacy code is anything written be it in a text file, in a database, a picture, etc.. that if it were somehow missing that you could not write (or otherwise reproduce) completely in its entirety from memory with an accuracy of better than 99%.

Most software systems sit in the legacy area either because they are too large in terms of lines of code, too complicated in terms of the problems being solved, or too unknown in the sense that you the reader don't know how the system does actually do. By this definition a new or junior developer will even see known problems as legacy code.

Many people will tell you all sorts of ways to make the code easier to change. Not all of them will work on your code base, because at this size and scale no two code-bases are even remotely identical in what they are trying to solve or how they solve it. Otherwise we would either have a well known problem, or no code.

The problem is how do you define "easy to change"? Everyone will have a different opinion which is not useful. Also we are dealing with complex problems (otherwise they would already be solved and well understood) and simple problems are known to have multiple equally valid solutions (just look at sorting). So it just might be that there are several ways to write a program that is easy to change.

Kevlin Henney talks about this in a couple of lectures where he shows different approaches for writing software that generates the expected output for a game of FizzBuzz. It is interesting because each representation of the solution favours some sorts of change more easily than others.

This chases the idea that there is nothing more dangerous than having a single idea. With a single idea you cannot orientate yourself because it is a single point of reference.

The number of points needed to orientate yourself increases with the dimensionality of the space, 2D requires 2+, 3D requires 3+, etc... Its not just the number of points though, but the quality of the points. Each point needs to tell you something new that none of the other points contain, this new thing should be noticeably different, otherwise the point is useless for orientating (even though it might be a decent end solution).

Code has a very high dimensionality so you are going to need many points of reference to be somewhat sure that you have a good-enough orientation. Only then can you look at those points and make a decision as to what is better. You will know it is better because it outshines these other solutions.

## OO Development

Focus less on it being Object Orientated. It is all code, the techniques are universal, if not always easy to implement.

You have a language, it provides you with a wealth of tools. Learn them.

Each tool has a place when and where it is useful, as it equally has places when and where it is useless, or even out-right dangerous.

Every tool is an implementation of some known problem domain. As there are many ways to solve problems, there are usually several tools that are implementations of that domain. Before picking one up, look at each in turn and contrast their strengths and weaknesses, perhaps solve the same simple problem that exercises the features you need with each tool, then decide.

Train yourself in other languages and other paradigms of programming. This will sharpen your skill at orientating in code space largely because it improves the quality of the points in code space you have knowledge of.

Don't throw out those general rules of thumb. They are general precisely because they represent problems that manifest regardless of you programming paradigm. Of course if you have out-grown them, great you have already internalised the wisdom they contain.

Find already existing software that solves similar problems. Read their code and study the patterns used (a.k.a. the well known solutions).

Make use of the techniques we as industry have discovered to not get code wrong to start with. Obviously mileage will vary for each code base.
