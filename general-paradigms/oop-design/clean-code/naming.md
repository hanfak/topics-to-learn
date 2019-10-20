# Naming

- Choose descriptive and unambiguous names.
- It is sometimes a good idea to extract even one-line-if-condition to a separate method, as one can give this method a more descriptive name.
- It is important to keep in mind the keywords specific to different areas of IT, and avoid using them when we mean them in a different context.
  - E.g. do not call `accountList` something which is not a list.
- Do not use names that differ only sligthly, for example `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`.
- Do not use lowercase L together with uppercase O, as this will look like number 10.
  - Just don’t be confusing when you don’t have to.
- Avoid using noise words, like a, an, the, info, data,… to “make up” a new, non-conflicting name.
  - For example would you be able to guess the difference between `ProductInfo` and `ProductData`?
- Don’t try to be funny when choosing names (someone may not understand).
- Use consistent lexicon, e.g. get, fetch, retrieve - decide on one word to use per project, not per developer. Or same with manager vs controller vs driver.
  - BUT be aware to use one word only when semantics are same - for example adding two strings together is not same as adding an element to a list. Then you have to use a different name.
- Problem domain (e.g. customer, account) vs solution domain (e.g. visitor, queue) terms - first try to use solution domain, then problem domain. The more code has to do with the solution domain problems, the more solution domain vocabulary it should use, and vice versa. It is important to know the difference.
- Prefixing everything with same prefix may not be a good idea - as it makes it harder to use code completion. Why to work against your tools? Add no more context to the name than neccessary.
- Don’t be afraid of renaming.
- Avoid encodings. Don't append prefixes or type information.
- Avoid acronyms and avoid confusing names, which may bring anyone who reads the code to the wrong conclusions
- Don’t invent your own language when there is a standard.

## Variable

- Variable name should say what is being measured and the unit of measurement, e.g. `int elapsedTimeInDays` instead of `int i`.
- It is always useful to add the context to the variable names, e.g. `gameBoard` instead of `theList`.
  - Also the whole class is a context to their variables/methods.
- Make your names pronouncable, so that you can later discuss the code without sounding like an idiot.
- Make your variable names be easy to find via a text search - makes your life easier.
- Replace magic numbers with named constants.
- Use Long Names for Long Scopes
  - fields -> parameters -> locals -> loop variables
  - long ------------------------------->    short

## Methods

- Name Methods After What They Do
  - The name of a method should describe what is done, not how it is done.
- Names Describe Side Effects
  - Names have to reflect the entire functionality.
-

## Classes

- Class names should have a noun in the name.
- It is better to have factory methods and private constructors, than a big amount of overloaded constructors
  - because the factory methods can have descriptive names.
- Better add suffixes to interface implementations than prefixes to the interface name.
  - No one needs to know that e.g. `ShapeFactory` is an interface, it’s less ugly to name its implementation `ShapeFactoryImpl`.
- Name Classes After How They Implement Their Interfaces
  - The name of a class should reflect how it fulfils the functionality provided by its interface(s), such as MemoryStream : IStream
