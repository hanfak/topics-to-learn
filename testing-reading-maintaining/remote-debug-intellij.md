First lets create a Java application which keeps on printing increasing number indefinitely with a delay of 5 seconds between each number.

```java
package com.blah;

public class App {
    public static void main(String[] args) {
        System.out.println("Starting the remote debugging application");
        System.out.println("The application will be running inside a docker image");
        int i = 0;
        while(true){
            System.out.println("Value of i is " + i);
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            i++;
        }

    }
}
```

Package the application in a jar. I’m using maven, but you can use your preferred way to package the jar.
Now lets create a docker file for this application.


```
FROM openjdk:8
WORKDIR /app
ENV JAVA_TOOL_OPTIONS -agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n
COPY remote-debugging-1.0-SNAPSHOT.jar  remote-debugging.jar
ENTRYPOINT ["java", "-cp", "remote-debugging.jar", "com.blah.App"]
```

he thing to note is the 3rd line where I’m setting JAVA_TOOL_OPTIONS environment variable. This variable tells the JRE that it has to enable JPDA session so that the application can be debugged remotely using Java Debug Wire Protocol (JWDP).
Lets create the docker file. Make sure your jar and Dockerfile are in the same directory.

`docker build -t remote-debugger:0.1 .`

Run the application.

`docker run -d -p 8000:8000 remote-debugger:0.1`

This will start your application in daemon mode and also will expose 8000 port on host machine.
You’ll see a log line like below.

`Listening for transport dt_socket at addres: 8080`

Now lets configure remote debugging in Intellij.
Goto Run > Debug > Edit Configurations

Click + and add a remote configuration.
debugger mode - Attacht ot remote vm
transport - socket
host - ip address
command line args - `-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8000`
use module classpath - remote debugging

Select Attach to remote JVM for Debugger Mode.
Enter IP address of remote host and Port that you configured.
Hit Apply.

Add a break-point to the print statement.
Goto Run > Debug and select the configuration that we just created. It should start the debugger.

You’ll see following logs.
`Connected to target VM address: ...`

Intellij will load all the variables and call stack in the window.

Goto the logs of your application, you’ll see they have stopped progressing and are waiting for debugger to move to next statement.
