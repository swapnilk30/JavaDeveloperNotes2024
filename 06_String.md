### What is String class?
- String is the final class that represents sequence of character.
- It is present in Package is Java.Lang.
- String class implements Serializable, comparable,CharSequence
interface.
- String is the immutable, once string object is created, it cannot
changed but new string object is created.
- String is not a primitive data type. It is a reference data type

### 11. What are different ways to create a string object ?
- Generally, there are two ways to create the string object in java.
- They are:
    - By string literal
    - By new keyword

```java
//String literal: String literal is created by using double quotes. For example:
String s = "Hello";

// New keyword: It is the second way of creating string object in java. 
// It is just like creating an object of any class. We can declare it as:
String s = new String("Hello");

```

### 9. What is String constant pool in java ?
- String constant pool is a special memory area in heap which is used for storing string objects. Internally, the string class uses a string constant pool.


### Why Java uses the concept of String literal?
- To make Java more memory efficient (because no new objects are created if it exists already in the string constant pool).

### Different Ways to Compare two strings ?
- By equals() method : It checks the content of string.
- By == operator (double equal operators) : It checks the Address of
strings

### Difference between == and equals() ?

- == is meant for reference comparison
- Return true if both left and right object of "==" have same address or have same reference.
```java
public class Test{
    public static void main(String[] args){

        Student s1 = new Student();
        Student s2 = s1;
        Student s3 = new Student();

        if(s1 == s2) {
            System.out.print("executed");
        }
        // since s1 and s2 are refering to same object thus "==" will give true result

        if(s1 == s3) {
            System.out.print("executed");
        }
        //and s1 and s3 are refering to different object thus it will give false
    }
}
```
- equals() is a method present in "Object" class and it return true or false on the
basis of reference comparision(address comparision)

- "equals" method is overridden in String class , Wrapper class , Collection classes for Content comparision
- note: "equals" method is not overrideen in "StringBuffer" class

![string](/images/equals%20and%20==%20.png)

### 17. What is use of intern() method in java ?

```java
public class InternExample {
    public static void main(String[] args) {
        String s1 = new String("hello");
        String s2 = "hello";

        // Before interning
        System.out.println(s1 == s2); // false, different references

        // Interning s1
        s1 = s1.intern();

        // After interning
        System.out.println(s1 == s2); // true, same reference
    }
}
```
### 14. What is difference between Stringbuilder and Stringbuffer in java ?
![string](/images/stringbuilder.jpg)
