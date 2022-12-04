# Correct By configuration

an architecture paradigm where objects are always in a valid state, or the system doesn’t compile. Parameters used to construct the object are checked at compile time.

In this architecture, programmers still code, but they can’t possibly mess it up (theoretically) ➔ Framework.

Correct by Configuration: an architecture paradigm that reduced the system to a highly tested and secure DSL.

In this architecture, programmers don’t code, they configure the application through the DSL ➔ Platform.
Low Code is a form of configuration.

How to create a DSL?
1. Team up with someone who perfectly understands the business domain and the requirements.
2. Make idioms out of these requirements.
3. Choose configuration style (JSON, CoffeeScript JSON, YAML…).
4. Represent the requirements in this configuration style.
5. Create the DSL using what you’ve learned with 3 and 4. Keep it very high level (example: When an order is made, …).

## Links

- https://youtu.be/lm4jEcnWeKI
