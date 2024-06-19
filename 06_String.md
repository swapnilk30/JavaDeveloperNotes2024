

### What is String class?
- String is the final class that represents sequence of character.
- It is present in Package is Java.Lang.
- String class implements Serializable, comparable, char sequence
interface.
- String is the immutable, once string object is created, it cannot
changed but new string object is created.
- String is not a primitive data type. It is a reference data type

### How to create the string object?

### What is String constant pool?
- string constant pool is a separate place in the heap memory where the
values of all the strings which are defined in the program are stored.

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

```


char[] ch={'j','a','v','a','t','p','o','i','n','t'};  
String s=new String(ch);  
// is same as:
String s="javatpoint";  
```