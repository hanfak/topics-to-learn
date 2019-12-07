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

We can see it has two goals, and the phase these goals are run in. The excution 'default-compile' is bound to the 'compile' phase. So when 'mvn compile' is run, it excutes defualt-compile goal ie 'compile'.

If execution does not have a phase set, it will use the default phase that has been set. If not default has been set, then the execution will not be run during the build. If there is a defualt phase set, we can override it by explicitly setting it in the pom ie '<phase>compile</phase>'.

To execute on the command line, `mvn compiler:compile@default-compile`

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

To configure plugins: http://maven.apache.org/guides/mini/guide-configuring-plugins.html


## Surefire

- Used to run unit tests
- Class name of test file should end with Test

## Failsafe

- Used to run integration tests
- Class name of test file should end with IntegrationTest or IT
- can run integration only test `mvn test-compile failsafe:integration-test failsafe:verify`

## Create Plugin

- https://developer.okta.com/blog/2019/09/23/tutorial-build-a-maven-plugin
