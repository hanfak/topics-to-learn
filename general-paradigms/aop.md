# Aspect oriented Programming (AOP)

- paradigm aiming to extract cross-cutting functionalities, such as logging, into what’s known as “Aspects”.
- achieved by adding behavior (“Advice”) to existing code without changing the code itself. We specify which code we want to add the behavior to using special expressions (“Pointcuts”).

JoinPoint
Simply put, a JoinPoint is a point in the execution flow of a method where an Aspect (new behavior) can be plugged in.

Advice
It’s the behavior that addresses system-wide concerns (logging, security checks, etc…). This behavior is represented by a method to be executed at a JoinPoint. This behavior can be executed Before, After, or Around the JoinPoint according to the Advice type as we will see later.

Pointcut
A Pointcut is an expression that defines at what JoinPoints a given Advice should be applied.

Aspect
Aspect is a class in which we define Pointcuts and Advices.
