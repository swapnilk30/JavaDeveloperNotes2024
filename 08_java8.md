Below are **clean, interview-ready notes** covering **frequency counting using Java Stream API** for **Lists and primitive arrays**.
These notes are structured the way interviewers expect explanations.

---

# Frequency Counting Using Java Stream API

### (List & Primitive Array – Interview Notes)

---

## 1. Frequency Count Using `List<T>`

### Standard & Recommended Approach

```java
Map<T, Long> freqMap =
    list.stream()
        .collect(Collectors.groupingBy(
            Function.identity(),
            Collectors.counting()
        ));
```

### Key Interview Points

* `groupingBy()` groups identical elements
* `Function.identity()` returns the element itself as the key
* `counting()` counts occurrences per group
* Output value type is always `Long`
* Works for any object with proper `equals()` and `hashCode()`

### Example

```java
List<Integer> list = Arrays.asList(1,2,2,3,3,3);
```

**Result**

```text
{1=1, 2=2, 3=3}
```

---

## 2. Using `toMap()` for Frequency Count

```java
Map<T, Long> freqMap =
    list.stream()
        .collect(Collectors.toMap(
            e -> e,
            e -> 1L,
            Long::sum
        ));
```

### Interview Notes

* Third argument (`merge function`) resolves duplicate keys
* `Long::sum` adds existing and new values
* More control, but **less readable** than `groupingBy`
* Commonly asked as an alternative solution

---

## 3. Frequency Count in `int[]` (Primitive Array)

### Stream API Solution

```java
int[] arr = {1,2,2,3,3,3};

Map<Integer, Long> freqMap =
    Arrays.stream(arr)   // IntStream
          .boxed()       // Stream<Integer>
          .collect(Collectors.groupingBy(
              Function.identity(),
              Collectors.counting()
          ));
```

### Important Interview Notes

* `Arrays.stream(int[])` → returns `IntStream`
* `boxed()` converts primitive `int` to wrapper `Integer`
* Boxing is required because `Map` works with objects
* Slight performance overhead due to boxing

---

## 4. Frequency Count in `char[]`

```java
char[] chars = {'a','b','a','c','b'};

Map<Character, Long> freqMap =
    IntStream.range(0, chars.length)
             .mapToObj(i -> chars[i])
             .collect(Collectors.groupingBy(
                 Function.identity(),
                 Collectors.counting()
             ));
```

### Interview Notes

* No direct `CharStream` in Java
* Use `IntStream.range()` for index-based access
* Convert `char` to `Character` for map keys

---

## 5. Frequency Count of Characters in a `String`

```java
String str = "banana";

Map<Character, Long> freqMap =
    str.chars()                 // IntStream
       .mapToObj(c -> (char) c)
       .collect(Collectors.groupingBy(
           Function.identity(),
           Collectors.counting()
       ));
```

### Interview Notes

* `chars()` returns ASCII values (`int`)
* Explicit cast to `char` is mandatory
* Frequently asked question in interviews

---

## 6. Sorted Frequency Map (Descending Order)

```java
Map<T, Long> sortedMap =
    freqMap.entrySet()
           .stream()
           .sorted(Map.Entry.<T, Long>comparingByValue().reversed())
           .collect(Collectors.toMap(
               Map.Entry::getKey,
               Map.Entry::getValue,
               (a, b) -> a,
               LinkedHashMap::new
           ));
```

### Interview Notes

* `LinkedHashMap` preserves insertion order
* Sorting is done on `entrySet()`
* Common follow-up question

---

## 7. High-Performance Approach (Without Streams)

```java
int[] arr = {1,2,2,3,3,3};
int[] freq = new int[10];

for (int n : arr) {
    freq[n]++;
}
```

### Interview Notes

* Best performance (no boxing)
* Less flexible
* Use when:

  * Input size is huge
  * Range of values is small
* Good to mention in **optimization discussions**

---

## 8. Common Interview Traps ⚠️

| Trap                                   | Explanation                            |
| -------------------------------------- | -------------------------------------- |
| Using `int` instead of `Long`          | `Collectors.counting()` returns `Long` |
| Forgetting merge function in `toMap()` | Causes `IllegalStateException`         |
| Not boxing primitive streams           | Maps cannot hold primitives            |
| Ignoring `equals()` / `hashCode()`     | Leads to incorrect grouping            |

---

## 9. When to Use What?

| Scenario             | Best Choice               |
| -------------------- | ------------------------- |
| Readability          | `groupingBy + counting()` |
| Custom merge logic   | `toMap()`                 |
| Primitive array      | `Arrays.stream().boxed()` |
| Character frequency  | `str.chars()`             |
| Performance critical | Plain array / loop        |

---

## 10. One-Line Interview Answer (Very Important)

> “To count frequency using Java Streams, we use `Collectors.groupingBy()` with `Collectors.counting()`. For primitive arrays, we first convert them into boxed streams before grouping.”

---

If you want, I can also provide:

* **30 interview Q&A**
* **Real-time coding problems**
* **Time & space complexity explanations**
* **Java 8 vs Java 17 comparison**

Just tell me 😊




```
Java Streams (Stream API in Java)
https://www.youtube.com/playlist?list=PLUDwpEzHYYLvTPVqVIt7tlBohABLo4gyg
```

```
21. What are new features of java 8 ?
22. What is Lambda expression in Java 8 ?
23. What is metaspace in java 8 ?
24. What is use of functional interface in Java 8 ?
25. In which scenario you will use parallel stream in java 8 ?
26. Have you used parallel streams as well ?
27. How does lambda expression relates to functional interfaces ?
```

```
Predefined Functional Interfaces  :

    Predicate 
    Function
    Consumer
    Supplier
```

# What is Lambda Expression (λ):

### The Main Objective of Lambda Expression is to bring benefits of functional programming into Java.
    • Lambda Expression is just an anonymous (nameless) function. That means the function which
    doesn’t have the name, return type and access modifiers.
    • Lambda Expression also known as anonymous functions or closures.

# Stream API
- to process the data from collection we use streams concepts.

## What is an Intermediate operation
- The Operations which return another stream as a result are called intermediate operations.
- filter(), map(), distinct(), sorted(), limit(), skip()

```
- The filter() method in the Stream API of Java is used to filter elements of a stream based on a given predicate.
- This method returns a new stream that consists of elements that match the predicate.

Stream<T> filter(Predicate<? super T> predicate)

// Example :
List<String> names = List.of("Alice", "Bob", "Charlie", "David", "Eve");

// Create a stream: 
Stream<String> nameStream = names.stream();

//Apply the filter() method:
Stream<String> filteredStream = nameStream.filter(name -> name.startsWith("A"));

- The filter() method takes a Predicate as an argument.
- A Predicate is a functional interface that has a method boolean test(T t) which returns true or false.

// Collect or process the filtered elements:
List<String> filteredNames = filteredStream.collect(Collectors.toList());

```

## distinct() - filters out duplicate elements from the stream.
```java
public class DistinctEx {
	
	public static void main(String[] args) {
		
		int[] arr = {3,7,4,6,2,5,1,4,6,2,5};
		
		List<Integer> list = Arrays.asList(3,5,4,6,2,5,6,8,9);
		
		List<String> fruits = Arrays.asList("Banana","Orange","Mango","Kiwi","Apple","Orange","Mango");
		
		// To get the distinct elements as an array
		
		int[] distinctArray = Arrays.stream(arr).distinct().toArray();
		
		System.out.println(Arrays.toString(distinctArray));
		
		//
		List<Integer> diList = list.stream().distinct().collect(Collectors.toList());
		
		System.out.println(diList);
		
		//
		List<String> distinctList = fruits.stream().distinct().collect(Collectors.toList());
		
		System.out.println(distinctList);
	}
}

```

### Wap to print 1 to 100 numbers using Stream Api

```java
public class PrintOneToHundread {

	public static void main(String[] args) {
	
		// Wap to print 1 to 100 numbers using Stream Api
		
		IntStream.range(1, 101).forEach(x->System.out.println(x));
		
	}
}

```
### Wap to sum of list using java 8
```java
public class SumExample {
	
	public static void main(String[] args) {
		
		int[] arr = {3,7,1,4,6,2,5};
		
		int sum = Arrays.stream(arr).sum();
		
		System.out.println(sum);
		
		List<Integer> list = Arrays.asList(3,7,1,4,6,2,5);
		
		// Using IntStream sum method
		int sum2 = list.stream().mapToInt(Integer::intValue).sum();
		
		System.out.println(sum2);
		
		// Using Stream API with reduce method
		int sum3 = list.stream().reduce(0,Integer::sum);
		
		System.out.println(sum3);
		
		// Using Collectors.summingInt
		int sum4 = list.stream().collect(Collectors.summingInt(Integer::intValue));	
	}
}
```

### Wap to get Min and Max element
    int[] arr = {3,7,1,4,6,2,5};


```java
public class MinMax{

    public static void main(String[] args){
        
        int[] arr = {3,7,1,4,6,2,5};

        int min = Arrays.stream(arr).min().getAsInt();

        System.out.println(min);

        int max = Arrays.stream(arr).max().getAsInt();

        System.out.println(max);
    }
}
```


### Write a java program to find sum of even numbers and sum of odd numbers in a given list using java 8 streams.
    List<Integer> list = Arrays.asList(3,5,6,8,9);

```java
public class SumOfEvenOdd {
	
	public static void main(String[] args) {
		List<Integer> list = Arrays.asList(3,5,6,8,9);
		
		//filter even numbers and add to list
		List<Integer> listOfEvenNum = list.stream().filter(n -> n % 2 ==0 ).collect(Collectors.toList());
		System.out.println(listOfEvenNum);
		
		int sumOfEvenNumbers = list.stream().filter(n->n%2==0).mapToInt(Integer::intValue).sum();

		System.out.println(sumOfEvenNumbers);
		
		//filter Odd numbers and add to list
		List<Integer> listOfOddNum = list.stream().filter(n->n%2 == 1).collect(Collectors.toList());
		
		System.out.println(listOfOddNum);
		
		int sumOfOddNumbers = list.stream().filter(n->n%2==1).mapToInt(Integer::intValue).sum();
	
		System.out.println(sumOfOddNumbers);
	}
}
```

### find out all the numbers starting with 1 in a list by using Stream API ?
```java
    List<Integer> list = Arrays.asList(20,15,80,11,48,25,98,32,17);

    list.stream().map(s -> s.toString()).filter(s -> s.startsWith("1")).forEach(System.out::println);
```

## Find the second largest number in a list of integers using stream ?
```java
public class SecondHighestNumber {
	
	public static void main(String[] args) {
		
		List<Integer> list = Arrays.asList(1,1,1,2,4,3,4,6,7,8,0,9,3,21,1);
		
		//Find the second largest number of a list
		
		Optional<Integer> findFirst = list.stream().distinct().sorted(Comparator.reverseOrder()).skip(1).findFirst();
		
		Integer integer = findFirst.get();
		
		System.out.println(integer);
		
	}
}
```


# JAVA 8 STREAM API
## Sort List in Ascending and Descending Order


```
List<Integer> numbers = Arrays.asList(1,2,3,1,1,1,1,2,3,9,7,6,5,4,3,-1,-4,0);

List<String> fruits = Arrays.asList("Banana","Orange","Mango","Kiwi","Apple");
```
### Sorting List of String objects in Ascending order using Stream Api
```java

List<String> sortedAsc = fruits.stream().sorted().collect(Collectors.toList());

List<String> sortedAsc = fruits.stream().sorted(Comparator.naturalOrder()).collect(Collectors.toList());

List<String> sortedAsc = fruits.stream().sorted((o1,o2)->o1.compareTo(o2)).collect(Collectors.toList());

```
### Sorting List of String objects in Descending order using Stream Api
```java
List<String> sortedDesc = fruits.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toList());

List<String> sortedDesc = fruits.stream().sorted((o1,o2)->o2.compareTo(o1)).collect(Collectors.toList());
```


```java


class Employee{

    private int id;
    private String name;
    private int age;
    private long salary;

    // getter and setter
    // default and parameterized Constructor
    // toString

}

		List<Employee> employees = Arrays.asList(
				new Employee(10, "Ramesh", 29, 45000),
				new Employee(20, "Suresh", 30, 55000),
				new Employee(30, "Bhushan", 28, 38000),
				new Employee(40, "Swapnil", 32, 54000),
				new Employee(50, "Ramesh", 29, 38000));

```
### Sorting List of Employee objects (By Salary) in Ascending order using Stream Api
```java
List<Employee> sortedAsc = employees.stream().sorted(Comparator.comparingLong(Employee::getSalary)).collect(Collectors.toList());

List<Employee> sortedAsc = employees.stream().sorted((o1,o2)->(int)(o1.getSalary()-o2.getSalary())).collect(Collectors.toList());
```
### Sorting List of Employee objects (By Salary) in Descending order using Stream Api
```java

List<Employee> sortedDesc = employees.stream().sorted(Comparator.comparingLong(Employee::getSalary).reversed()).collect(Collectors.toList());

List<Employee> sortedAsc = employees.stream().sorted((o1,o2)->(int)(o2.getSalary()-o1.getSalary())).collect(Collectors.toList());
		
```

### Sorting List of Employee objects (By Age) in Ascending order using Stream Api
### Sorting List of Employee objects (By Age) in Descending order using Stream Api


### Sorting List of Employee objects (By Name) in Ascending order using Stream Api
### Sorting List of Employee objects (By Name) in Descending order using Stream Api

```
https://www.youtube.com/watch?v=BIQvBe0KYKI

```


```
Features of Java 8
What is the Use Of Optional Class in java
```


# What is the Optional class in Java 8?
- The Optional class in Java 8 is a container object that may or may not contain a value.
- **It is used to avoid null pointer exceptions.**
- If a value is present, isPresent() will return true.
- get() will return the value otherwise throws **NoSuchElementException**.

```java
/*you might encounter a Null Pointer Exception when you try to invoke a method or access a field on a variable that is null.
 Null Pointer Exceptions can be common sources of bugs in programs,
 especially if proper null checks are not performed before accessing object references.
*/
public class OptionalExample {
	
	public static void main(String[] args) {
		
		String str = null;
		int length = str.length(); // This line will throw a NullPointerException
	}
}

// To Handle Above NullPointerException we have to Check null using if else 

public class OptionalExample {
	
	public static void main(String[] args) {
		
		String str = null;
		//int length = str.length(); // This line will throw a NullPointerException
	
		if(str == null) {
			System.out.println("this is null object");
		}else {
			System.out.println(str.length());
		}
	}
}
```
#### Handle Using Optional Class
```java
public class OptionalExample {
	
	public static void main(String[] args) {
		
		String str = null;
		//int length = str.length(); // This line will throw a NullPointerException
		
		Optional<String> optional = Optional.ofNullable(str);
		
		System.out.println(optional.isPresent());// false
		
		//System.out.println(optional.get());// Exception in thread "main" java.util.NoSuchElementException: No value present
		
		System.out.println(optional.orElse("No value present"));
	}
}
```

```java
// Example : Used in project 

@Repository
public interface UserRepository extends JpaRepository<User, String>{

	Optional<User> findByEmail(String username);

}


{
	User user = userRepository.findById(userId).orElseThrow(()-> new ResourceNotFoundException("User not found by Given Id !!"));
}
```



### Given two integer arrays firstArray and secondArray,return an array of their intersection using java 8.
	each element in result must be unique and you may return the result in any array
	Example : int firstArray={4,9,5};
		int secondArray[]={9,4,9,8,4};
		output : [9,4]
```java
public class IntersectionOfTwoArrays {

	public static void main(String[] args) {

		int firstArray[]= {4,9,5};
		int secondArray[]= {9,4,9,8,4};
		
		Arrays.stream(firstArray).filter(x->Arrays.stream(secondArray)
				.anyMatch(y->y==x))
					.distinct().forEach(System.out::println);
	}
}

```

## find highest salary of an employee from each department
- https://www.youtube.com/watch?v=okPecNk797Y
## find the average salary of each department using java 8 Stream API?
## Find Nth Highest Salary Using Java Streams API | unique and duplicate records
- https://www.youtube.com/watch?v=X80i0QHRByQ




```
Collect()
Collectors.toList()
Collectors.joining()
```
Below are **clean, structured interview notes + code examples** for **Java 8 Stream API** covering **salary problems** and **collect / collectors usage**.
This is **very common in interviews**.

---

# Java 8 Stream API – Interview Notes & Examples

We’ll use this **Employee class** for all examples:

```java
class Employee {
    int id;
    String name;
    String department;
    double salary;

    // constructor + getters
    public Employee(int id, String name, String department, double salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public String getDepartment() { return department; }
    public double getSalary() { return salary; }
    public String getName() { return name; }
}
```

Sample Data:

```java
List<Employee> employees = List.of(
    new Employee(1, "A", "IT", 80000),
    new Employee(2, "B", "IT", 90000),
    new Employee(3, "C", "HR", 70000),
    new Employee(4, "D", "HR", 75000),
    new Employee(5, "E", "Finance", 85000)
);
```

---

## 1. Highest Salary of Employee from Each Department

### ✅ Recommended Approach

```java
Map<String, Optional<Employee>> highestSalaryByDept =
    employees.stream()
             .collect(Collectors.groupingBy(
                 Employee::getDepartment,
                 Collectors.maxBy(
                     Comparator.comparingDouble(Employee::getSalary)
                 )
             ));
```

### Simplified (Salary Only)

```java
Map<String, Double> highestSalaryByDept =
    employees.stream()
             .collect(Collectors.groupingBy(
                 Employee::getDepartment,
                 Collectors.collectingAndThen(
                     Collectors.maxBy(Comparator.comparingDouble(Employee::getSalary)),
                     emp -> emp.get().getSalary()
                 )
             ));
```

### Interview Notes

* `groupingBy()` → department-wise grouping
* `maxBy()` → finds max element per group
* Result is wrapped in `Optional`

---

## 2. Average Salary of Each Department

```java
Map<String, Double> avgSalaryByDept =
    employees.stream()
             .collect(Collectors.groupingBy(
                 Employee::getDepartment,
                 Collectors.averagingDouble(Employee::getSalary)
             ));
```

### Interview Notes

* `averagingDouble()` returns `Double`
* Handles division internally
* No need for manual sum/count

---

## 3. Find Nth Highest Salary (Unique Records)

### Example: 2nd Highest Salary

```java
int n = 2;

Optional<Double> nthHighestSalary =
    employees.stream()
             .map(Employee::getSalary)
             .distinct()
             .sorted(Comparator.reverseOrder())
             .skip(n - 1)
             .findFirst();
```

### Interview Notes

* `distinct()` removes duplicates
* `skip(n-1)` skips higher salaries
* `findFirst()` returns `Optional`

---

## 4. Nth Highest Salary (With Duplicate Records)

```java
int n = 2;

Optional<Double> nthHighestSalary =
    employees.stream()
             .map(Employee::getSalary)
             .sorted(Comparator.reverseOrder())
             .skip(n - 1)
             .findFirst();
```

### Difference (Very Important)

| Case                       | Use `distinct()` |
| -------------------------- | ---------------- |
| Unique salaries            | ✅ Yes            |
| Duplicate salaries allowed | ❌ No             |

---

## 5. `collect()` Method – Core Concept

```java
<R, A> R collect(Collector<? super T, A, R> collector)
```

### Purpose

* Converts a stream into:

  * List
  * Set
  * Map
  * String
  * Custom structure

---

## 6. `Collectors.toList()`

```java
List<String> names =
    employees.stream()
             .map(Employee::getName)
             .collect(Collectors.toList());
```

### Interview Notes

* Returns a **mutable list**
* Order is preserved
* Java 16+: `toList()` returns immutable list

---

## 7. `Collectors.joining()`

### Join Names with Comma

```java
String employeeNames =
    employees.stream()
             .map(Employee::getName)
             .collect(Collectors.joining(", "));
```

### Prefix & Suffix

```java
String result =
    employees.stream()
             .map(Employee::getName)
             .collect(Collectors.joining(", ", "[", "]"));
```

**Output**

```text
[A, B, C, D, E]
```

### Interview Notes

* Works only on `Stream<String>`
* Internally uses `StringBuilder`
* Very common string-related interview question

---

## 8. One-Line Interview Answers 🔑

> **Highest salary by department:**
> Use `groupingBy()` with `maxBy()`.

> **Average salary:**
> Use `Collectors.averagingDouble()`.

> **Nth highest salary:**
> Sort in descending order, skip `n-1`, and fetch first.

> **joining():**
> Converts stream of strings into a single string with delimiter.

---

## 9. Time & Space Complexity (Asked Often)

| Operation   | Complexity |
| ----------- | ---------- |
| groupingBy  | O(n)       |
| sorting     | O(n log n) |
| nth highest | O(n log n) |
| joining     | O(n)       |

---

## 10. Interview Tip ⭐

Always mention:

* **Optional handling**
* **distinct vs non-distinct**
* **boxing/unboxing cost**
* **readability vs performance tradeoff**

---

If you want, I can also provide:

* **Top 50 Java Stream interview questions**
* **Real-world coding challenges**
* **Parallel stream caveats**
* **Java 17 stream enhancements**

Just say the word 😊

