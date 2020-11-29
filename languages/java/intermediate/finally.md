# Finally


- The try statement also lets you run code at the end with a finally clause regardless of whether an exception is thrown.
```java
try {
  //code that may throw an exception and/or
  // opens some resource
}
// Does not need to be here if no exception thrown in try blcok
catch(Exception e) {

}
finally {
  //
}
```
-  If an exception is thrown, the finally block is run after the catch block. If no exception is thrown, the finally block is run after the try block completes.
- finally block always at the end
- finally is typically used to close resources such as files or databases
- Example of reading a line from a file
```java
public void oldApproach(Path path1, Path path2) throws IOException {
  BufferedReader in = null;
  BufferedWriter out = null;
  try {
    in = Files.newBufferedReader(path1);
    out = Files.newBufferedWriter(path2);
    out.write(in.readLine());
  } finally {
    if (in != null) in.close();
    if (out != null) out.close();
 }
}
```
- Closing resources can lead to issues
  - you forget to add it, or write error prone code
  - in the above code if in.close() throws exception, then out.close() is never closed
  - To avoid this we can do
  ```java
  ...
  } finally {
    try {
      in.close();
    } catch (IOException e) {}
    try {
      out.close();
    } catch (IOException e) {}
  }
  ```

## Autoclosable interface & try-with-resources

- try-with-resources avoids the user having to use a finally blcok to close resources (ie in file example above)
- Instead, we can wrap the methods which opens some resource within the try-with-resources part, and if those methods implement Autoclosable interface, it will close the resource when the try block has finished, by calling the close() method from Autoclosable interface
-  the resources (args for try) are closed before any programmer-coded catch blocks are run.
  - This means that we can catch the exception thrown by close() if we wish
  - or we can allow the caller to deal with it.
- Resources are closed in the reverse order from which they were created
- example
  ```java
  public void oldApproach(Path path1, Path path2) throws IOException {
    try (BufferedReader r = Files.newBufferedReader(path1);
        BufferedWriter w = Files.newBufferedWriter(path2))   {
      out.write(in.readLine());
    }
  }
  ```
  - This code is shorter

- AutoClosable interface
  - should be idempotent
    - Idempotent means that the method can called be multiple times without any side effects or undesirable behavior on subsequent runs.
    - ie  it shouldn’t throw an exception the second time or change state or the like
    - No side effects
  - Can throw exception (due to interface)
    - but should avoid this, especially a checked exception
