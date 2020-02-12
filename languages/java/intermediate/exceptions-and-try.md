# Exceptions

- Types
  - Runtime/unchecked
  - checked
  - errors

- https://www.javacodegeeks.com/2017/12/handling-exceptions-java.html
- https://dzone.com/articles/how-to-deal-with-exceptions

## List of Exceptions

- https://stackify.com/top-java-software-errors/


https://dzone.com/articles/ignore-exceptions-in-java

## Throwing Exceptions
  - `throw`
  - message
  - type of exception
  - through code that compiles but throws runtime exception
  - methods throwing exception
    - `throws`
    - defined in superclass of abstract and interface

## Handle exceptions

- When your code encounters an exception, it must either
  - handle it,
  - let it bubble up,
  - wrap it, or
  - log it
- If your code can programmatically handle an exception (e.g., retry in the case of a network failure), then it should
- If it can't handle it, it should generally either let it bubble up (for unchecked exceptions) or wrap it (for checked exceptions).
- However, it is ultimately going to be someone's responsibility to log the fact that this exception occurred if nobody in the calling stack was able to handle it programmatically.
  - This code should typically live as high in the execution stack as it can
-

- https://stackify.com/best-practices-exceptions-java/
- https://stackify.com/common-mistakes-handling-java-exception/
- https://www.javaworld.com/article/3269036/learn-java/java-101-mastering-java-exceptions-part-1.html
- https://www.javaworld.com/article/3269037/mastering-java-exceptions-part-2-advanced-features-and-library-types.html
- https://dzone.com/articles/9-best-practices-to-handle-exceptions-in-java

## try - catch
  - catch exceptions
    - logging exceptions and stack trace that are thrown
    - wrapping Exceptions
      - Why?
      - As runtime exceptions
  - finally block
  - multi catch
- creating custom exceptions
- try with resources

## Anti patterns to handling exceptions

- Log and Throw
  - Either log the exception, or throw it, but never do both.
  - Logging and throwing results in multiple log messages for a single problem in the code, and makes life hell for the support engineer who is trying to dig through the logs.
- Throwing Exception
  - `public void foo() throws Exception {`
  - defeats the purpose of using a checked exception. It tells your callers "something can go wrong in my method."
  - Not specific enough
  - Declare the specific checked exceptions that your method can throw. If there are several, you should probably wrap them in your own exception
- Throwing the Kitchen Sink
  - `public void foo() throws MyException, AnotherException, SomeOtherException, YetAnotherException {`
  - Throwing multiple checked exceptions from your method is fine, as long as there are different possible courses of action that the caller may want to take, depending on which exception was thrown.
  - If you have multiple checked exceptions that basically mean the same thing to the caller, wrap them in a single checked exception.
- Catching Exception
  - `try { foo(); } catch (Exception e) { LOG.error("Foo failed", e); }`
  - Catch the specific exceptions that can be thrown.
  - The problem with catching Exception is that if the method you are calling later adds a new checked exception to its method signature, the developer's intent is that you should handle the specific new exception.
  -  If your code just catches Exception (or worse, Throwable), you'll probably never know about the change and the fact that your code is now wrong.
- Destructive Wrapping
  - `catch (NoSuchMethodException e) { throw new MyServiceException("Blah: " + e.getMessage()); }`
  - This destroys the stack trace of the original exception, and is always wrong.
- Log and Return Null
  - `catch (NoSuchMethodException e) { LOG.error("Blah", e); return null; }`
  - `catch (NoSuchMethodException e) { e.printStackTrace(); return null; }`
  - Although not always incorrect, this is usually wrong.
  - Instead of returning null, throw the exception, and let the caller deal with it.
  - You should only return null in a normal (non-exceptional) use case (e.g., "This method returns null if the search string was not found.").
-  Catch and Ignore
  - c`atch (NoSuchMethodException e) { return null; }`
  - This one is insidious. Not only does it return null instead of handling or re-throwing the exception, it totally swallows the exception, losing the information forever.
- Throw from Within Finally
  - `try { blah(); } finally { cleanUp(); }`
  - This is fine, as long as cleanUp() can never throw an exception.
  - In the above example, if blah() throws an exception, and then in the finally block,cleanUp() throws an exception, that second exception will be thrown and the first exception will be lost forever.
  - If the code that you call in a finally block can possibly throw an exception, make sure that you either handle it, or log it. Never let it bubble out of the finally block.
- Multi-Line Log Messages
  - `LOG.debug("Using cache policy A"); LOG.debug("Using retry policy B");`
  - Always try to group together all log messages, regardless of the level, into as few calls as possible.
  - So in the example above, the correct code would look like:
    - `LOG.debug("Using cache policy A, using retry policy B");`
  - Using a multi-line log message with multiple calls to log.debug() may look fine in your test case, but when it shows up in the log file of an app server with 500 threads running in parallel, all spewing information to the same log file, your two log messages may end up spaced out 1000 lines apart in the log file, even though they occur on subsequent lines in your code.
- Unsupported Operation Returning Null
  - `public String foo() { /** Not supported in this implementation.*/ return null; }`
  - When you're implementing an abstract base class, and you're just providing hooks for subclasses to optionally override, this is fine.
  - However, if this is not the case, you should throw an UnsupportedOperationExceptioninstead of returning null.
    - This makes it much more obvious to the caller why things aren't working, instead of her having to figure out why her code is throwing some random NullPointerException.
- Ignoring Interrupted Exception
  - `while (true) { try { Thread.sleep(100000); } catch (InterruptedException e) {} doSomethingCool(); }`
  - InterruptedException is a clue to your code that it should stop whatever it's doing.
    - Some common use cases for a thread getting interrupted are the active transaction timing out, or a thread pool getting shut down.
  - Instead of ignoring the InterruptedException, your code should do its best to finish up what it's doing, and finish the current thread of execution.
    - So to correct the example above:
      - `while (true) { try { Thread.sleep(100000); } catch (InterruptedException e) { break; } doSomethingCool(); } `
- Relying on getCause()
  - `catch (MyException e) { if (e.getCause() instanceof FooException) { ...`
  - The problem with relying on the result of getCause is that it makes your code fragile.
  - It may work fine today, but what happens when the code that you're calling into, or the code that it relies on, changes its underlying implementation, and ends up wrapping the ultimate cause inside of another exception?
  - Now calling getCause may return you a wrapping exception, and what you really want is the result of getCause().getCause().
  - Instead, you should unwrap the causes until you find the ultimate cause of the problem.
    - Apache'scommons-lang project provides ExceptionUtils.getRootCause()to do this easily.

- General
  - Failing to handle error states
  - Failing to anticipate error states
  - Hiding error states (e.g. catch Exception)
  - Complecting control flow
-


## checked exceptions

### Why bad

- Exceptions increase the complexity of our code
- Exceptions disrupt the flow of execution in our applications, jumping from the point at which the exception is thrown to whatever point, with whatever state, our application defines the catch point


- https://phauer.com/2015/checked-exceptions-are-evil/
- https://programming.guide/java/checked-exceptions-good-or-bad.html
- http://literatejava.com/exceptions/checked-exceptions-javas-biggest-mistake/
- https://stackoverflow.com/questions/613954/the-case-against-checked-exceptions
- https://stackoverflow.com/questions/37834521/why-one-should-try-throw-unchecked-exception-over-checked-exception
