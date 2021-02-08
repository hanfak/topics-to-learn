# Pyramid of Refactoring

https://refactoring.pl/en/pyramid-of-refactoring-discovery/ 

## Discovery

General principles, patterns – at one side allow us to tidy up knowledge, use common approach when solving certain kind of problems. On the other side they might impede our creativity and inspiration. But even then we have something we can base on even if we want to reject it and invent something better.

In case of refactoring to be able to perform it effectively I’ve discovered such a principle and gave it name of “Pyramid of Refactoring”. This rule allows to approach refactoring from the smallest possible transformations into more and more complex ones.

This concept is based on idea that you shouldn’t (although you can) jump into bigger refactorings, like extract new class, extract new method, before you finished dealing with clear sequential flow. Clear flow means that you are able to read and understand your code easily and quickly. This means that it doesn’t contains things like mysterious field / variable names, (deeply) nested conditions and loops. Getting rid of single exit point from your code also might reduce the number of local variables significantly.

How did I discover it? During the last 7-8 years I’ve conducted over 100 workshops about refactoring. They were always using concepts from two core books about refactoring. First book by Martin Fowler was always like a catalogue to me. The second one “Refactoring to Patterns” by Joshua Kerievsky was always a kind of “guidelines” book with steps to follow when going from current legacy code towards expected design pattern. The concept of Refactoring Pyramid is placed between and also visible inside each of these books… although such a name is not used anywhere


In case of Martin Fowler’s “Refactoring” book – each transformation can be placed somewhere higher or lower within the pyramid. For example extract parameter goes into method-level, move method begins the level of classes. But inline or extract variable would be put into the lowest (but basic!) level called level of flow. Extract base class that contains template method allows to think in terms of abstractions / patterns level. Similar case applies to extracting interface to hide a class behind pattern of command or factory.


The second book by Joshua Kerievsky (“Refactoring to Patterns”) takes the subject of refactoring much further. It is a continuation of Martin’s Fowler’s above book. It contains lots of refactorings into some design patterns. Each of these samples can be broken down into set of transformations that goes from the bottom of the pyramid towards its top.

For example in order to extract command design pattern, we start with extracting parts of switch / if-else statements into smaller methods (of lower level of abstractions). Next we put each of these methods into a new class, later extract an interface that is implemented by each such an extracted class. Finally the main classe delegates to command classes hidden behind the abstraction of an interface.

## Example

In my previous post Pyramid of Refactoring – Discovery I talked about origins of Pyramid of Refactoring. Something that inspires me, something I try to engage in lots of places / techniques like Test Driven Development, working with with Legacy Code or just when our daily programming activities take places.

Nowadays applying refactoring techniques is much easier, as tools like (especially) IntelliJ but also Eclipse, NetBeans provide us with lots of automated code transformations. Moreover when we use these transformations wisely then the logic of our code should still work as expected (or rather as it worked before…). Some exceptions to this rule are transformations like “extract field” because when a method sets up a field instead of using local variables we might run into concurrency issues when second thread is running the same method at the same time.

In this post I would like to show you “Refactoring Pyramid in Practice”. In order to do so, I will follow the sequence of small transformations like in one of refactoring examples in “Refactoring to Patterns” book by Joshua Kerievsky. The sample will will be refactoring to Interpreter, but I’ve experienced that my “Pyramid of refactoring” concept can be applied to majority of examples from this book, which is a proof that the concept makes sense.

Let’s start with extract from ProductFinder class.

```java
public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   public List<Product> byBelowPrice(float price) {
       List<Product> foundProducts = new ArrayList<>();
       Iterator<Product> products = repository.iterator();
       while (products.hasNext()) {
           Product product = products.next();
           if (product.getPrice() < price)
               foundProducts.add(product);
       }
       return foundProducts;
   }

   public List<Product> byColor(ProductColor color) {
      List<Product> foundProducts = new ArrayList<>();
      Iterator<Product> products = repository.iterator();
      while (products.hasNext()) {
         Product product = products.next();
         if (product.getColor().equals(color))
            foundProducts.add(product);
      }
    return foundProducts;
  }
}
```

As you see both of the methods are almost the same. The only difference is the condition to to check if given Product should be considered as part of valid output or not.

*** Level of methods ***

Let’s extract the difference (one of the conditions) into a separate method for a while.

```java
public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   public List<Product> byBelowPrice(float price) {
       List<Product> foundProducts = new ArrayList<>();
       Iterator<Product> products = repository.iterator();
       while (products.hasNext()) {
           Product product = products.next();
           if (isSatisfiedBy(price, product))
               foundProducts.add(product);
       }
       return foundProducts;
   }

   private boolean isSatisfiedBy(float price, Product product) {
       return product.getPrice() < price;
   }
}
```

Now when you have a closer look at the extracted method you notice that calling byBelowPrice method entails calling isSatisfiedBy method. But in case of 1000 products the isSatisfiedBy method is called 1000 times with the same value of first parameter (price) and different value of the second parameter (Product).

Such a notice leans our thoughts towards creating BelowPriceSpec class that holds a field that stores the price, and contains a method isSatisfiedBy that takes a single parameter Product.

*** Level of classes ***

```java
public class BelowPriceSpec {
   private float price;

   public BelowPriceSpec(float price) {
       this.price = price;
   }

   public float getPrice() {
       return price;
   }
}

public class ProductFinder {
   ...
   public List<Product> byBelowPrice(float price) {
       BelowPriceSpec belowPriceSpec = new BelowPriceSpec(price);

       List<Product> foundProducts = new ArrayList<>();
       Iterator<Product> products = repository.iterator();
       while (products.hasNext()) {
           Product product = products.next();
           if (product.getPrice() < belowPriceSpec.getPrice())
               foundProducts.add(product);
       }
       return foundProducts;
   }
}
```

Please note that currently the condition uses “belowPriceSpec.getPrice()” instead of parameter price directly. This way when I extract isSatisfiedBy method method again its first parameter is different what allows me to move this method into BelowPriceSpec class.

```java
public class ProductFinder {
       …
       public List<Product> byBelowPrice(float price) {
           BelowPriceSpec belowPriceSpec = new BelowPriceSpec(price);

           List<Product> foundProducts = new ArrayList<>();
           Iterator<Product> products = repository.iterator();
           while (products.hasNext()) {
               Product product = products.next();
               if (isSatisfiedBy(belowPriceSpec, product))
                   foundProducts.add(product);
           }
           return foundProducts;
       }

   private boolean isSatisfiedBy(BelowPriceSpec belowPriceSpec, Product product) {
       return product.getPrice() < belowPriceSpec.getPrice();
   }
}
```

*** Level of abstractions / patterns ***

Here is how BelowPriceSpec class looks like after isSatisfiedBy method has been moved into it and the only temporary getter (getPrice) has been inlined.

```java
public class BelowPriceSpec {
   private float price;

   public BelowPriceSpec(float price) {
       this.price = price;
   }

   public oolean isSatisfiedBy(Product product) {
       return product.getPrice() < price;
   }
}
```

Our next thoughts say that we might end up with lots of such classes like DeliverySpec, SizeSpec, MinAgeSpec (if it is a toy) and so on. This classes will be married by our Spec interfaces, so we can extract it.


```java
public interface Spec {
   boolean isSatisfiedBy(Product product);
}

public class BelowPriceSpec implements Spec {
   private float price;

   public BelowPriceSpec(float price) {
       this.price = price;
   }

   @Override
   public boolean isSatisfiedBy(Product product) {
       return product.getPrice() < price;
   }
}

public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   public List<Product> byBelowPrice(float price) {
       Spec spec = new BelowPriceSpec(price);

       List<Product> foundProducts = new ArrayList<>();
       Iterator<Product> products = repository.iterator();
       while (products.hasNext()) {
           Product product = products.next();
           if (spec.isSatisfiedBy(product))
               foundProducts.add(product);
       }
       return foundProducts;
   }
}
```

*** Coming back to Method Level ***

Now the interfaces has been extracted and is used within byBelowPrice method. But majority of this method is using the Spec interface, not BelowPriceSpec. This way we might extract the part of methods that would be common between similar methods (like byMinAge, bySize) and extract a brand new method bySpec(Spec spec).

```java
public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   private List<Product> bySpec(Spec spec) {
       List<Product> foundProducts = new ArrayList<>();
       Iterator<Product> products = repository.iterator();
       while (products.hasNext()) {
           Product product = products.next();
           if (spec.isSatisfiedBy(product))
               foundProducts.add(product);
       }
       return foundProducts;
   }

   public List<Product> byBelowPrice(float price) {
       Spec spec = new BelowPriceSpec(price);

       return bySpec(spec);
   }
}
```
*** Flow Level ***

Now we are going to have a closer look at bySpec method. It uses very old constructions coming from Java pre 1.5. Let change it into for loop and streams. Martin Fowler in his last book put additional refactoring called “Replace for loop with a stream”.

```java
public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   public List<Product> bySpec(Spec spec) {
       return repository.stream()
               .filter(spec::isSatisfiedBy)
               .collect(Collectors.toList());
   }

   @Deprecated
   public List<Product> byBelowPrice(float price) {
       return bySpec(new BelowPriceSpec(price));
   }
}
```
The other method byBelowPrice does not require “spec” local variable for its readability so it has been inlined.

*** Architecture Level ***

Finally we might think about improving Architectures. The current article is growing so I have decided to explain Architectures level as part of next article. Refactoring Pyramid is S.O.L.I.D.

## SOLID

In my previous post Pyramid of Refactoring – Example I was talking about levels of Refactoring Pyramid while refactoring some java code. We took the simplest case from “Refactoring to Patterns” book and explained the first four levels of refactoring pyramid. In you haven’t gone thought that article – read it before as this article is a continuation.


This article complements the subject by explaining connections between the Pyramid and Uncle Bob’s SOLID principles. We will see how each of SOLID rules acts as basement for each level in the pyramid. We will end up at the top level of architectures.

SINGLE RESPONSIBILITY PRINCIPLE
First of all let’s have a closer look what single responsibility principle means. One reason for a change? This is only common & vague theory to me… When I do explain it, I always talk about SRP in context of abstraction levels. Single responsibility means a lot of things expressed / contained within single word from higher level of abstraction, and refers to a single small thing from low level of abstraction.

In the first case a kind of manager / controller class is a the top entry that delegates to subclasses to perform details. In the second case small action is being performed itself.

Methods should do one thing, as Uncle Bob writes in Clean Code. When I join it with my above explanation the case makes sense to me. A method should refer to single level of abstraction. A method should not contain code that delegates logic to lower level class and deal with low level details at the same time. A method should never contain two levels of abstrations. It should delegate both parts  to lower level class.

This leads us towards things like

split loop into two parts
replace loop with stream
extract smaller methods
extract composed methods
extract smaller classes
Play with the above in such a case. Experiments are the first steps to go forward.

```java
private boolean checkMaxPrice(float price, Product product) {
    return product.getPrice() < price;
}
private boolean checkMinAge(float age, Product product) {
    return product.getMinAge() < age;
}
```

Continue your experiments towards having smaller classes.

```java
public class BelowPriceSpec {
   private float price;

   public BelowPriceSpec(float price) {
       this.price = price;
   }

   public boolean isSatisfiedBy(Product product) {
       return product.getPrice() < price;
   }
}
```
INTERFACE SEGREGATION PRINCIPLE
Once we have a few similar classes, we can think about common way we interact with then. This leads to hiding them behind an interface that refers to a kind of abstraction.

When following the refactoring approach in my previous post we would end up a set of classes like MinAgeSpec, DeliveryTimeSpec, AndSpec and so on.

Finally all of them can implement the Spec interface

```java
public interface Spec {
   boolean isSatisfiedBy(Product product);
}
```

OPEN CLOSED PRINCIPLE
Once we have a setup of interfaces then our common logic is based on these contracts. When a logic is based on contracts or uses such contracts that the logic is not likely to change often. Even when new implementation of such a contract is provided as a parameter of class’s constructor, or method’s parameter – the logic stays the same!

Here is how Open Closed Principle reveals as a next level in Pyramid of Refactoring. Look below at “bySpec” method that is not likely to be changed in the future.

```java
public class ProductFinder {
   private List<Product> repository;

   public ProductFinder(List<Product> repository) {
       this.repository = repository;
   }

   public List<Product> bySpec(Spec spec) {
       return repository.stream()
               .filter(spec::isSatisfiedBy)
               .collect(Collectors.toList());
   }

   @Deprecated
   public List<Product> byBelowPrice(float price) {
       return bySpec(new BelowPriceSpec(price));
   }
}
```
At the same time new implementations of Spec interface are likely – and moreover expected – to happen. For example what happens when we are constrained by delivery time when choosing an item to buy?

```java
public class DeliveryDeadlineSpec implements Spec{
   private Datetime deadline;

   public DeliveryDeadlineSpec(Datetime  dealine) {
       this.deadline = deadline;
   }

   public boolean isSatisfiedBy(Product product) {
       Datetime latestDelivery =
           timeProvider.getTime().plusDays((product.getDeliveryTime())
       return deadline.before(latestDelivery);
   }
}
```

DEPENDENCY INVERSION PRINCIPLE
Finally it’s time to outline the emerging architecture. Architectures emerge at level of

classes
sets of APIs
modules
libraries
microservices
domains
… and probably more

For some time the concept is clear and copy-pasted (ugh…). Once the concept become vague and foggy then it’s time to refactor it again in order to make it clear again.

Let’s come back to ProductFinder and see how Dependency Inversion Principle is expressed.

```
package pl.refactoring.ProductFinder
package pl.refactoring.Spec

package pl.refactoring.specs.BelowPriceSpec
package pl.refactoring.specs.MinAgeSpec
package pl.refactoring.spesc.DeliveryDeadlineSpec
```

Please note that higher level of abstraction (ProductFinder) defined its contract interface Spec. Then the implementations of the interfaces might be delivered in different packages, different modules or even different libraries.

LISKOV SUBSTITUTION PRINCIPLE
There was no clear example for usage of LSP here, but it is placed at level of classes. This is because usually usage of this principle ends up with replacing inheritance with delegation.
