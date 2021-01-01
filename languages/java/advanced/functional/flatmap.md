# Flatmap

-  is applicable for anything that is a “container of something”
  -  Stream<T> and CompletableFuture<T>
-  Combination of mapping then flattening
-  The idea for map
  -  take all elements of a stream or collection and apply a function to
    ```java
    Stream.of(1, 2, 3, 4)
      .map(x -> x * 2)
      .collect(Collectors.toList())
    // -> [2, 4, 6, 8]
    ```
- Applying map to create a list of lists
  ```java
  Stream.of(1, 2, 3, 4)
    .map(x -> Stream.of(-x, x, x + 1))
    .collect(Collectors.toList())
  /*
  [java.util.stream.ReferencePipeline$Head@3532ec19,
  java.util.stream.ReferencePipeline$Head@68c4039c,
  java.util.stream.ReferencePipeline$Head@ae45eb6,
  java.util.stream.ReferencePipeline$Head@59f99ea]
  */
  ```
  -  For every singular element, we’re creating a plural. If you perform a map with a plural
  -  Instead use flatmap
    ```java
    Stream.of(1, 2, 3, 4)
      .flatMap(x -> Stream.of(-x, x, x+1))
      .collect(Collectors.toList())
    // [-1, 1, 2, -2, 2, 3, -3, 3, 4, -4, 4, 5]
    ```
- Example
  - We are given only a Stream<Manager> and our goal is to determine all the salaries of all employees, including Managers and their Employees.
  ```java
  class Employee {
    private String firstName, lastName;
    private Integer yearlySalary;
    // getters, setters, toString
  }
  class Manager extends Employee {
    private List<Employee> employeeList;
    // getters, setters, toString
  }
  ```
  - Instead of using forEach and start digging through those salaries.
    - **This, unfortunately, would model our code to the structure of the data and would cause needless complexity**
  - Use flatmap
  ```java
  List.of(manager1, manager2).stream()
    .flatMap(m ->
      Stream.concat(m.getEmployeeList().stream(), Stream.of(m)))
    .distinct()
    .mapToInt(Employee::getYearlySalary)
  ```
