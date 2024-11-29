# Mapstruct
* A library for automating and simplifying mappings between objects
* General usage is between mapping between database objects and domain objects (vice versa)
## Usage
* When mapping complex object structures, start by mapping the simplest parts first and then combine them and put together to make a whole.
  * Now and then take a look at the generated code. In this way, you will be more confident about what you are doing
## Advantages
*  provides feedback faster: during the compile time.
  * the Java compiler will generate warnings or errors if the source or target Java class attributes have not been considered by the mapping definition.
* easy to use and understand. Performances are also great
* Reduces boilerplate code
*  generates type-safe mapping code at compile time
* Highly customizable
* useful if classes are huge and doing it manually could be too slow, or for cases where both clases are going to be the same
## Disadvantages
* https://kenbonny.net/why-automatic-mapping-is-an-antipattern
*  rely on runtime mapping model and bean introspection
  * you need to write unit tests to ensure the correctness of bean mapping policy.
* The syntax is can be less intuitive
* high probability for bugs, especially with refactoring
  * conceals compile time errors into runtime errors. If you forget to map a property then try and access it, with AutoMapper you get a runtime error, but if done manually with a simple LoC, you get a red squiggle in your IDE before you even try and build it. You can get around this by unit testing each of the maps, but if anything that's more code than just mapping manually, and merely testing simple assignments a lot of the time.
  *  can't easily navigate code. If you try and find all usings for a setter on your property, you won't. This can lead to subtle bugs as you change a name somewhere but not in the DTO; or you make refactoring a little harder because it's not clear what's used.
  *  when you're trying to find where a value is used or set there's an opaque layer hiding things and compile time errors become runtime errors. It hurts refactoring because it's hard to know if a property is still used.
* May not save time
  * Configuration complexity
  * Issues debugging 
    * ie fields that have 0 references but that are really used. Classes with fields that don’t match or mapping configurations that do custom stuff aren’t explicit on the code
  * can't easily modify one of our models to suit the needs of it's layer, because custom AutoMapper rules are harder to write than just changing a line or two in a custom mapper class. So now teams aren't changing models to fit needs, and are instead basically copy+pasting model classes from one layer to another without regard to what each layer's model should look like.
* Complex mapping scenarios may not be covered, leading to hacks to get it working with the library
* Performance maybe less optimal than manual mapping
* Issues with 3rd party apps
* If not thought out (a concisous decision with trade offs), and just used cause of "this is always the way" or tutorial, then it might fail the YAGNI or KISS pattern
* If not careful, people can mix business rules with mapper
* It enforces conventions, which might not be what you want or have issues with in the future
## Links 
* https://mapstruct.org/
* https://mapstruct.org/documentation/stable/reference/html/
* https://www.baeldung.com/mapstruct
* https://martinfowler.com/bliki/LocalDTO.html
* https://plugins.jetbrains.com/plugin/10036-mapstruct-support
* https://blogs.prama.ai/mapstruct-a-traditional-task-on-modern-way-spring-part-1-4e586ceaa22d
  * https://medium.com/tag/mapstruct