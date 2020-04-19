@Geert

I am an enterprise backend software developer working for a multi national company for a few years now. Heres my take:

1 - You work in finance, the sector makes more money than coding, apart from being a contractor. I would not leave that field, unless you don’t like this work.

2 - If you stay in this field, then learn automation. I agree with Aaron, do not make this your main skill.

 For example, if you use excel a lot, then learn how to automate common and time hogging tasks ie common calculations, or loading data. This can be a mix of VBA and a scripting language like python/javascript to access it’s api (do a search for excel api).

This will improve you productivity, but at the cost of high upfront time spent.

3 - Become a Business analysis.

With you background in finance, you could change careers to be a product owner/ business analysis, who do the research and create the work for developers to code. Going through this area, you can have a good career in the financial IT world, it is easier to transition to upper management, than from a pure developer role . This is what my brother did, he was programmer for 3 years, then a business analysis and after several years he is like head of digital operations (one step below CTO) for a massive bank.

But I would say compare salaries, future salaries, career paths etc and other factors before making this move.

TBC ….


4 - If this is just a side skill, then you do not need to learn a whole load of stuff. Most of this stuff, esp the beginner stuff can be learned online.

Most of the time, you will just run a script/program on you machine, do some manual steps (Cause the cost benefit of coding this is not worth it) and run another script, and repeat until you are done.

Here is a list …

- Use mac or dual boot your windows machine to have ubuntu running. These are far better for coding, if you want to do non microsoft stuff. But Windows are upping their game, but not quite their yet (I cannot do work on Windows, to many issues to workaround ).
- The terminal command line (bash) and learn how to manipulate your operating system
	- Also learn what your operating system is and how it works
- version control (mainly  GIT and GITHUB)
- To write procedural code using a language (start with Python version 3, simple, does not have many weirdness like javascript)
	- The basics includes - decisions (if), loop (for/while), methods (calling and creating, parameters, returns), Memory (variables -storing, using, changing), statements/expressions, types and data structures. With this you can program anything, but will take along time, so eventually you use libraries and write your code in a certain way ie object oriented, functional, and use patterns to make you code better designed.
	- Do a tutorial on codecdemy for python, actually very good
	- Do simple coding exercises ie check code wars, to get comfortable writing code, and to see how others would do it.
	- These can be done online
	- I would not learn a framework, as this is just more stuff to learn. and should not be necessary for small tasks.
- Setup computer to be able to run python scripts ( the terminal) and write it (VScode - but need lots of plugins, Pycharm, but start with a simple editor like notepad++ or atom)
	- A good guide is python the hard way, https://github.com/chris-void/pyway/blob/master/Learn%20Python%20The%20Hard%20Way%2C%203rd%20Edition%20.pdf
- Be able to write some simple programs which  interact with the database, http service, files
- Don’t worry about learning computer science topics yet (ie algorithms -sorting/searching, BigO, graphs etc) as most of these will be implemented in libraries, although learning about data structures is necessary. These can learned later, if you want to go deep or just for interest (a good intro book is https://bigmachine.io/products/the-imposters-handbook/ it also has info on software engineering ideas too)
- I suggest be comfortable in one language, know it well, before moving to other languages. All languages are very similar, they have differences esp syntactically
  - If you want to websites, you will have to learn javascript. But if you are comfortable workign in a terminal, then you dont need a website/gui/frontend, as you can see the out put in the terminal or files or database.
- If you want to learn sql, then learn postgres. If you want to code with a database, then you need to learn a library in Python that interacts with the database, this will have it's own way of talking to the database but easier to use one where you write sql in the python code, which will not be sql. If you want to setup postgres (install it first see a tutorial), you can interact with it via the terminal or use a gui like dbeaver (https://dbeaver.io/) which i just started to use and is very good.
  - https://www.postgresqltutorial.com/postgresql-python/insert/
-

TBC…

5 - If you want to learn to build a product to use outside of work (ie to make you money), to eventually commercialise then you have to consider a few thing….
  - This will be a massive undertaking, esp for HFTrading, and I would avoid using something like python for this. Most likely C or Java or C#, due to performance, reliability, maturity, tooling, and help
  - You will need to learn a lot more programming topics, such as concurrency, parallelism, async, message queues, scheduling jobs, frontend gui (either website - means javascript, or app for operating systme) to be able see graphs and tables and have them update (hard to see on a terminal), use lots of libraries which means you have to learn how they work.
  - You will need to be able to test your code, just running it and seeing if the output is good will not work. So need to write unit other tests (testing pyramid). You will also need to run all your tests, build an executable file and store this file somewhere ( also version the file), this might include things like Docker.
  - Your program will likely be large, and will need to split up into modules, this is where Object Oriented programing comes in, design patterns, architectural patterns,
  - You will eventually have to deploy and run the program, at first on your machine but if other want to use it you need to have access to some hosting service. This will be things like AWS, GKE, GCE, Horuku etc, knowing how this works.
  - Due to large programs with lots of files and libraries, you will need to maintain it, so need to have pratices and style code to be maintaable and extendable
  - Depending on the constraints ie each action should take 100 milliseconds, you will need to understand how to improve low latency and high throughput, trade offs between engineering needs (ie scalable, reliable, consistent, secure etc), know how to program these.
  - If doing any sort of trading, you will likely be talking to a 3rd party service, which means understanding rest/soap, http, tcp/ip, working, and security involving this ie tls/ssl, transport information types like json/xml
  - You will probably need to learn a lot about computer science topics to write algorithms which are performanent.
  - You will need to be able to debug programs, use the memomry management tools to view where in your code is going slow or running out of memory, ie things like jsconsole. if you designed you code correctly, you will only have to change a small portion of the code to be more performant and likely less readable and maintable. see https://youtu.be/JoQN4xoXY5Y for a basic example
  - If you want to use machine learning, AI, etc that is more to learn

This is a lot to do, esp on your own. But the downfall of most people who do their own thing is build something with the final product in mind, and having to do too much or end up with a product which does not do what the customers want. Better to build in iterations with few features, and have a working MVP, then add/remove/update features depending on what is needed by the customer (this is lean development and goes hand in hand with Agile developement)

6 - If you want to be dev, then you will need to start at the bottom, lower salary and it will be tough to get in without a CS/maths or similar degree, or have a portfolio (something on github) or have some product that is being used.

TBC ...

7 - I work primarily in java, for most things java (or any jvm language) or C# is good enough, esp for backend/server code. C/rust is good for systems or embedded coding, or high performance code. Other dynamic languages like python, ruby and javascript or good for startups, but have drawbacks esp when running high loads or speeds or tooling. There is alot choice of languages to use, and they have the uses. But for me, I get alot of calls through my recruiter to work on HFT codebases which are built using java. 
