# Packaging Application

In general, a java application will have several classes( and thus class files). To run the application, we need all the files to be together. We create a jar or war, which is a zip file which holds all the files (and the libraries in the class path, properties, manifest file etc). The java command can run the jar so the application starts.

## WAR vs JAR

- .jar files: The .jar files contain libraries, resources and accessories files like property files.
- .war files: The war file contains the web application that can be deployed on any servlet/jsp container. The .war file contains jsp, html, javascript and other files necessary for the development of web applications.
  - A .war file has a specific structure in terms of where certain files will be.
  - A WAR has a specific hierarchical directory structure. The top-level directory of a WAR is the document root of the application. The document root is where JSP pages, client-side classes and archives, and static web resources are stored.
  - A .war file is a Web Application Archive which runs inside an application server
  - Web Application Archive intended to be execute inside a 'Servlet Container' and may include other jar files (at WEB-INF/lib directory) compiled classes (at WEB-INF/classes (servlet goes there too)) .jsp files images, files etc. All WAR content that is there in order to create a self-contained module.


## Commands

- https://docs.oracle.com/javase/tutorial/deployment/jar/build.html

### Maven

- If included the package plugin for maven and set the configuration, can run `mvn package`. This should be build a jar, in the target directory.
  - maven-jar-plugin
- Can build an uber jar, which contains all the dependencies in the jar
  - maven-shade-plugin
  - maven-assembly-plugin

## Manifest file

- This states where the main method is, so that the jar can be run
- Can use the build tool to generate this for us (ie maven)
- which hold informative information like versioning, and instructional attributes like classpath and main-class for the JVM that will execute it.

## Links

- https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html
