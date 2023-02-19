# Random numbers

## Common

### Math.random
```Java
double d = Math.random();
```

### java.util.Random

```Java
Random random = new Random();
int i = random.nextInt();
random.ints(0, 1000).limit(7).forEach(System.out::println);
random.ints(7, 0, 1000).forEach(System.out::println);
```

###  ThreadLocalRandom
```Java
Random random = ThreadLocalRandom.current();
int randomNumber = random.nextInt();
int number = 1 + random.nextInt(10);

```
- backed by Random class

## Seed Value

- this is used to generate a predicatable set of numbers for the random generators

## Non predicatable

- should use for cryptographic use cases ie passwords
- java.security.SecureRandom
```java
SecureRandom secureRandom = new SecureRandom();
double strongRandomNumber = secureRandom.nextDouble();
```
## Links

- https://www.happycoders.eu/java/random-number/
