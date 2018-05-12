# Excuting code

## Have main method

To run a Java app a main() method must be supplied. This is where all the code is wired up (objects newed up) and methods run. It is the entry point of a Java app.

## Use command line for single class

This way is best for single file apps (which is rare). If using an IDE then these steps are  very easy and wont really ever need to use the command line. Must have a main method in the class.

NOTE: make sure the path for the jdk is setup

1. compile the class
```bash
javac Helloworld.class
```
2. Run the compiled class
```bash
java Helloworld
```
  - running with arguments that are passed to the main(), all args serparted by space
  ```bash
  java Helloworld arg1 arg2 arg3
  ```

## Use intellij

In class with main, click on the green arrow next to the main() method on the left hand side.

## Use jar

- https://docs.oracle.com/javase/tutorial/deployment/jar/index.html
- https://en.wikipedia.org/wiki/JAR_(file_format)

## Manifest file

A manifest file is created when a jar is created. It contains info about the files that packaged in the jar

- Add entry point for running jar

In manifest file, add `Main-Class: <MyPackage.MyClass>`. Then run the jar.

NOTE: Always have empty line or carriage return on last line

- https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html

### using maven

Always good to have

#### Build jar

- Simple jar

  1. Add to pom.xml

    ```xml
    <build>
      <plugins>
        ...
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-jar-plugin</artifactId>
          <configuration>
              <!-- DO NOT include log4j.properties file in your Jar -->
              <excludes>
                <exclude>**/log4j.properties</exclude>
              </excludes>
              <archive>
                <manifest>
                  <!-- Jar file entry point, where main method is-->
                    <mainClass>com.hanfak.wiring.App</mainClass>
                </manifest>
              </archive>
          </configuration>
        </plugin>

    ```

  2. Run `mvn package`

- Uber/Fat jar - Have jar with dependencies

  1. Add to pom.xml

    ```xml
    <build>
      <plugins>
        ...
      <!-- Make this jar executable -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <configuration>
          <excludes>
            <exclude>**/log4j.properties</exclude>
          </excludes>
          <archive>
            <manifest>
              <addClasspath>true</addClasspath>
              <mainClass>com.hanfak.wiring.App</mainClass>
              <classpathPrefix>dependency-jars/</classpathPrefix>
            </manifest>
          </archive>
        </configuration>
      </plugin>

      <!-- Copy project dependency -->
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
        <version>2.5.1</version>
        <executions>
          <execution>
          <id>copy-dependencies</id>
          <phase>package</phase>
          <goals>
            <goal>copy-dependencies</goal>
          </goals>
          <configuration>
            <!-- exclude junit, we need runtime dependency only -->
            <includeScope>runtime</includeScope>
            <outputDirectory>${project.build.directory}/dependency-jars/</outputDirectory>
          </configuration>
          </execution>
        </executions>
      </plugin>
    ```

  2. Run `mvn package`

Or use maven-assembly-plugin

  ```xml
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <executions>
        <execution>
            <goals>
                <goal>attached</goal>
            </goals>
            <phase>package</phase>
            <configuration>
                <finalName>App</finalName>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifest>
                        <mainClass>Main</mainClass>
                    </manifest>
                </archive>
            </configuration>
        </execution>
    </executions>
  </plugin>
  ```


Can also use **shade plugin** https://maven.apache.org/plugins/maven-shade-plugin/index.html

- https://www.mkyong.com/maven/create-a-fat-jar-file-maven-assembly-plugin/
- https://stackoverflow.com/questions/11947037/what-is-an-uber-jar

#### Run jar

1. Add to pom.xml

  ```xml
  <build>
      <plugins>
        ...
          <plugin>
              <groupId>org.codehaus.mojo</groupId>
              <artifactId>exec-maven-plugin</artifactId>
              <version>1.2.1</version>
              <configuration>
                  <mainClass>com.example.Main</mainClass>
              </configuration>
          </plugin>
        ...
      </plugins>
  </build>
  ```

2. In command line run: `mvn exec:java`

NOTE: The phase this is set is not specified, so should be run as pluging goal instead of using lifecylce ie mvn verify

### Command line

#### creating jar

- Add individually:

 `jar cvf <name of jar>.jar file1 file2 directory1 directoy2 ...`

- Add all, must be in directory

  `jar cvf <name of jar>.jar .`

NOTE: `v` in the flag is for verbose, and is optional

#### Running jar

`java -jar helloworld.jar`

#### Running main() method

`java -cp jarName.jar <packageName.ClassName> <argumentsIfAny>`

## Use Docker

1. Create the jar as above, and check it working
2. Create a dockerfile
3. Run container

see project here https://github.com/hanfak/docker-java-maven-rapidoid this has notes on how to set it up. I have used the maven-assembly-plugin to create the jar. Where the docker file runs this jar.

### Using maven fabric8
