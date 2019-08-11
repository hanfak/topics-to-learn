# Phases

Instead of run lots of goals. For example, running a simple build
`clean:clean compiler:compile compiler:testCompile surefire:test` which is verbose a issue to run (although can create alias in bash profile). Can use phases to do this for us.

From the [table of phases mapped to plugins goals](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Packaging) we can see that each phase has mapping to a goal from a plugin. We can instead run `mvn test` and this will run all the phases before inclusively and thus run all the goals.


package phase - packages up code into a jar or war, depending on what is set in pom

install phase - take the jar file created, and install into local maven repository or m2 folder

deploy phase - deploys to a remote maven repository (ie artifactory)

Site phase - create web site to show how to use created jar

site deploy phase - deploy to some server
