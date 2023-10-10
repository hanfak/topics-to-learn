# String Class

- https://www.journaldev.com/16928/java-string
- https://www.java67.com/2018/01/10-important-points-about-string-in-java.html
- https://javarevisited.blogspot.com/2013/07/java-string-tutorial-and-examples-beginners-programming.html

## format

- New lines
   - String.format("Hallo%n") inserts an operating system specific line break. The result differs depending on the operating system on which your program is running.
   - String.format("Hallo\n") always inserts a Linux line break regardless of the operating system.
   - Best to use \n instead 

## Concatenation

- https://pellegrino.link/2015/08/22/string-concatenation-with-java-8.html

## Splitting

- https://www.java67.com/2019/12/difference-between-stringtokenizer-and.html

## String, String Builder & String buffer

- https://www.java67.com/2014/05/difference-between-stringbuilder-and-StringBuffer-java.html
- https://www.java67.com/2012/08/difference-between-string-and-stringbuffer-in-java.html

## Operations

- https://www.javacodegeeks.com/2017/09/overview-functional-programming.html

```java
String output;

        // replace one placeholder
        output = String.format("Hello %s", "Alex");
        System.out.println(output); // Hello Alex

        // replace multiple placeholders of different types
        output = String.format("The %s costs $%f", "Bag", 12.99f);
        System.out.println(output); // The Bag costs $12.990000

        // format number to two-decimal places
        output = String.format("The %s costs $%.2f", "Bag", 12.99f);
        System.out.println(output); // The Bag costs $12.99

        // add comma number separator
        output = String.format("The %s costs $%,.2f", "Car", 54999.99f);
        System.out.println(output); // The Car costs $54,999.99

        // Enclose a negative numbers with parenthesis
        output = String.format("Absolute zero is %(.2f degrees Celsius", -273.15f);
        System.out.println(output); // Absolute zero is (273.15) degrees Celsius

        // Positive/negative numbers
        output = String.format("Temperature of the Sun %,+d K", 5778);
        System.out.println(output); // Temperature of the Sun +5,778 K

        output = String.format("Temperature of Jupiter %,+d K", -145);
        System.out.println(output); // Temperature of Jupiter -145 K

        // A padded number
        output = String.format("A padded number %010d", 42);
        System.out.println(output); // A padded number 0000000042

        // A left-justified number
        output = String.format("A left-justified number <%-10d>", 42);
        System.out.println(output); // A left-justified number <42        >

        // A right-justified number
        output = String.format("A right-justified number <%10d>", 42);
        System.out.println(output); // A right-justified number <        42>

        // Octal numbers
        output = String.format("An octal number %o", 100);
        System.out.println(output);// An octal number 144
        output = String.format("An octal number %#o", 100);
        System.out.println(output);// An octal number 0144

        // Hexadecimal numbers
        output = String.format("An hex number %x", 100);
        System.out.println(output); // An hex number 64
        output = String.format("An hex number %#x", 100);
        System.out.println(output); // An hex number 0x64

        // Multiple String arguments of multiple types
        output = String.format("The %1s has %2d moons", "Saturn", 53);
        System.out.println(output); // The Saturn has 53 moons

        // Specify a width
        output = String.format("Fun with <%10s>", "Java");
        System.out.println(output); //Fun with <      Java>

        // Specify a left justification with width
        output = String.format("Fun with <%-10s>", "Java");
        System.out.println(output); // Fun with <Java      >

        // Truncate the maximum number of characters
        output = String.format("Fun with <%.1s>", "Java");
        System.out.println(output); // Fun with <J>
    }

```
