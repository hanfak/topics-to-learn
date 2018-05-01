# Maven Plugins

list of available plugins (https://maven.apache.org/plugins/)

Plugins provide a set of goals. A goal represents a specific task which contributes to the building and management of the project. IT be bound to 0 or more build phases.

It is just a  downloadable jar file with exposed functionality.

## How to use it

Go to a specific plugin and look at its usages ie for compiler its documentation is https://maven.apache.org/plugins/maven-compiler-plugin/usage.html

## To run individual goal

`mvn compiler:compile` will just run this goal from the compiler plugin. This plugin is already in pom, as it is inherited from the super pom

```xml
<build>
  <plugins>
    <plugin>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.1</version>
      <executions>
        <execution>
          <id>default-compile</id>
          <phase>compile</phase>
          <goals>
            <goal>compile</goal>
          </goals>
        </execution>
        <execution>
          <id>default-testCompile</id>
          <phase>test-compile</phase>
          <goals>
            <goal>testCompile</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

We can see it has two goals, and the phase these goals are run in.

NOTE: Always run `clean` before any other phase.

## Modifying Plugins

In the above section we saw the plugin for compile from the super pom (in the effective pom). In our project pom, we can modify this by adding the same xml, and changing some of the contents. for example

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.1</version>
      <!-- Here we override the plugin in the superpom by adding some optional parameters into the configuration -->
      <configuration>
        <!-- put your configurations here -->
        <verbose>true</verbose>
        <source>1.8</source>
        <target>1.8</target>
      </configuration>
      <executions>
        <execution>
          <id>default-compile</id>
          <phase>compile</phase>
          <goals>
            <goal>compile</goal>
          </goals>
        </execution>
        <execution>
          <id>default-testCompile</id>
          <phase>test-compile</phase>
          <goals>
            <goal>testCompile</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

To get a list of options for example for compile goal go to its goal (https://maven.apache.org/plugins/maven-compiler-plugin/compile-mojo.html)

To get the maven coordinates, check the `full name` at the top of the page from the link above, ie `org.apache.maven.plugins:maven-compiler-plugin:3.7.0:compile`, where it is split as so <groupID>:<artifactId>:<version>:<goal>

Can add any of the parameters, like verbose in the xml above.
