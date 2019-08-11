# Customising build lifecycle

example

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-report-plugin</artifactId>
    <version>2.20.1</version>
    <executions>

        <execution>
            <id>surefire-report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
            <configuration>
    <!-- Can place config here for goal, and make it local in scope for this phase -->
            </configuration>
        </execution>
    </executions>
</plugin>
```

- ```<phase>none</phase>```
  - This will override the phase with same execution id in parent pom (ie super pom)
  - the `none` means it will not run this execution in any phase
  - Can still run if run the goal
