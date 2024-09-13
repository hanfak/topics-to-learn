# Separation of Concerns

- Use of dependency injection, DIP help with this
- Improves modularity, testability, cohesion and coupling


### Areas to separate

- Essential and Accidental Complexity

## Ideas

“Separation of Concerns is about splitting up your code into different layers”. Correct! But also wrong.

“Separation of Concerns is separating UI code from business logic”. Correct! But… also wrong.

“Separation of concerns is about splitting up your application into different domains and then put these domains into different (micro) services”. Correct! But … also wrong.

“Separation of concerns is decomposing processes into different steps and put these steps into proper code units”. Correct! But also wrong!

Each of the above statements is wrong if you think it is the only one that is true. All of these statements are correct if you understand that all of them are correct. I see a lot of people who think too narrowly about this concept. And this sometimes causes weird design and architectural decisions.

It will make more sense once you understand where ‘Separation of Concerns’ come from. It was coined by Edgar W. Dijkstra, a Dutch mathematician and computer scientist. He used this term in an essay called ‘On the role of scientific thought”. In this essay, Dijkstra promotes the idea of studying one aspect of a subject, in isolation. He called this scientific thought or separation of concerns. In short, focus your attention on only one aspect at the time.

It is easy to translate this into the context of software design. In the context of software design, ‘Separation of Concerns’ is seen as a design principle. And in essence, it tells us that different aspects of the problem we are solving should be separated in code so that we can focus on that aspect in isolation. Simply said: you need to isolate different aspects of your code from each other.

In essence, it tells us to separate the code we need for different aspects of the problem we are solving so that we can focus on those aspects in isolation. And those aspects, that can be on any level. This can be on the level of domains and microservices, it can be on the level of process and business logic, it doesn’t really matter. The key thing to understand is the importance of isolation.

## Links 

- https://www.linkedin.com/posts/jasongorman_tailwindcss-htmx-activity-7183056247577792514-OyT-/?utm_source=share&utm_medium=member_android