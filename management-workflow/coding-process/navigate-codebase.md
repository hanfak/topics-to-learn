# Navigate codebase

When asked to do some work in a code base, we need to know where to do it, what effects it causes in the code base, how it links with the domain/business.

There is no one method that fits all situations. There are different types of codebases, different levels of developer experience, etc etc

Tips:

- Understand how the app flows, from the input to the app (ie http request) all the way to the output (ie http response).
  - This can lead to a rabbit hole, as there may be many branches depending on the input or the data stored or the responses from other dependencies (ie calls to other apps).
  - The better designed (clean architecture), there easier it is too follow the flow of the input to output
  - Regardless of well designed, readable codebase, with time and added functionality, the code eventuallys becomes more complex and harder to follow.
- Find similar acceptance tests (especially end to end) this will help understand the domain/business logic being implemented in the code
  - This might be hard to follow in the code, if cannot debug
  - Best practice to start with acceptance test using a similar one, then follow the errors, which will guide you through the code base.
- Know specific key classes where the flow will generally go through
  - ie controllers of the server, where the entry point is; rules engine; database; marshallers/unmarshallers; wiring/config (where objects are created)
- Know the dependencies from acceptance test. This will give you a clue of some sort of class that talks to it (ie http client).
- Know where the request is being unmarshalled or being marshalled (Created) to the input of the app or talking to other dataproviders
- Find the controllers, usually have the paths in the method (which are mentioned in the acceptance test). This should help with following the flow of the code to the logic of the app
- Find what tables are being changed or queried in datastores (ie databases). Can find where the query or method to do this is at
- IF cannot understand the flow from the code, put a break point and use the debugger while running an end to end test
- Check the Readme or any documentation
- pair program with someone more experienced
- Talk to experts or people who have worked on it
  - Trust no one, they may forget, be confused, misremember
- If using a library that has little documentation, then check its tests to see how it is used. If there are no tests in the library or poor code coverage. you should not be using this library
- Find one thing you know the code does, and trace those actions backward, starting at the end.
  - Let’s call those connected pieces of code a “chain of actions.”
  - ie you know that the code you’re viewing ultimately creates a file with a list of movie titles. Figure out where in the code — the specific, few lines — it generates that file. Then, move one step backward and figure out how it places the info in the file. Then, move another step backward and figure out where the info came from. And so on…
  - Repeat that process multiple times, and you’ll rapidly increase your understanding of more and more pieces of the overall codebase.
    - For different stories or flows or endpoints
- Read high quality code
- Understand the domain that the code base is covering
- As you go through the code, document it, draw flow diagrams
- Draw an app level architectural diagram, get high level architectural diagram (how all apps interact)
- Write from scratch, but only good for small projects, as there might be too many business rules and lots of testing to do
- Refactor and adding tests

## Links

- https://selftaughtcoders.com/how-to-quickly-and-effectively-read-other-peoples-code/
- https://simpleprogrammer.com/master-new-codebase-record-time/
- https://www.reddit.com/r/learnprogramming/comments/89pjdy/how_to_learn_a_new_codebase_quickly/
