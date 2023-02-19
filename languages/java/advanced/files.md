# Files IO

## REading
### For small files use
```java
byte[] bytes = Files.readAllBytes(Path.of(fileName));
String text = Files.readString(Path.of(fileName));
List<String> lines = Files.readAllLines(Path.of(fileName));
Stream<String> lines = Files.lines(Path.of(fileName));
```

### LArge files

- use nio
-  FileInputStream
  - we read a binary file byte by byte and then process these bytes
  ```java
  try (FileInputStream is = new FileInputStream(fileName)) {
    int b;
    while ((b = is.read()) != -1) { // -1 is EoF
      System.out.println("Byte: " + b);
    }
  }
  ```
  -  access is relatively expensive
- large binary files with the NIO.2 InputStream
```java
try (InputStream is = Files.newInputStream(Path.of(fileName))) {
  int b;
  while ((b = is.read()) != -1) {
    System.out.println("Byte: " + b);
  }
}
```
- Reading faster with BufferedInputStream
  - loads data from the operating system not byte by byte, but in blocks of 8 KB and stores them in memory. The bytes can then be read out again bit by bit – and from the main memory, which is much faster.
  ```java
  try (FileInputStream is = new FileInputStream(fileName);
     BufferedInputStream bis = new BufferedInputStream(is)) {
    int b;
    while ((b = bis.read()) != -1) {
      System.out.println("Byte: " + b);
    }
  }
  ```
  - The only exception is if you do not read data byte by byte, but in larger blocks whose size is adjusted to the block size of the file system.
- Reading large text files with FileReader
  - When being loaded, an InputStreamReader can be used to convert their bytes into characters. Place it around a FileInputStream, and you can read characters instead of bytes
  ```java
  try (FileInputStream is = new FileInputStream(fileName);
     InputStreamReader reader = new InputStreamReader(is)) {
    int c;
    while ((c = reader.read()) != -1) {
      System.out.println("Char: " + (char) c);
    }
  }
  ```
  -  with FileReader: It combines FileInputStream and InputStreamReader,
  ```java
  try (FileReader reader = new FileReader(fileName)) {
    int c;
    while ((c = reader.read()) != -1) {
      System.out.println("Char: " + (char) c);
    }
  }
  ```
- Read text files faster with BufferedReader
  - improves upon InputStreamReader
  ```java
  try (FileReader reader = new FileReader(fileName);
     BufferedReader bufferedReader = new BufferedReader((reader))) {
    int c;
    while ((c = bufferedReader.read()) != -1) {
      System.out.println("Char: " + (char) c);
    }
  }

  try (FileReader reader = new FileReader(fileName);
     BufferedReader bufferedReader = new BufferedReader((reader))) {
    String line;
    while ((line = bufferedReader.readLine()) != null) {
      System.out.println("Line: " + line);
    }
  }
  ```
  - BufferedReader achieves higher speeds by extending the InputStreamReader's 8 KB buffer with another buffer for 8,192 decoded characters.
  - it offers the additional method readLine(), which allows you to read and process the text file not only character by character but also line by line
- Reading text files faster with the NIO.2 BufferedReader
  ```java
  try (BufferedReader reader = Files.newBufferedReader(Path.of(fileName))) {
    int c;
    while ((c = reader.read()) != -1) {
      System.out.println("Char: " + (char) c);
    }
  }
  ```
-
## JAva 8

- https://reflectoring.io/processing-files-using-java-8-streams/

## Streams and Buffers

## Creating files

- https://www.callicoder.com/how-to-create-new-file-java/


## Paths

## Locking

- https://dzone.com/articles/locking-files-in-java
- https://www.java67.com/2018/01/how-to-lock-file-before-writing-in-java.html

## PDF

- https://dzone.com/articles/pdf-creation-with-java

## CSV

- https://examples.javacodegeeks.com/core-java/java-convert-csv-excel-file-example/


## Links

- https://examples.javacodegeeks.com/core-java/java-8-read-file-line-line-example/
- https://www.marcobehler.com/guides/java-files
- https://www.happycoders.eu/java/how-to-read-files-easily-and-fast/
