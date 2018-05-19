# packages and imports

A way of organising interfaces and classes, to avoid conflicts. Similar to directories. Logically group similar items together. Applying access restriciton to the package.

Package names are in lowercase and cannot start with special character or digit. Can have _ in the name.

Any class in a package can access anything in other classes that is not `private` defined

- static imports

```java
import static java.lang.System.out;

out.println("Hello static  import!");
```

```java
import static <package>.ImportsExamples.SOME_CONSTANT;

String constant = SOME_CONSTANT;
// Instead of String constant = ImportsExamples.SOME_CONSTANT;
```

- import one

  ```java
  import com.hanfak.Dog;
  ```

- import all

  ```java
  import com.hanfak.*;
  ```

  - Imports all classes from this package
  - not good if only need to import up to 2 or 3 classes


- Same class conflicts
  - Use fully qualified name

  ```java
  com.hanfak.Dog.run();

  com.hanfak.Dog dog = new com.hanfak.Dog();
  ```
    - When another import has same Class name and thus conflict


- class path
  - libraries/classes that accessible
