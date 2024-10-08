# Junit

- http://tutorials.jenkov.com/java-unit-testing/simple-test.html

## Junit 5

- https://dzone.com/articles/7-reasons-to-consider-junit-5
- https://youtu.be/6uSnF6IuWIw JUnit 5 Tutorial - Nice & Easy

### Paramatised tests

- https://www.arhohuttunen.com/junit-5-parameterized-tests/

### Junit 4 and Junit 5 running together

```xml
 <build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>3.0.0-M4</version> <!-- this version is important! -->
      <dependencies>
        <dependency>
          <groupId>org.junit.jupiter</groupId>
          <artifactId>junit-jupiter-engine</artifactId>
          <version>5.3.2</version>
        </dependency>
      </dependencies>
    </plugin>
  </plugins>
</build>
```

## Best practices

- https://phauer.com/2019/modern-best-practices-testing-java/

## Extensions

- https://dev.to/kirekov/junit-5-link-tests-with-task-tracker-issues-2fif
- https://www.lambdatest.com/blog/junit5-extensions/
