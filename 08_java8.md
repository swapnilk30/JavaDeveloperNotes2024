
### Wap to print 1 to 100 numbers using Stream Api

```java
public class PrintOneToHundread {

	public static void main(String[] args) {
	
		// Wap to print 1 to 100 numbers using Stream Api
		
		IntStream.range(1, 101).forEach(x->System.out.println(x));
		
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