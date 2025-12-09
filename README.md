
---

# ✅ **Java Stream API Methods (Cheat Sheet)**

## **1. Creating Streams**

| Method                        | Description                                    |
| ----------------------------- | ---------------------------------------------- |
| `Collection.stream()`         | Creates a sequential stream from a collection. |
| `Collection.parallelStream()` | Creates a parallel stream.                     |
| `Stream.of(T...)`             | Creates a stream from given elements.          |
| `Stream.ofNullable(T)`        | Creates a stream with 0 or 1 elements.         |
| `Stream.generate(Supplier)`   | Produces infinite stream.                      |
| `Stream.iterate(seed, f)`     | Infinite stream of iterative elements.         |
| `Arrays.stream(array)`        | Stream from array.                             |
| `Files.lines(path)`           | Stream of lines from a file.                   |

---

## **2. Intermediate Operations (return Stream)**

These are **lazy** — they don’t run until a terminal operation is called.

### **Filtering**

* `filter(Predicate)`
* `distinct()`
* `limit(long)`
* `skip(long)`
* `takeWhile(Predicate)` *(Java 9+)*
* `dropWhile(Predicate)` *(Java 9+)*

### **Mapping**

* `map(Function)`
* `mapToInt(ToIntFunction)`
* `mapToLong(ToLongFunction)`
* `mapToDouble(ToDoubleFunction)`
* `flatMap(Function)`
* `flatMapToInt(...)`, etc.

### **Sorting**

* `sorted()`
* `sorted(Comparator)`

### **Peeking**

* `peek(Consumer)` (for debugging)

---

## **3. Terminal Operations (produce non-stream result)**

These actually trigger stream processing.

### **Matching**

| Method                 | Returns | Description           |
| ---------------------- | ------- | --------------------- |
| `anyMatch(Predicate)`  | boolean | At least one matches  |
| `allMatch(Predicate)`  | boolean | Every element matches |
| `noneMatch(Predicate)` | boolean | No elements match     |

### **Finding Elements**

* `findFirst()`
* `findAny()` (useful in parallel streams)

### **Reducers**

| Method                                    | Description |
| ----------------------------------------- | ----------- |
| `reduce(identity, accumulator)`           |             |
| `reduce(accumulator)`                     |             |
| `reduce(identity, accumulator, combiner)` |             |

### **Collecting**

* `collect(Collector)`
  Examples:

  * `Collectors.toList()`
  * `Collectors.toSet()`
  * `Collectors.toMap()`
  * `Collectors.groupingBy()`
  * `Collectors.partitioningBy()`
  * `Collectors.joining()`

### **Iteration**

* `forEach(Consumer)`
* `forEachOrdered(Consumer)`

### **Stats**

* `count()`
* `max(Comparator)`
* `min(Comparator)`

### **Conversions**

* `toArray()`

---

## **4. Primitive Streams**

### **IntStream, LongStream, DoubleStream**

Methods specific to primitive streams:

* `sum()`
* `average()`
* `range(start, end)`
* `rangeClosed(start, end)`
* `boxed()`
* `summaryStatistics()`

---

## **5. Short Examples**

### **Filter + Map + Collect**

```java
List<String> result = list.stream()
    .filter(s -> s.length() > 3)
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

### **Find max**

```java
Optional<Integer> max = numbers.stream().max(Integer::compareTo);
```

### **Group by field**

```java
Map<String, List<Person>> peopleByCity =
    people.stream().collect(Collectors.groupingBy(Person::getCity));
```

---

# ✅ **What is `reduce()` in Java Streams?**

`reduce()` is a **terminal operation** that **combines all elements of a stream into a single value**.

It repeatedly applies an **accumulator function** to produce one result.

---

# ✅ **3 Method Signatures**

### **1️⃣ Optional<T> reduce(BinaryOperator<T> accumulator)**

No identity → may return empty.

```java
Optional<Integer> sum = list.stream()
                            .reduce((a, b) -> a + b);
```

---

### **2️⃣ T reduce(T identity, BinaryOperator<T> accumulator)**

Identity → starting value.

```java
int sum = list.stream()
              .reduce(0, (a, b) -> a + b);
```

💡 Identity makes the result **non-Optional**.

---

### **3️⃣ <U> U reduce(U identity,

BiFunction<U, ? super T, U> accumulator,
BinaryOperator<U> combiner)**
Used for **parallel streams**.

```java
int length = words.stream()
                  .reduce(0,
                          (total, word) -> total + word.length(),
                          Integer::sum);
```

---

# 🔥 How `reduce()` Works (Diagram)

For a stream: **[1, 2, 3, 4]**

### With identity = 0

```
accumulator(0, 1) → 1
accumulator(1, 2) → 3
accumulator(3, 3) → 6
accumulator(6, 4) → 10
```

Final result = **10**

---

# 🎯 When to Use reduce()

Use `reduce()` when you want **one final value**, such as:

* sum, min, max
* string concatenation
* product of numbers
* combining objects

---

# ✅ **Top Interview Examples**

---

## **1️⃣ Sum of Numbers**

```java
int sum = Arrays.asList(1,2,3,4)
                 .stream()
                 .reduce(0, Integer::sum);
```

---

## **2️⃣ Maximum Value**

```java
Optional<Integer> max = nums.stream()
                            .reduce(Integer::max);
```

---

## **3️⃣ Multiply All Numbers**

```java
int product = nums.stream()
                  .reduce(1, (a, b) -> a * b);
```

---

## **4️⃣ Concatenate Strings**

```java
List<String> names = List.of("A", "B", "C");

String result = names.stream()
                     .reduce("", (a, b) -> a + b);
```

---

## **5️⃣ Count Characters in All Strings**

```java
int charCount = words.stream()
                     .reduce(0,
                             (sum, word) -> sum + word.length(),
                             Integer::sum);
```

---

## **6️⃣ Sum of Salaries (map + reduce)**

```java
double total = employees.stream()
                        .map(Employee::getSalary)
                        .reduce(0.0, Double::sum);
```

---

## **7️⃣ Reduce to Custom Object**

```java
int totalAge = persons.stream()
                      .reduce(0,
                              (sum, p) -> sum + p.getAge(),
                              Integer::sum);
```

---

## **8️⃣ Reduce With No Identity**

```java
Optional<Integer> sum = nums.stream()
                            .reduce((a, b) -> a + b);
```

---

## **9️⃣ Reduce to find Min**

```java
int min = nums.stream()
              .reduce(Integer.MAX_VALUE, Integer::min);
```

---

## **🔟 Build a Frequency Map Using reduce()**

(Not recommended — just for understanding)

```java
Map<Character, Integer> freq =
    chars.stream()
         .reduce(new HashMap<Character, Integer>(),
             (map, c) -> {
                 map.put(c, map.getOrDefault(c, 0) + 1);
                 return map;
             },
             (map1, map2) -> {
                 map1.putAll(map2);
                 return map1;
             });
```

---

# 🚫 When **NOT** to Use reduce()

❌ Avoid `reduce()` when combining into a **mutable container** (like List, Map).
Use **Collectors.toList()**, **toMap()**, or **groupingBy()** instead.

---

# ⭐ reduce() vs collect()

| Feature         | reduce()                             | collect()                                 |
| --------------- | ------------------------------------ | ----------------------------------------- |
| Purpose         | Combine into single immutable result | Build mutable containers (List, Map, Set) |
| Mutable?        | ❌ No                                 | ✔ Yes                                     |
| Recommended for | sum, max, product                    | grouping, partition, list/map creation    |

---

# Want more?

I can give:

✅ reduce() tricky interview questions
✅ reduce() vs map/filter detailed comparison
✅ custom reduce example for your Spring Boot project

Just tell me!

---

# ✅ **Why static methods cannot be overridden?**

Static methods belong to the **class**, not to the object.

Overriding works only on **instance methods (object methods)** using **dynamic binding (runtime polymorphism)**.

Static methods use **compile-time binding**, so Java does **not** support overriding for them.

---

# 🟥 **Example (Static Method Hiding)**

```java
class Parent {
    static void show() {
        System.out.println("Parent show");
    }
}

class Child extends Parent {
    static void show() {
        System.out.println("Child show");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.show(); // Output: Parent show (not Child)
    }
}
```

### ✔ Why output is *Parent show*?

Because static methods use **class reference**, not object type.

So:

* `p` is of type `Parent`
* So `Parent.show()` is called.

This proves **static methods are not overridden**, only **hidden**.

---

# 🟩 **Interview-perfect answer**

> **No, static methods cannot be overridden in Java.**
> If a subclass declares a static method with the same signature, it is called *method hiding*, not overriding.
> Overriding requires runtime polymorphism, but static methods are resolved at compile time.

---
# Converting ArrayList to Array in Java

There are several ways to convert an ArrayList to an array in Java. Here are the most common methods:

## 1. Using `toArray()` without parameter

```java
ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Orange");

// Convert to Object array
Object[] array = list.toArray();
```

## 2. Using `toArray(T[] a)` with parameter (recommended)

This is the preferred way as it provides type safety:

```java
ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Orange");

// Convert to String array
String[] array = list.toArray(new String[0]);

// Alternative: Provide array of correct size
String[] array = list.toArray(new String[list.size()]);
```

## 3. Using Java 8 Streams

```java
ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Orange");

String[] array = list.stream().toArray(String[]::new);
```

## Important Notes:
- The parameterless `toArray()` returns an Object array
- The version with parameter returns an array of the specified type
- When using `toArray(T[] a)`, if the array is large enough, it will be used; otherwise a new array will be created
- For primitive types (int, double, etc.), you'll need to manually convert as ArrayList can only hold objects

## Example with Primitive Types

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

// Convert to int array
int[] intArray = list.stream().mapToInt(i -> i).toArray();
```

The method you choose depends on your specific requirements and Java version you're using.
---

Here's a detailed comparison between HashMap and ConcurrentHashMap:

## HashMap
- **Not thread-safe** - Cannot be safely used by multiple threads concurrently
- **Synchronization** - Requires external synchronization for thread-safe operations
- **Performance** - Faster in single-threaded environments
- **Null keys/values** - Allows one null key and multiple null values
- **Fail-fast iterator** - Throws `ConcurrentModificationException` if modified during iteration

## ConcurrentHashMap
- **Thread-safe** - Designed for concurrent access by multiple threads
- **Synchronization** - Uses internal locking mechanisms (segment-level or node-level locking)
- **Performance** - Better performance than synchronized HashMap in high-concurrency scenarios
- **Null restrictions** - Does not allow null keys or values
- **Weakly consistent iterator** - Does not throw ConcurrentModificationException

## Key Differences

| Aspect | HashMap | ConcurrentHashMap |
|--------|---------|-------------------|
| **Thread Safety** | No | Yes |
| **Synchronization** | External needed | Built-in |
| **Performance** | Better single-threaded | Better multi-threaded |
| **Null Support** | Allows null | No null allowed |
| **Iterator Behavior** | Fail-fast | Weakly consistent |
| **Locking Mechanism** | N/A | Segment/node locking |

## Code Examples

### HashMap (Not Thread-Safe)
```java
Map<String, Integer> hashMap = new HashMap<>();

// Requires external synchronization for thread safety
synchronized(hashMap) {
    hashMap.put("key", 1);
    Integer value = hashMap.get("key");
}
```

### ConcurrentHashMap (Thread-Safe)
```java
ConcurrentMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();

// No external synchronization needed
concurrentMap.put("key", 1);
Integer value = concurrentMap.get("key");

// Atomic operations
concurrentMap.putIfAbsent("key", 2);
concurrentMap.computeIfAbsent("newKey", k -> 42);
```

## When to Use Which

**Use HashMap when:**
- Single-threaded environment
- Performance is critical
- You can manage synchronization externally

**Use ConcurrentHashMap when:**
- Multiple threads will access the map
- High concurrency is expected
- You need atomic operations
- Better performance than synchronized HashMap in concurrent scenarios

## Performance Characteristics
- **HashMap**: O(1) average case for get/put operations
- **ConcurrentHashMap**: Nearly O(1) with minimal contention between threads

ConcurrentHashMap provides better scalability than synchronized HashMap because it allows multiple threads to read and a limited number of threads to write concurrently without blocking each other completely.
