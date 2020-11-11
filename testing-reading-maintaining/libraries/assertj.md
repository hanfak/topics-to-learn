- https://professional-practical-programmer.com/2016/06/26/assert-j/
- https://dzone.com/articles/assertj-and-collections-introduction
- https://dzone.com/articles/fluent-assertions-with-assertj?fromrel=true
- https://www.baeldung.com/assertJ-java-8-features
- https://www.baeldung.com/introduction-to-assertj

## describedAs

- when assertions fails, the message returned to the user can be consfusing
- using the method `describedAs`, allows you to pass in a message and possible values to give a better output to help the user make changes to pass the test
- You will need to use this at the beginning of the assertion

```java
assertThat(false).describedAs("Message to help with passing test").isTrue();
```

## custom asssertions

- https://www.javacodegeeks.com/2018/01/write-custom-assertj-assertions.html

```java
public class CoffeeAssert extends AbstractAssert<CoffeeAssert, Coffee> {

    public CoffeeAssert(Coffee actual) {
        super(actual, CoffeeAssert.class);
    }

    public static CoffeeAssert assertThat(Coffee actual) {
        return new CoffeeAssert(actual);
    }

    public CoffeeAssert hasType(Coffee.Type type) {
        isNotNull();

        if (actual.getType() != type) {
            failWithMessage("Expected the coffee type to be <%s> but was <%s>", type, actual.getType());
        }

        return this;
    }

    // hasStrength(Strength) omitted ...

    public CoffeeAssert isNotDecaf() {
        isNotNull();

        if (actual.getStrength() == Coffee.Strength.DECAF) {
            failWithMessage("Expected a coffee but got decaf!");
        }

        return this;
    }
}

```
Using the assetion

```java
import static com.example.coffee.CoffeeAssert.assertThat;
...

Coffee coffee = new Coffee();
coffee.setStrength(Strength.STRONG);
coffee.setType(Type.ESPRESSO);

assertThat(coffee)
    .hasType(Type.ESPRESSO)
    .isNotDecaf();
```
