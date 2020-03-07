# Serilization

## What

- To serialize an object means to convert its state to a byte stream so that the byte stream can be reverted back into a copy of the object.
-  A Java object is serializable if its class or any of its superclasses implements either the java.io.Serializable interface or its subinterface, java.io.Externalizable.
- Deserialization is the process of converting the serialized form of an object back into a copy of the object.
- For example, 
  - the java.awt.Button class implements the Serializable interface, so you can serialize a java.awt.Button object and store that serialized state in a file. Later, you can read back the serialized state and deserialize into a java.awt.Button object.

## Links

- https://dzone.com/articles/what-is-serialization-everything-about-java-serial
- https://stackoverflow.com/questions/447898/what-is-object-serialization
- https://gist.github.com/chatton/14110d2550126b12c0254501dde73616

## marshallign and Serilization

- https://stackoverflow.com/questions/770474/what-is-the-difference-between-serialization-and-marshaling

## Json
