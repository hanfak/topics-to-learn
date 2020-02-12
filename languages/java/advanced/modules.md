# Modules

**Java 9+ - will need the jdk of 9 and above**

- Different to maven modules
  - are a way to organize your project into several subprojects (modules). With Maven, you can control the versions of these modules and the dependencies between these modules. Each module will produce an artifact.
  - Java modules are a way to strongly encapsulate your classes. It does not provide any means to control the version of an artifact you are using.
- By default, a type in a module is not accessible to other modules unless it’s a public type and you export its package
- List all modules `java --list-modules`
  - Standard java libraries start with `java.`
  - Standard jdk libraries start with `jdk.`
  - At the end of the module name, is the jdk version this module is from
- Describe module `java --describe-module java.sql`
  - output example below
    ```
    java.sql@13
    exports java.sql
    exports javax.sql
    requires java.transaction.xa transitive
    requires java.logging transitive
    requires java.xml transitive
    requires java.base mandated
    uses java.sql.Driver
    ```
  - 'exports' lists all the packages this module can be used by
    - This means that public classes are, by default, only public within the module unless it is specified within the module info declaration.
  - An `exports…to` directive enables you to specify in a comma-separated list precisely which module’s or modules’ code can access the exported package—this is known as a qualified export.
  - The 'requires' keyword indicates that this module depends on another module.
  - The 'uses' keyword indicates that this module uses a service. making the module a service consumer
    - A service is an object of a class that implements the interface or extends the abstract class specified in the uses directive.
  - A 'provides...with' module directive specifies that a module provides a service implementation—making the module a service provider,
    - The provides part of the directive specifies an interface or abstract class listed in a module’s uses directive and the with part of the directive specifies the name of the service provider class that implements the interface or extends the abstract class.
  - To specify a dependency on another module and to ensure that other modules reading your module also read that dependency—known as implied readability—use requires transitive
    - `requires transitive modulename;`
    - if moduleOne has declared `requires transitive moduleTwo;`. Then any module that read moduleOne, will implicitly read moduleTwo
  - `open, opens, and opens…to` allows reflection to packages you want it to have
- jmod file
  -???
- It is not necessary to explicitly add the java.base module because it is always implicitly added
- compiling
  - The -d option specifies the destination directory for the compiled classes
    ```
      javac -d mods/com.mydeveloperplanet.jpmshello
      src/com.mydeveloperplanet.jpmshello/module-info.java
      src/com.mydeveloperplanet.jpmshello/com/mydeveloperplanet/jpmshello/HelloModules.java
    ```
- Execution
  -  module-path option sets the directories where the modules can be found. The module option sets the main class that must be invoked
  ```
  java --module-path mods
  --module com.mydeveloperplanet.jpmshello/com.mydeveloperplanet.jpmshello.HelloModules
  ```
- Packaging
  - The file option specifies the location and name of the JAR file.
  - The main-class option specifies the entry point of the application — in other words, where the main class resides.
  - The C option specifies the location of the classes to include in the JAR file
  ```
  jar
  --create
  --file target/jpms-hello-modules.jar
  --main-class com.mydeveloperplanet.jpmshello.HelloModules
  -C mods/com.mydeveloperplanet.jpmshello .
  ```
- Execute package/jar
  ```
  java
  --module-path target/jpms-hello-modules.jar
  --module com.mydeveloperplanet.jpmshello/com.mydeveloperplanet.jpmshello.HelloModules
  ```
- If importing package, which has not been declared inthe module-info file, we get `error: static import only from classes and interfaces`

### Links

- http://tutorials.jenkov.com/java/modules.html

## Examples

- https://mydeveloperplanet.com/2018/01/10/java-9-modules-introduction-part-1/
- https://mydeveloperplanet.com/2018/01/24/java-9-modules-with-intellij-and-maven-part-2/
- https://mydeveloperplanet.com/2018/02/07/java-9-modules-directives-part-3/
- Clean architecture
  - https://medium.com/slalom-engineering/clean-architecture-with-java-11-f78bba431041
- https://www.baeldung.com/java-9-modularity


## Migration

- https://www.romexsoft.com/blog/migrate-to-java-9/
