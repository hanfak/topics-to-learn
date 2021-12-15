# Arayslist/list

## What is a List

- is an interface for ordered collections with a stable indexing order
- allows duplicate elements to be inserted and provide a predictable iteration order
- Has two implementations: ArrayList and LinkedList

## What is an ArrayList

- backed by a static array that has a fixed size.
- it is a dynamic array
  - The size of the array is fixed on creation, but extended on add/remove etc operations, by creating a new array of greater length and copying the elements
  - The new size of the array is a geometric pattern, to allow for amortization of copying elments
- Entries can be added to the array up to the maximum size of the backing array.
  - When the backing array is full, the class will allocate a new, larger array and copy the old values.
  - This affects performance
  - An ArrayList is initially backed by an empty array. On the first addition to the ArrayList a backing array of capacity 10 is allocated.
  - We can prevent this resizing behavior by passing our preferred initial capacity value to the constructor.
  ```java
  List<String> list = new ArrayList<>(1_000_000);
  ```
    - Initializing the size on creation, improves insertion performance



## Difference between Arrays and ArrayList
  - ????

## Operations on ArrayList

### Creation

- **Creating new ArrayList**

  ```java
  List<Type> anArrayList = new ArrayList<>();
  ```

- **Creating an ArrayList with data**, ie list of Integers

  ```java
  List<Integer> integerList = Arrays.asList(1,2,3,4);
  ```

### General
- **Check if empty**

  - set up an empty list: `List<Integer> anArrayList = new ArrayList<>();`
  ```java
  anArrayList.isEmpty();
  ```
    - will return true if anArrayList is empty.

- **Clear a list**

  - `integerList.clear()` removes all elements from list

- **Size of ArrayList**

  ```java
  int sizeOfList = integerList.size();
  ```

- **Retrieving an element using its index**

  ```java
  intgerList.get(<index>);
  ```
  - `integerList.get(0)` returnz 1
  - `integerList.get(3)` returnz 4
  - `integerList.get(sizeOfList - 1)` returnz 4
  - `integerList.get(5)` throws ArrayIndexOutOfBoundsException


### **Add single element to list**

  ```java
  List<Integer> anArrayList = new ArrayList<>();
  ```
    - `anArrayList.add(5)` return a boolean
    - `System.out.println(anArrayList);` return [5]
      - ArrayList has toString overriden and thus shows the contents of a list instead of the object

  - Add without mutating

    ```java
    List<Integer> anArrayListWithNewElementAtTheEnd = Stream.concat(anArrayList.stream(), Stream.of(11)).collect(Collectors.toList());
    ```
      - Can add as many elements in `Stream.of(...)` if wanted to

    - An alternative using flatMap:

    ```java
    List<Integer> anArrayListWithNewElementAtTheEnd = Stream.of(anArrayList, Arrays.asList(12))
        .flatMap(Collection::stream).collect(Collectors.toList());
    ```
      - Can add as many elements in `Arrays.asList(...)` if wanted to
      - Can use `Collections.singletonList` instead of `Arrays.asList(...)`

- **Add multiple elements to list**

  - Add to an array of integers to the array:
    ```java
    anArrayList.addAll(Arrays.asList(1, 2, 3, 4));
    ```
  - `System.out.println(anArrayList);` returns [5, 1, 2, 3, 4] as anArrayList already has 5 in it
    - Also addAll adds to the end of the list

### **Replace an element at index**

  - setup list: `List<Integer> integerList = Arrays.asList(1,2,3,4);`
  ```java
  integerList.set(1,10);
  ```
    - This will mutate the integerList
    - will return [1,10,3,4]
  - more code but does not mutate original list
    ```java
    List<Integer> listThatHasChangedElement = IntStream.range(0, anArrayList.size()).
          mapToObj(replaceElementAtIndex(anArrayList, 1, 4)).
          collect(Collectors.toList());

    // Where replaceElementAtIndex checks the index in anArrayList to see if it matches  with indexOfElementToReplaceand replaces it with replacementElement
    private static IntFunction<Integer> replaceElementAtIndex(List<Integer> anArrayList, int indexOfElementToReplace, int replacementElement) {
          return index -> index == indexOfElementToReplace ? replacementElement : anArrayList.get(index);
      }
    ```

      - Where 1 is the index to find element to replace
      - where 4 is the replacement
      - This will return [1,4,3,4]


### **Element exist in list**

  ```java
  anArrayList.contains(<element>);
  ```
    - <element> must be of same type of those in anArrayList
    - `anArrayList.contains(2);` will return true as 2 is in the list
    - `anArrayList.contains(10);` will return false as 10 is not in the list

  ```java
  anArrayList.containsAll(<arraylist of elements>);
  ```
    - <arraylist of elements> must all be of same type of those in anArrayList
    - `anArrayList.containsAll(Arrays.asList(1, 5));` will return true as 1 and 5 are in the list
    - `anArrayList.containsAll(Arrays.asList(1, 8));` will return false as 8 is not in the list

### **Find index of an element**

  ```java
  int i = anArrayList.indexOf(3);
  ```
    - will return 3
    - If the arraylist was  [5, 3, 2, 3, 4], then `int i = anArrayList.indexOf(3);` will return the index of the first element it matches with, which is 1

### **Reverse a list**

  ```java
  Collections.reverse(anArrayList);
  ```
    - This will mutate the original list, not great

  ```java
  List<Integer> sortedReversedOrderList = anArrayList.stream().sorted(Collections.reverseOrder()).collect(Collectors.toList());
  ```
    - Can use the comparator, Collections.reverseOrder(), as list is of Integer types.


### **Sort list**

  ```java
  Collections.sort(anArrayList);
  ```
    - This will mutate the original list, not great
    - Uses natural ordering, as Arraylist implements comparable
    - If list contained elements of some user defined object, and does not have some natural ordering (does not implement comparable). then it will not sort and throw an exception with message `java.lang.ClassCastException: com.blah.Blah cannot be cast to java.lang.Comparable`. Thus needs to implement comparable
      - But can use a comparator:
      ```java
      Collections.sort(anArrayList, (x1,x2) -> x1.field - x2.field);
      ```
        - Where field is some type of some number.
        - instead of `(x1,x2) -> x1.field - x2.field` use this `Comparator.comparingInt(x -> x.id)`

  ```java
  List<Integer> sortedList = anArrayList.stream().sorted().collect(Collectors.toList());
  ```

  - Does not mutate the original list
  - Uses natural ordering, as Arraylist implements comparable

### **sublist of list**

  if anArrayList is [4,3,2,1,5]

  ```java
  List<Integer> integers = anArrayList.subList(0, 1);
  ```

    - This will create a new list, with elements from anArrayList starting at 0 index up to but not including 1st index. This will return only a list of one element

  ```java
  List<Integer> integers = anArrayList.subList(2, 4);
  ```

    - This will return [2,1]

  ```java
  List<Integer> integers = anArrayList.subList(0, 6);
  ```

    - This will throw `java.lang.IndexOutOfBoundsException: toIndex = 6` as the list is only size 5

### **Remove an element**

  - Two ways of doing this, either by remove an element using the index, or getting the first element matched.

  ```java
  anArrayList.remove(0)
  ```

    - removes element at index 0 from the list

  ```java
  anArrayList.remove(new Integer(5));
  ```

    - removes the object from the list

  - Without mutating
    - Removing the first specific element in the list

      ```java
      Integer elementToRemove = 1;
      List<Integer> integers = Arrays.asList(2, 4, 1, 2, 5, 1);
      int elementIndex = integers.indexOf(elementToRemove);
      List<Integer> listWithfirstOneRemoved = IntStream.range(0, integers.size())
            .filter(currentIndex -> currentIndex != elementIndex)
            .mapToObj(integers::get)
            .collect(Collectors.toList());
      ```

      OR

      ```java
      List<Integer> result = new ArrayList<>(integers); // copy the integers list
      result.remove(Integer.valueOf(elementToRemove))
      ```

    - Removing the element at a specific index in the list

      ```java
      List<Integer> result = new ArrayList<>(integers); // copy the integers list
      result.remove(integers.indexOf(elementToRemove))
      ```

## Links
  - https://dzone.com/articles/the-developers-guide-to-collections-lists
  - https://docs.oracle.com/javase/8/docs/api/java/util/List.html
