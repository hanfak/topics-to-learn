# Project Management - maven

Using maven to manage our dependencies, excute commands (ie docker image creation and starting), compile and zip up, etc.

https://maven.apache.org/

Alternatives are Gradle(new) and Ant(old)

## pom.xml

- structure

## Maven lifecycles

- https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html
-

## Dependencies

* dependency management
* test dependencies
  * Only used for tests, thus do not need to packaged with prod jar
* transistive dependencies
* exclusions
* Maven central to get dependencies

## Plugins

* http://javarevisited.blogspot.co.uk/2016/08/top-10-maven-plugins-every-java-developer-know.html
* https://www.fromdev.com/2012/07/25-best-free-maven-plug-ins-to-make.html

## Profiles

## Resources

## Repositories

## Plugin repository

## Builds

## Excutions

## Modules
* Grab modules with dedicated poms, so these can be excuted in this pom
* https://maven.apache.org/guides/mini/guide-multiple-modules.html
* http://www.codetab.org/apache-maven-tutorial/maven-multi-module-project/


## Properties

*  extracting common things like version numbers or boolean references or paths, to be used else where


## Parent POMs

* inheriting

## Best practises

- http://www.kyleblaney.com/maven-best-practices/
- http://books.sonatype.com/mvnref-book/reference/index.html

## Used plugins

- Fabric8
  - https://maven.fabric8.io/
- findbugs
  - https://gleclaire.github.io/findbugs-maven-plugin/
- pmd
  - https://maven.apache.org/plugins/maven-pmd-plugin/
- pitest
  - http://pitest.org/quickstart/maven/
- surefire
  - http://maven.apache.org/surefire/maven-surefire-plugin/
  - run all unit tests
- maven-surefire-report-plugin
  - generate reports
  - http://maven.apache.org/surefire/maven-surefire-report-plugin/
- Failsafe Plugin
  - run acceptance tests
  - http://maven.apache.org/surefire/maven-failsafe-plugin/
- maven-compiler-plugin
  - allows you to set your java language level
- Flywaydb
  - https://flywaydb.org/documentation/maven/
- Artifactory
  - Store jars and in cloud based space jfrog
  - https://www.jfrog.com/confluence/display/RTF/Maven+Repository
- Jar plugin
  - build jars of app
  - https://maven.apache.org/plugins/maven-jar-plugin/
- deploy plugin
  - http://maven.apache.org/plugins/maven-deploy-plugin/
  - deploy jars to repository
-  Resources Plugin
  - https://maven.apache.org/plugins/maven-resources-plugin/
