# packages and imports

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
