# Setup the system

- Installing java/JDK
  - Knowing the difference between JDK, JRE and JVM
  - `java -version` to verify
- Setting up the path
  - Setup JAVA_HOME, `export JAVA_HOME=/<your_JDK_folder>` for mac
    - for linus `export JAVA_HOME=/usr/local/jdk`
  - setup java and javac path: `export PATH=$PATH:$JAVA_HOME/bin/`
- Installing and setting up IDE (Intellij)
  - Can use Eclipse or Netbeans, but Intellij is far better
- Settings to use JDK
  - Create new project using maven and add java build in pom.xml
  - See for a common starter pom file https://github.com/hanfak/java-generics/blob/master/pom.xml
    - For options 'groupId' and 'artifactId' when asked, use a package structure like com.<yourname> as groupId and name of project as artifactId.
- Running a simple hello world program through Intellij to check it is working
```java
  public class Example {
      public static void main(String[] args) {
          System.out.println("Hello, World");
      }
  }
```
  - Use of shortcuts ie ```sout``` and ```psvm```

## Java Home

- https://self-learning-java-tutorial.blogspot.com/2017/06/why-and-how-to-set-javahome.html

### Links

- https://www.tutorialspoint.com/java/java_environment_setup.htm
- https://www.java.com/en/download/help/download_options.xml
- https://confluence.atlassian.com/adminjiraserver073/installing-java-861253016.html
- https://github.com/codepath/android_guides/wiki/Setting-up-IntelliJ-IDEA
- https://www.jetbrains.com/help/idea/configuring-mobile-java-sdk.html
