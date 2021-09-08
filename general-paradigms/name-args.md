# Named Arguments

When we define methods, with several parameters, this can lead to several issues:
* Several parameters might have the same type, this could lead to passing arguments in the wrong order.
* Some arguments are not needed, so when a method is called, we use nulls to replace it or some default value (ie -1) if it is a primitive type. This can lead to confusion from readers of this called method
* Some arguments maybe needed, but can be defaulted. This leads to a lot of method calls which have similar patterns in the arguments, which increase verboisty
* Cognitive load is increased when a method is called with lots of arguments.

How to handle this:
* Some langauges have named arguments, like below:
  ```python
  def count_letter(string,letter = ' '):
      count = 0
      for i in string:
          if i == letter:
              count = count + 1

      return count

  num = count_letter(letter='a',string='dead parrot')  .. (1)
  num = count_letter(string='dead parrot', letter='a') .. (2)
  num = count_letter(string='dead parrot')             .. (3)
  num = count_letter('dead parrot', 'a')               .. (4)
  ```
  * The above code allows for:
    *  setting defaults, thus no need to set arg in method call (3)
    *  calling parameters with same type in different order (1) and (2)
    *  can still call method in standard way of setting it's args (4)
* Other languages do not have this feature, instead common patterns are used:
  * Builder pattern for args
    * Allows to set defaults, makes clear what argument is being set
  * Builder pattern for method
    * Allows to set defaults, makes clear what argument is being set
  * Static factory method
    * Have mutliple methods or constructors (overloaded, using telescoping) to set defaults or null values etc, as well as naming methods with better granuality
  * Tiny types
    * Creating types, which are wrappers around default types (String) or primitives (int). So using these types as parameters, means that you know what arg should be passed into the method
    * This does not prevent passing args in wrong order if the same type is used by multiple params
    * Helps with readability
  * Use methods which wrap the type, with granular name
  ```java
  robot.punch(force(1), speed(100));

  int force(int i) { return i;}
  int speed(int i) { return i;}
  ```
    * This does not prevent wrong order of passing in args
    * Makes it clear to reader what is being passed
  * Use a map as an argument
    * Thus the parameter name is the key, and arg value is the value for that key
    * can be verbose
  * Use a single object to encapsulate all the args
    * An alternative, i think better than map, to capture all args in one object (constructing a new obj)
