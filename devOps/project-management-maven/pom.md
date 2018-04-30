# POM

- POM = Project Object Model
- In xml
- Only one POM.xml per project

## Contents of a pom

### General Project Info

Things like:

- Project name
- URL
- devs and contributors
- license details
- artifactId
- groupId
- version

### Build Settings

Such as:

- Can customise default maven build
- Change location of source and test files
- Add Plugins
- Add plugin goals to lifecycle

### Build Environment

Contains profiles that can be used in different environments

### POM Relationships

How parent and modules interact, inherit settings and properties

## Basic pom.xml

This is basic pom.xml of the project.

NOTE: ```<!-- -->``` is how comments are written. Below the comments are optional and only for description.

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!--model version is the version of project descriptor your POM conforms to.-->
  <modelVersion>4.0.0</modelVersion>
  <!-- Maven Coordinates below -->
  <groupId>com.blah</groupId> <!-- id of organisations group -->
  <artifactId>blah</artifactId> <!-- ID of the project, normally the name -->
  <version>1.0-SNAPSHOT</version>
</project>
```

### Super POM

In fact there is a `super pom`, which this pom above inherits from. It inherits `compiler, surefire, jar, resources`

Can see this if run ```mvn clean package``` in the project directory in the terminal. you will see plugins being run and the `target` directory being created and a jar with the version `blah-1.0-SNAPSHOT.jar` in it. Notice that `blah` is the artifactid is part of the name of the jar

If we change the version to 2.0-SNAPSHOT and run  ```mvn package``` a new jar is created in the target directory.

See ????? for more info on running maven builds.

This super pom allows us to inherit from it and perform mvn package which compiled it and produced a jar.

The `super pom + project pom = effective pom`. To see this in IntelliJ, go to search `ctrl + shift + a`, and type `effective pom`. This will show the file.

## Packaging

We can package our project into a jar or war (For web apps to be run on web containers like tomcat). By default it is a jar.

We can add the following to decide what type of packaging to use a war, before `</project>`

```xml
 <packaging>war</packaging>
 ```

There are different types of packaging to choose from `pom, jar, maven-plugin, ejb, war, ear, rar, par`

## Links

- https://maven.apache.org/pom.html
-
