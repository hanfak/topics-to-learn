
# Starting a maven project

Use the IDE to do this, it is much easier than using the command line.

NOTE: Make sure you have an internet connection to allow maven to download stuff.

## Starting archtype project

This will create a simple project with a prod file and test file, some dependencies and plugins in the pom.xml. In most cases, these files will be amended to suit the projects needs.

### Via IntelliJ

1. click file> new project
2. click maven on right hand side
3. tick archtype box
4. select `maven-archetype-quickstart` click next
5. Name group id ie com.project
6. Name artifact ie project-name
7. click next (change if you want)
8. click next (I normally change the folder of the project)
9. click finish

This will start to download all the dependcies, you can see this at the bottom right of Intellij. Sometimes a pop up will ask to `import` or `enable auto-import`, click auto import makes life easier. You can check the `project tool window > External libraries` to see the libraries of the dependencies that have been downloaded and can be used in this project.

Go into the pom.xml and change the following version to the current version of java you are using.

```xml
<maven.compiler.source>1.7</maven.compiler.source>
<maven.compiler.target>1.7</maven.compiler.target>
```

### Via command line

Follow the example in the documentation

- https://maven.apache.org/archetypes/maven-archetype-quickstart/

## Starting a non archtype project

This will be the bog standard way of doing it. It will give you a blank canvas to work with. Much better to use to help customise what you want.

### Via IntelliJ

1. click file> new > project
2. click maven on right hand side
3. Name group id ie com.project
4. Name artifact ie project-name
5. click next (I normally change the folder of the project)
5. click finish

It will be good to add the following to pom.xml to set the java version

```xml
<properties>
    <java.language.level>1.8</java.language.level>
</properties>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.6.0</version>
      <configuration>
        <source>${java.language.level}</source>
        <target>${java.language.level}</target>
      </configuration>
    </plugin>
  </plugins>
</build>
```
