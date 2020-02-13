### Functions/methods

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

		- [Functions/methods](#functionsmethods)
	- [method signature](#method-signature)
	- [Method body](#method-body)
	- [Parameter list](#parameter-list)
	- [Overloading methods](#overloading-methods)
	- [Instance method](#instance-method)
	- [Static method](#static-method)
	- [Return type is declared](#return-type-is-declared)
		- [void](#void)
	- [Using methods](#using-methods)
	- [Naming conventions](#naming-conventions)
	- [side effects](#side-effects)
	- [CQRS](#cqrs)
	- [Links](#links)

<!-- /TOC -->

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
  - Cannot be overridden
  - Disadvantage - breaks encapsulation
    - allow state to be maintained across all instances of a class
    - If a variable can be altered by any instance of a class then the fundamental principle behind encapsulation/information hiding is lost entirely
  - Disadvantage - Cannot mock if used in a classes
    - If a instance method calls a static method, and you need to mock it as it is calls an expensive (time/money/performance) operation (ie database), it becomes hard to add a mock for it. Thus hard to test the instance method as a unit.
  - Disadvantage - polymorphism goes out the window
    - Cannot override
  - Disadvantage - Cannot handle state
    - As other calls, which is not the class of the static method can change it's state
    - Causes concurrency bugs
  - One rule-of-thumb: ask yourself "does it make sense to call this method, even if no Obj has been constructed yet?" If so, it should definitely be static.
  - Requirements for static methods
    - If you are writing utility classes and they are not supposed to be changed.
    - If the method is not using any instance variable.
    - If any operation is not dependent on instance creation.
    - If there is some code that can easily be shared by all the instance methods, extract that code into a static method.
  - Reason for static methods
    - Performance: if you want some code to be run, and don't want to instantiate an extra object to do so, shove it into a static method. The JVM also can optimize static methods a lot
    - Practicality: instead of calling new Util().method(arg), call Util.method(arg), or method(arg) with static imports. Easier, shorter.
    - Adding methods: you really wanted the class String to have a removeSpecialChars() instance method, but it's not there (and it shouldn't, since your project's special characters may be different from the other project's), and you can't add it , so you create an utility class, and call removeSpecialChars(s) instead of s.removeSpecialChars().
    - Purity: taking some precautions, your static method will be a pure function, that is, the only thing it depends on is its parameters. Data in, data out. This is easier to read and debug, since you don't have inheritance quirks to worry about. You can do it with instance methods too, but the compiler will help you a little more with static methods (by not allowing references to instance attributes, overriding methods, etc.).

## Return type is declared

- ```static String method() {... return ....}```
- return should match the type to be returned of the method in the method signature.
- Can return `null`
- multiple returns of same type
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
- Return multiple types
  - not possible
  - Can get around this by:
    - returning an object wrapper which holds all the types you want to return
    - return a Pair (part of jdk) or a tuple library
    - return an Object ArrayList/Array
    - Return a string with delimiters

### void

- The void type is used to declare that a method does not return a value.
- a method that has void return type, cannot set a variable to it. As the type of the variable cannot be declared
  -

## Using methods

- passing arguments to a method
- within class, private method
  - just use the name of method
  - ie ```method(1)```
- in different class
  - where instance is initialized and thus intance can be used ie `Instance instance = new Instance();`
    - ```instance.method(1);```
    - ```instance.methodTwo(1, "hello");```
    - ```instance.methodThree(1, new Car(new Engine(), "Honda"), Arrays.asList(1,2,3), (x, y) -> x > y);```
  - Use of static methods
    - `Instance.staticMethod();`
- Defining variable for storing/referencing output of method
  - ```Integer a = instance.method(1);```
  - ```Integer a = method(1);```

## Naming conventions

  - camel case
    - aMethod()
    - method()
  - Should be descriptive

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
