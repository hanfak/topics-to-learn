### Functions/methods

## method signature
- Defines the inputs and outputs of the method
- ie `void aMethod(String firstParam, Intger secondParam)`
  - output is void
  - inputs is firstParam of type STring and secondParam of type Integer
- Can also have `throws` exception
  - ie `void aMethod(String firstParam, Intger secondParam) throws Exception`

## Method body
  - can be empty
    - ie ```String method() {}```
  - where the logic happens
  - any thing that needs to be returned
  - Should use the params provided
    - Although should not change the param
    -
## Parameter list

- No parameters ```String method(){...}```
- parameters
  - parameters are the type of data that the method can receive
  - with one parameter ```String method(int a){...}```
  - with multiple parameters ```String method(int a, NewType b){...}```
    - Can have any length of parameters in method parameter list
      - best to keep this small
  - varags ie ```Integer method(String... x){...}```
    - can pass in any number of arguments of type String, and these will then be a seen as an array of type string, where you can get those arguments
    - multiple parameters and varags
      - if there are one or more params along with the varags, the varags needs to be last
      - ie ```Integer method(Integer a, String b, String... x){...}```
      - Cannot have multiple varage parameters
    - Old school way of doing varags
      - `String[] arg`
  - final parameters
    - ```String method(final int a){...}```
    - cannot change parameter
    - if parameter is an object (ie `Integer b`), then the reference of the object cannot be changed
      - but state of object can be changed
## Overloading methods
  - Same method name with different number of parameter types or type of parameters
  - for example
    - ```String method(){...}```
    - ```String method(int a){...}```
    - ```String method(String a){...}```

## Instance method
  - no static keyword
  - only used with an instance of class

## Static method
  - use of static keyword
  - ```static String method() {...}```
  - no instance needed to be created to be used

## Return type is declared
- ```static String method() {... return ....}```
- return should match the type to be returned of the method in the method signature.
- Can return `null`
- multiple returns
  - using a control flow statement like if else, both blocks should return the same type.
- `return` on its own?
  - exits the level ie if statement or method returns the to higher leve.
  - Example:

```java
  Arraylist<String> list =  new ArrayList<>();

  public void addingToTheList() {

    if(isSunday()) {
        list.add("Pray today")
        return;
    }
  }
```
  - in the above code, if isSunday() == true, then add to list then exit method.
- throw Exception
  - can throw exception and no need to return anything
```java
public String aMethod(int x) throws Exception {
    throw new Exception();
}
```
  - but the method should throw that exception
    - also any other method that uses this method should throw that exception too.
    - but can use `try/catch` and placing the method which throws the exception in the try block and do something with it in the catch block, thus no need to add the `throw exception` in the method signature.

### void

- The void type is used to declare that a method does not return a value.
- a method that has void return type, cannot set a variable to it. As the type of the variable cannot be declared
  -

## Using methods

- passing arguments to a method
- within class
  - just use the name of method
  - ie ```method(1)```
- in different class
  - where instance is initialized and thus intance can be used ie `Instance instance = new Instance();`
  - ```instance.method(1);```
  - Use of static methods
    - `Instance.staticMethod();`
- Defining variable for storing/referencing output of method
  - ```Integer a = instance.method(1);```
  - ```Integer a = method(1);```

## Naming conventions
  - camel case
    - aMethod()
    - method()

## side effects
  - Avoid using setters to alter the Instance
    - new up another instance with changed state instead
    - make fields private
  - Called Methods instead of functions as functions cannot have side effects and only effect he arguments passed to it
  - Links
    - https://en.wikipedia.org/wiki/Side_effect_(computer_science)
    - https://stackoverflow.com/questions/1073909/side-effect-whats-this

## CQRS
  - method should either query and return something, or do something (ie delegate to another object and its behaviour) and return void

## Links

- https://www.tutorialspoint.com/java/java_methods.htm
- http://tutorials.jenkov.com/java/methods.html
