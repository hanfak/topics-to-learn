# Shallow vs Deep Copy

- https://blog.wacekdziewulski.ovh/2019/10/28/java-unmodifiable-immutable-copyof/

The problem of aliases arises when a copy of an object’s data is required but instead a copy of the object’s reference is returned. These two types of copies are sometime referred to as deep copy (for a copy of an object’s data) and shallow copy (for a copy of an object’s reference). By sending back a shallow copy, the original object can be manipulated, whereas a deep copy would not cause any harm to the original object.

If such objects are immutable, you do not have to worry about creating aliases of these objects and do not need to provide them with clone methods

sds
