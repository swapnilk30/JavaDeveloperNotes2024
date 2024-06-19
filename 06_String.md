

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

```


char[] ch={'j','a','v','a','t','p','o','i','n','t'};  
String s=new String(ch);  
// is same as:
String s="javatpoint";  
```