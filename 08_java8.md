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

## What is Lambda Expression (λ):

### The Main Objective of Lambda Expression is to bring benefits of functional programming into Java.
    • Lambda Expression is just an anonymous (nameless) function. That means the function which
    doesn’t have the name, return type and access modifiers.
    • Lambda Expression also known as anonymous functions or closures.

## Stream API
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