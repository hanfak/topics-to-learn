# Build Lifecycles

What a project is built, it follows set of phases.

There are three lifecyles in Maven:

1. Clean
  - Cleans up previous build
  - IE everything in target directory is deleted
2. Default/Build
  - Handles project building and deployment
3. Site
  - Handles creation of project site documentation
  -

All Lifecycles can be customised.

Each lifecycle has its own *build phases*. A build phase represent a stage in the lifecycle. The phase *executes a goal*.

Running a goal:

`mvn help:describe -Dcmd=clean`

mvn - to run Maven
help - run the plugin help
describe - run the goal describe
-D - is the parameter being passed to the goal

For example this command describes the phases withing the lifecycle clean. See below:

```
[INFO] --- maven-help-plugin:3.0.1:describe (default-cli) @ blah ---
[INFO] 'clean' is a phase within the 'clean' lifecycle, which has the following phases:
* pre-clean: Not defined
* clean: org.apache.maven.plugins:maven-clean-plugin:2.5:clean
* post-clean: Not defined
```

The order of the phases, are the order in which they run. The clean phase has a goal (`org.apache.maven.plugins:maven-clean-plugin:2.5:clean`), which is from the maven plugin and it executes clean. The `post-clean` does not have mapping to a goal.

NOTE can see all the commands in IntelliJ by looking for the maven tool window (menu view > tool window > maven OR on right hand side maven option should be there). Click on  `<project name> -> lifecycle`


## Build/Default Lifecycle

Here is the list of phases in default

1. validate - validate the project is correct and all necessary information is available
2. compile - compile the source code of the project
3. test - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
4. package - take the compiled code and package it in its distributable format, such as a JAR.
5. verify - run any checks on results of integration tests to ensure quality criteria are met
6. install - install the package into the local repository, for use as a dependency in other projects locally
7. deploy - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

These lifecycles have goals and/or plugins bound to them

For all the 23 lifecycles see (https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference). Not all of theses have a binding.

Call a phase for example `mvn compile` this will run everything up to and includin compile so it will run validate and everything within the link (7 phases in total will run).

If a goal has been mapped to a phase we can bind it ourselves. We can also override a binding ourselves.

See Plugins next
