Sure! Here's a clear and structured **question and answer** that explains this concept well:

---

### ❓ **Question:**

In the following Java code, what will be the output and why?

```java
public class Main {
    public static void main(String[] args) {
        Integer x = 120;
        Integer y = 120;

        System.out.println(x == y);
    }
}
```

---

### ✅ **Answer:**

**Output:**

```
true
```

**Explanation:**

In Java, the `==` operator compares object references when used with objects like `Integer`, not their actual values.

However, Java maintains an internal cache for `Integer` values in the range **-128 to 127**. When you assign values within this range to `Integer` objects using autoboxing (like `Integer x = 120;`), Java reuses the same cached object.

So in this code:

```java
Integer x = 120;
Integer y = 120;
```

Both `x` and `y` refer to the **same cached object**, because 120 is within the cache range. As a result, `x == y` returns `true`.

If the values were outside the cache range (e.g., `Integer x = 128;`), then `x == y` would return `false`, because new `Integer` objects would be created for each variable.

To compare the **values** of two Integer objects (regardless of caching), you should use `.equals()`:

```java
x.equals(y); // Always true if values are equal
```

---

Let me know if you want a multiple-choice version too!
