# Mutual Exclusion

- locks
- synchronized
- Atomic

## Which to use

-  In general, if you're using Java, synchronized statements and methods are easier to program with than locks.
- And they can prevent many common pit falls that can occur when using locks.
-  So, if synchronized methods or statements will work for your needs, they're a good default option.
- That said, there may be times when you need to work with locks in more complex ways, perhaps **acquiring and releasing a series of locks in a nested or hand over hand manner**, and that's not possible with a synchronized statement,
- but locks do allow more flexibility to be acquired and released in different scopes and to be acquired and released in any order.
- But with that increased flexibility, comes additional responsibility
