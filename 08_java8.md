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