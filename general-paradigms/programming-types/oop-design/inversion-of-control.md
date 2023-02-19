# Inversion of control

Related to DIP

- Inversion of Control is a concept that states that objects should not create their own dependencies, but rather the control of dependency creation should be inverted and given to something else

- a method of removing responsibilities from a class to make it simpler and less coupled to the rest of the system. inversion of control is not having to know who will create and use your objects, how, or when. It is about being as dumb and oblivious as possible, as having to know less is a good thing for software design.

- Dependency Injection and Service Locator design pattern is specific implementation that falls under the more generic umbrella term of IoC

- a practical implementation of IoC through the use of a Dependency Injection Container (DIC) such as Guice, Spring

- IOC is also referred to as “the Hollywood principle” because the subject of IOC is being told, “Don’t call us, we will call you.”
  - this means your classes do not have to know when their instances are created, who is using them, or howtheir dependencies are put together.
  - Your classes are plugins, and some external force will decide how and when they should be used

This is linked to use of IoC containers ie Spring

## Links

- https://www.yegor256.com/2017/05/10/inversion-of-control.html

- https://completedeveloperpodcast.com/episode-165/
