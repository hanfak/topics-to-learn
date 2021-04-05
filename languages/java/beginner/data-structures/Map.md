# Map

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Map](#map)
	- [HashMap](#hashmap)
	- [Full buckets](#full-buckets)
	- [Treeifying](#treeifying)
	- [Links](#links)
	- [Why hashcode is used is in hashmap](#why-hashcode-is-used-is-in-hashmap)
	- [Links](#links)

<!-- /TOC -->

-  is an interface that maintains key-to-value relationships, and retains only unique keys
- If the same key and different value is added to a map, the old value is replaced by the new value.
- Implementations
  - hashmap
  - treemap
  - LinkedHashMap
- Other languages call it a dictionary

## HashMap

- hash table, but with a few additional embellishments
- Initially the bucket entries will be stored in a list.
- When it comes to finding a value, the hash of the key is calculated and then the equals() method is used to find the key in the list.
  - Because of the mechanics of hashing the key and using equality to find it in the list, duplicate keys are not permitted in a HashMap.
  - Inserting the same key simply replaces the key currently stored in the HashMap.
- initialCapacity and loadFactor affect performance
  - can be set via constructor args
  - The capacity of a HashMap represents the current number of buckets that have been created, which defaults to 16.
    - An accurate initialCapacity will avoid the need to automatically rehash as the table grows.
  - The loadFactor represents how full the hash table is allowed to get before the capacity is automatically increased.
    - Increasing the capacity and recalculating hashes is a procedure known as rehashing, which doubles the number of buckets available and redistributes the data stored.
    - It is also possible to tweak loadFactor, but 0.75 (the default) provides a good balance between space and time of access.
    - A loadFactor of higher than 0.75 will reduce the rehashing requirement, but access will become slower as buckets will generally become fuller
    - Setting the initialCapacity to the maximum number of elements divided by the loadFactor will prevent a rehash operation from occurring.
- operations
  - constant-time support for get() and put() operations, but iteration can be costly.
    - high loadfactor and initialcapacity can impact iteration

## Full buckets

- Due to using hashcode for the hashtable, there are around 4billion available numbers (range of an int).
  - but the number of objects you could choose to create is much larger. Therefore some objects must share the same hash code, by the pigeonhole principle.
- This problem of keys sharing buckets, leads to the issue of how to find the correct entry (key-value) when they have the same hashcode
  - This leads to the bucket containing a linkedlist, to being changed to a red black tree, when the number of elements associated with a bucket reaches a threshold value
  - The use of the tree as default is not worth it for small numbers in linked list
  - So the hashcode is used to check the buckets, if no buckets then can create new linked list in bucket of the entry
    - if bucket exists it will use equals, if not equals it will add it to the linked list or tree. Otherwise overwrite if equals

## Treeifying

- internal aspect of hashmap
- when a bucket becomes highly populated. If the bucket elements are implemented as a LinkedList, traversal to find an element becomes on average more expensive as the list grows.
- To reduce this linear affect, the bucket turns from list to tree (treeenodes), when the treeifying_threshold is reached
- This is not done at the beginning
  - tree nodes are double the size of list nodes
  - A well-distributed hashing function will rarely cause buckets to be converted to TreeNodes.
- If this happens needs to change initialCapacity and loadFactor
- Implements a red-black tree structure, for better performance in searching
  - Offers worst case guarentees
- If the hash codes are the same, it uses the compareTo method of Comparable if the objects implement that interface, else the identity hash code.


## Links

- https://stackoverflow.com/questions/30164087/how-does-java-8s-hashmap-degenerate-to-balanced-trees-when-many-keys-have-the-s/30180593
- https://stackoverflow.com/questions/43911369/hashmap-java-8-implementation



## Why hashcode is used is in hashmap

- The idea of a hashtable is that you want to be able to realize a datastructure called a dictionary in an efficient way. A dictionary is a key/value store, i.e., you want to be able to store certain objects under a certain key and later on be able to retrieve them again using the same key.
- One of the most efficient ways to access values is to store them in an array. For instance, we could realize a dictionary that uses integers for keys and Strings for values like so:
```java
String[] dictionary = new String[DICT_SIZE];
dictionary[15] = "Hello";
dictionary[121] = "world";

System.out.println(dictionary[15]); // prints "Hello"
```
- Unfortunately, this approach is not very general at all: the index of an array has to be an integer value, but ideally we'd like to be able to use arbitrary kinds of objects for our keys, not only integers.
- Now, the way to solve this point is to have a way of mapping arbitrary objects to integer values which we could then use as keys for our array. In Java, that's what hashCode() does. So now, we could try to implement a String -> String dictionary:
```java
String[] dictionary = new String[DICT_SIZE];
// "a" -> "Hello"
dictionary["a".hashCode()] = "Hello";

// "b" -> "world"
dictionary["b".hashCode()] = "world";

System.out.println(dictionary["b".hashCode()]); // prints world
```
- But hey, what if there is some object which we'd like to use as a key, but its hashCode method returns a value that's greater than or equal to DICT_SIZE? Then we'd get an ArrayIndexOutOfBoundsException and that would be undesirable. So, let's just make it as big as we can, right?
```java
public static final int DICT_SIZE = Integer.MAX_VALUE // Ooops!
```
- But that would mean that we would have to allocate ginormeous amounts of memory for our array, even if we only intend to store a few items. So that can't be the best solution, and in fact we can do better. Let's assume we had a function h that for any given DICT_SIZE maps arbitrary integers into the range [0, DICT_SIZE[. Then we could just apply h to whatever the hashCode() method of a key object returns and be certain that we stay in the boundaries of the underlying array
```java
public static int h(int value, int DICT_SIZE) {
    // returns an integer >= 0 and < DICT_SIZE for every value.
}
```
- That function is called a hash function. Now we can adapt our dictionary implementation to avoid the ArrayIndexOutOfBoundsException:
```java
// "a" -> "Hello"
dictionary[h("a".hashCode(), DICT_SIZE)] = "Hello"

// "b" -> "world"
dictionary[h("b".hashCode(), DICT_SIZE)] = "world"
```
- But that introduces another problem: what if h maps two different key indices to the same value? For instance:
```java
int keyA = h("a".hashCode(), DICT_SIZE);
int keyB = h("b".hashCode(), DICT_SIZE);
```
- may yield the same values for keyA and keyB, and in that case we would accidentally overwrite a value in our array:
```java
// "a" -> "Hello"
dictionary[keyA] = "Hello";

// "b" -> "world"
dictionary[keyB] = "world"; // DAMN! This overwrites "Hello"!!

System.out.println(dictionary[keyA]); // prints "world"
```
- Well, you may say, then we just have to make sure that we implement h in such a way that this can never happen. Unfortunately, this isn't possible in general. Consider the following code:
```java
for (int i = 0; i <= DICT_SIZE; i++) {
    dictionary[h(i, DICT_SIZE)] = "dummy";
}
```
- This loop stores DICT_SIZE + 1 values (always the same value, actually, namely the String "dummy") in the dictionary. Mhh, but the array can only store DICT_SIZE different entries! That means, when we use h, we would overwrite (at least) one entry. Or in other words, h will map two different keys to the same value! These "collisions" can't be avoided: if n pigeons try to go into n-1 pigeon holes, at least two of them have to go into the same hole.
- But what we can do is to extend our implementation so that the array can store multiple values under the same index. This can easily be done by using lists. So instead of using:
```java
String[] dictionary = new String[DICT_SIZE];
```
- we write :
```java
List<String>[] dictionary = new List<String>[DICT_SIZE];
// Side remark: note that Java doesn't allow the creation of arrays of generic types, so the above line wouldn't compile...but it's the idea
```
- That will change the access to the dictionary as follows:
```java
// "a" -> "Hello"
dictionary[h("a".hashCode(), DICT_SIZE)].add("Hello");

// "b" -> "world"
dictionary[h("b".hashCode(), DICT_SIZE)].add("world");
```
- In case our hashfunction h returns different values for all our keys, this will result in lists with only one element each, and retrieving elements is really simple:
```java
System.out.println(dictionary[h("a".hashCode(), DICT_SIZE)].get(0)); // "Hello"
```
- But we already know that in general h will map different keys to the same integer sometimes. In these cases, the lists will contain more than one value. For retrieval, we have to go through the whole list to find the "correct" value, but how would we recognize it?
- Well, instead of storing the value alone, we could always store the complete (key,value) pair in the lists. Then lookup would be performed in two steps:
  - Apply the hashfunction to retrieve the correct list from the array.
  - Iterate through all pairs stored in the retrieved list: if the pair with the desired key is found, return the value from the pair.
- Now adding and retrieving have become so complex that it's not indecent to treat ourselves separate methods for these operations:
```java
List<Pair<String,String>>[] dictionary = List<Pair<String,String>>[DICT_SIZE];

public void put(String key, String value) {
    int hashCode = key.hashCode();
    int arrayIndex = h(hashCode, DICT_SIZE);

    List<Pair<String,String>> listAtIndex = dictionary[arrayIndex];
    if (listAtIndex == null) {
        listAtIndex = new LinkedList<Pair<Integer,String>>();
        dictionary[arrayIndex] = listAtIndex;
    }

    for (Pair<String,String> previouslyAdded : listAtIndex) {
        if (previouslyAdded.getKey().equals(key)) {
            // the key is already used in the dictionary,
            // so let's simply overwrite the associated value
            previouslyAdded.setValue(value);
            return;
        }
    }

    listAtIndex.add(new Pair<String,String>(key, value));
}

public String get(String key) {
    int hashCode = key.hashCode();
    int arrayIndex = h(hashCode, DICT_SIZE);

    List<Pair<String,String>> listAtIndex = dictionary[arrayIndex];
    if (listAtIndex != null) {
        for (Pair<String,String> previouslyAdded : listAtIndex) {
            if (previouslyAdded.getKey().equals(key)) {
                return previouslyAdded.getValue(); // entry found!
            }
        }
    }

    // entry not found
    return null;
}
```
- So, in order for this approach to work, we actually need two comparison operations: the hashCode method to find the list in the array (this works fast if hashCode() and h are both fast) and an equals method which we need when going through the list.
- This is the general idea of hashing, and you will recognize the put and get method from java.util.Map. Of course, the above implementation is an oversimplification, but it should illustrate the gist of it all.
- Naturally, this approach is not limited to Strings, it works for all kinds of objects, since the methods hashCode() and equals are members of the top-level class java.lang.Object and all other classes inherit from that one.
- As you can see, it doesn't really matter if two distinct objects return the same value in their hashCode() method: the above approach will always work! But still it is desirable that they return different values to lower the chances for hash collisions produced by h. We have seen that these can't be avoided 100% in general, but the less collisions we get, the more efficient our hashtable becomes. In the worst case, all keys map to the same array index: in that case, all pairs are stored in a single list and finding a value will then become an operation with costs linear in the size of the hashtable.

## Links

- https://beginnersbook.com/2013/12/hashmap-in-java-with-example/
- https://www.javacodegeeks.com/2017/11/java-hashmap-detail-explanation.html
- https://dzone.com/articles/how-to-use-java-hashmap-effectively
