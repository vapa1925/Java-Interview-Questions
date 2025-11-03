# Java-Interview-Questions
Collection Interview Questions

1)Parent Interface of collections class? (Iterable)

2)Collections hierarchy?

3)Uses of collections?

 1. Efficient Data Storage
 2. Easy Data Manipulation
 3. Iteration and Traversal
 4. Sorting and Searching
 5. Type Safety and Generics
 6. Thread-Safe Operations
 7. Flexible Data Structures
 8. Performance Optimization
    
4)Difference between collections and collection?
1. Collection (Interface)
Type: Interface in java.util package.
Role: Root interface of the Collections Framework.
Purpose: Defines the basic operations for working with a group of objects (like add(), remove(), size()).
Implemented by: List, Set, Queue interfaces.
 2. Collections (Utility Class)

Type: Final class in java.util package.
Role: Provides static utility methods to operate on collections.
Purpose: Helps with tasks like sorting, searching, synchronization.
Common Methods:

Collections.sort(list)
Collections.reverse(list)
Collections.synchronizedList(list)

5) when to use LinkedList and ArrayList?

   
 ArrayList
Best for:
Frequent random access (get by index).
When you mostly read data and occasionally add/remove at the end.
Why:
Backed by a dynamic array, so get(index) is O(1).
Adding at the end is usually O(1) (amortized).
Avoid:
Frequent insertions/removals in the middle or beginning (costly because elements need shifting).
✅ LinkedList
Best for:
Frequent insertions/removals anywhere in the list (especially at the start or middle).
When you need a Queue or Deque (it implements both).
Why:
Backed by a doubly linked list, so adding/removing nodes is O(1) if you have the reference.
Avoid:
Random access by index (get(index) is O(n) because it must traverse nodes).


6)Difference between List and Set?
✅ 1. Ordering
List:
Maintains insertion order.
Elements can be accessed by index.
Set:
Does not guarantee order (except LinkedHashSet or TreeSet which provide specific ordering).
✅ 2. Duplicates
List:
Allows duplicates.
Example: [A, B, A] is valid.
Set:
Does NOT allow duplicates.
Example: {A, B} only.
✅ 3. Access
List:
Provides indexed access (get(index)).
Set:
No index-based access; you iterate using Iterator or enhanced for.
✅ 4. Implementations
List:
ArrayList, LinkedList, Vector.
Set:
HashSet, LinkedHashSet, TreeSet.

7)Difference between ArrayList and Vector?

Key Differences
1) Thread-safety

ArrayList: Not synchronized (not thread-safe by default).
You can make it thread-safe with Collections.synchronizedList(list) or use CopyOnWriteArrayList depending on your read/write pattern.
Vector: Synchronized—all public methods are synchronized, making it thread-safe but slower under contention.

2) Performance

ArrayList: Faster in single-threaded contexts due to no synchronization overhead.
Vector: Slower because of method-level synchronization even when you don’t need it.

3) Growth Policy

ArrayList: Grows by ~1.5x when capacity is exceeded (implementation detail but typical in OpenJDK).
Vector: Traditionally grows by 2x, or by a custom capacityIncrement if set.
This can cause more memory churn or over-allocation.

4) API & Legacy

ArrayList: Modern, commonly used; pairs well with List interface.
Vector: Legacy class (kept for backward compatibility). Also exposes Enumeration (e.g., elements()), which is largely superseded by Iterator.

5) Iterators & Fail-Fast

ArrayList: Iterators are fail-fast—concurrent structural modification throws ConcurrentModificationException.
Vector: Same fail-fast behavior for Iterator and ListIterator.
But Enumeration from Vector.elements() is not fail-fast (it won’t detect concurrent modifications).

6) Usage as List

Both back a contiguous array underneath and have O(1) average get(index) and set(index), and amortized O(1) appends.
Insertions/removals in the middle are O(n) for both due to shifting.


When to Use Which?
Choose ArrayList when:

You’re writing new code.
Performance matters and you don’t need built-in synchronization.
You want control over synchronization (e.g., via Collections.synchronizedList or better, java.util.concurrent classes).

Choose Vector when:

You’re maintaining legacy code that already returns/consumes Vector or Enumeration.
You specifically require method-level synchronization and cannot refactor to better concurrency primitives.

8)Differance between HashSet and TreeSet?
✅ 1. Ordering

HashSet:

No guaranteed order of elements.
Uses hashing internally.


TreeSet:

Sorted order (natural ordering or custom Comparator).
Uses Red-Black Tree internally.




✅ 2. Performance
OperationHashSet (Average)TreeSetAdd / RemoveO(1)O(log n)SearchO(1)O(log n)

✅ 3. Null Elements

HashSet: Allows one null element.
TreeSet: Does NOT allow null (throws NullPointerException).


✅ 4. Underlying Structure

HashSet: Backed by a HashMap.
TreeSet: Backed by a NavigableMap (usually TreeMap).

9)HashSet internal implementation?
Backed by HashMap

A HashSet internally uses a HashMap to store its elements.
Each element in the HashSet is stored as a key in the HashMap.
The value for each key is a constant dummy object (PRESENT).



Hashing Mechanism

When you add an element, HashSet computes its hash code using hashCode() and determines the bucket in the hash table.
If two elements have the same hash code, they go into the same bucket (collision handled by linked list or tree in HashMap).



Duplicate Handling

Before inserting, HashSet checks if the key already exists in the underlying HashMap.
If yes, it ignores the new element (ensuring uniqueness).
Load Factor & Capacity
Default initial capacity: 16
Default load factor: 0.75
When size exceeds capacity × loadFactor, the HashMap resizes (rehashes).

Performance

Average time complexity for add(), remove(), contains() is O(1).
Worst case (hash collisions): O(n).

10)Hashset vs HashTable?(key value pairs, syncronization)
11)HashMap vs TreeMap?
✅ 1. Purpose

Both implement the Map interface and store key-value pairs.
Both ensure unique keys.


✅ 2. Ordering

HashMap:

No guaranteed order of keys.
Keys are arranged based on hash codes.


TreeMap:

Maintains sorted order of keys (natural ordering or custom Comparator).




✅ 3. Performance




















OperationHashMap (Average)TreeMapInsert / RemoveO(1)O(log n)SearchO(1)O(log n)

✅ 4. Null Handling

HashMap:

Allows one null key and multiple null values.


TreeMap:

Does NOT allow null key (throws NullPointerException).
Allows null values.




✅ 5. Underlying Structure

HashMap: Backed by hash table.
TreeMap: Backed by a Red-Black Tree (self-balancing binary search tree).


✅ 6. Thread Safety

Neither is synchronized by default.
Use Collections.synchronizedMap() or ConcurrentHashMap for thread safety.


✅ 7. Use Cases

HashMap:

When you need fast lookups and don’t care about order.


TreeMap:

When you need sorted keys or range queries (e.g., headMap(), tailMap()).

11) Hashmap rehashing?
HashMap uses an array of buckets internally.
Each bucket stores entries (key-value pairs) based on their hash code.
When the number of entries exceeds capacity × loadFactor, the map resizes to maintain performance.

Default capacity: 16
Default load factor: 0.75
Threshold: capacity × loadFactor (e.g., 16 × 0.75 = 12)




✅ What Happens During Rehashing

New Capacity

The bucket array size is doubled (e.g., 16 → 32).


Recompute Index

Each existing entry is rehashed to compute its new bucket index:
Javaindex = hash(key) & (newCapacity - 1);Show more lines



Redistribute Entries

All entries are moved to the new bucket array based on the new index.

Performance Impact
Rehashing is expensive because it involves iterating over all entries and recalculating positions.

✅ HashMap Internal Behavior

In Java 8+, if a bucket becomes too large (due to collisions), it converts the linked list into a balanced tree (Red-Black Tree) for faster lookups.
After resizing, tree nodes may revert to linked lists if the bucket size drops below a threshold.

12) FailFirst fail safe collections? 
13) comparable vs comparator?
14) concurent Hashmap ?
15)coursers in collections?







 





