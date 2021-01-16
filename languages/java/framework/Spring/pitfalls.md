# Pitfalls and advice

-it provides too many things as a single dependency, which has caused a lot of pain over the years because teams that used it just for dependency injection needed to constantly update it for security issues non-related to any dependency injection feature, which is the opposite of Guice and Dagger
- when a project use Spring beyond its DI features it becomes extremely coupled to Spring and then it’s architected based on the framework capabilities and not the business logic
- https://dzone.com/articles/spring-pitfalls-proxying
- https://www.toptal.com/spring/top-10-most-common-spring-framework-mistakes
- https://spring.io/blog/2015/11/29/how-not-to-hate-spring-in-2016
