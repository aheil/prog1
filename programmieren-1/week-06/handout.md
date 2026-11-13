# Handout

## Week 6 Handout: Arrays, References, and First Objects

So far, every variable has held exactly one value. This week you learn to store many values under one name (**arrays**) and meet the idea behind all larger Java programs: **objects** that live in memory and are reached through **references**.

### Suggested two-session sequence

| Session | Time | Content |
| --- | --- | --- |
| 1 | 0-10 min | Why arrays? Declaring, creating, indexing, `length` |
| 1 | 10-25 min | Looping over arrays; for-each; standard patterns (sum, max, count, search) |
| 1 | 25-40 min | Exercises 1.1-1.6 |
| 1 | 40-45 min | Common mistakes; `ArrayIndexOutOfBoundsException` |
| 2 | 0-10 min | What is an object? `Scanner`, `Random`, and arrays as objects |
| 2 | 10-20 min | Memory model: primitive vs. reference variables, aliasing, `null` |
| 2 | 20-30 min | A first class of your own: `Point` with fields |
| 2 | 30-42 min | Exercises 2.1-2.5 |
| 2 | 42-45 min | Outlook: instance methods and constructors (weeks 8-9) |

***

## Session 1: Arrays

### 1. Why arrays?

Suppose you want to store the temperatures of one week:

```java
int t0 = 12;
int t1 = 15;
int t2 = 9;
// ... t3 to t6
```

Seven variables are awkward, and 365 are impossible. You also cannot write a loop over `t0`, `t1`, `t2`, because the number is part of the *name*. An **array** stores many values of the same type under one name and numbers them for you.

### 2. Declaring and creating an array

```java
int[] temperatures = new int[7];
```

- `int[]` is the type "array of `int`".
- `new int[7]` creates an array with **7 elements**.
- Every element starts with a **default value**: `0` for `int`, `0.0` for `double`, `false` for `boolean`, and `null` for objects.

If you already know the values, use an **initializer list**:

```java
int[] temperatures = {12, 15, 9, 17, 20, 18, 14};
```

The size of an array is fixed when it is created. It cannot grow or shrink later.

### 3. Indexes and `length`

Elements are numbered by an **index** that starts at **0**:

```text
index:   0   1   2   3   4   5   6
value:  12  15   9  17  20  18  14
```

```java
System.out.println(temperatures[0]);   // 12 (first element)
temperatures[2] = 10;                   // change the third element
System.out.println(temperatures.length); // 7
```

- The valid indexes are `0` to `length - 1`.
- `length` is a field, not a method: write `temperatures.length` without parentheses.
- Accessing `temperatures[7]` compiles but crashes at runtime with `ArrayIndexOutOfBoundsException`.

### 4. Looping over an array

The index-based `for` loop is the standard pattern:

```java
for (int i = 0; i < temperatures.length; i++) {
    System.out.println("Day " + i + ": " + temperatures[i]);
}
```

Use `i < temperatures.length`, never `i <= temperatures.length`.

### 5. The enhanced `for` loop (for-each)

If you only need to *read* every value and do not need the index, use the for-each loop:

```java
int sum = 0;
for (int t : temperatures) {
    sum += t;
}
```

Read it as "for each `t` in `temperatures`". The for-each loop is **not suitable** when you:

- need the index (e.g., "the maximum is at index 4"),
- want to change elements (assigning to `t` only changes a copy),
- want to visit only part of the array or go backwards.

### 6. Reading values into an array

```java
import java.util.Scanner;

public class ReadValues {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        for (int i = n - 1; i >= 0; i--) {
            System.out.print(values[i] + " ");
        }
        System.out.println();
    }
}
```

Once the values are stored, you can process them **as often as you like**. Without an array, you could not print them backwards.

### 7. Standard patterns

**Sum and average.** Use a `double` for the average to avoid integer division:

```java
int sum = 0;
for (int v : values) {
    sum += v;
}
double average = (double) sum / values.length;
```

**Maximum and its position.** Start with the first element, not with `0` (all values could be negative):

```java
int maxIndex = 0;
for (int i = 1; i < values.length; i++) {
    if (values[i] > values[maxIndex]) {
        maxIndex = i;
    }
}
System.out.println("Max: " + values[maxIndex] + " at index " + maxIndex);
```

**Counting.** Count the elements that meet a condition:

```java
int count = 0;
for (int v : values) {
    if (v > average) {
        count++;
    }
}
```

**Linear search.** Stop as soon as you find the value:

```java
int found = -1;
for (int i = 0; i < values.length; i++) {
    if (values[i] == target) {
        found = i;
        break;
    }
}
```

`-1` is a common "not found" marker because it is never a valid index.

**Counter arrays.** The index itself can stand for something. To count dice throws, use `counts[face]`:

```java
int[] counts = new int[7];   // indexes 0-6; index 0 stays unused
for (int face : throwsArray) {
    counts[face]++;
}
```

### 8. Printing an array

`System.out.println(values)` does **not** print the contents. It prints something like `[I@1b6d3586` (the type and a hash code). Write a loop, or use `Arrays.toString` while debugging:

```java
import java.util.Arrays;

System.out.println(Arrays.toString(values));   // [3, 1, 4]
```

### 9. Common mistakes

| Mistake | Effect |
| --- | --- |
| `for (int i = 0; i <= a.length; i++)` | `ArrayIndexOutOfBoundsException` in the last iteration |
| `for (int i = 1; i < a.length; i++)` to visit all elements | The first element is skipped |
| `a.length()` | Compile error: `length` is a field for arrays |
| `int[] a;` and then `a[0] = 5;` | Compile error: `a` might not have been initialized |
| `int max = 0;` for the maximum | Wrong result if all values are negative |
| Confusing `i` and `a[i]` | You process positions instead of values |

### 10. Compute in methods, print in `main`

From this week on, we separate the work of a program into three parts:

1. **Reading** input: a method that gets the `Scanner` and returns the data.
2. **Computing**: methods that get arrays (or objects) and **return** a result. They neither read nor print.
3. **Printing**: `main` calls the methods and prints their results.

```java
import java.util.Scanner;

public class ScoreStats {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[] scores = readValues(sc);
        System.out.println("Sum: " + sum(scores));
        System.out.println("Max: " + scores[indexOfMax(scores)]);
    }

    static int[] readValues(Scanner sc) {
        int n = sc.nextInt();
        int[] values = new int[n];
        for (int i = 0; i < n; i++) {
            values[i] = sc.nextInt();
        }
        return values;
    }

    static int sum(int[] values) {
        int total = 0;
        for (int v : values) {
            total += v;
        }
        return total;
    }

    static int indexOfMax(int[] values) {
        int maxIndex = 0;
        for (int i = 1; i < values.length; i++) {
            if (values[i] > values[maxIndex]) {
                maxIndex = i;
            }
        }
        return maxIndex;
    }
}
```

Why is this better than doing everything in `main`?

- **Reuse:** `sum` works for any `int[]`, whether it comes from the keyboard, a file, or another method.
- **Testing:** you (and the automatic tests) can call `sum(new int[] {1, 2, 3})` and check that the result is `6`, without typing input or comparing printed text. `readValues` can even be tested without a keyboard: `readValues(new Scanner("3 1 2 3"))` reads from the text.
- **Readability:** `main` reads like a summary of the program.

A method that should produce **several values** can return an array (e.g., a counter array), and a method that should produce a variable number of values returns a new array of the right size: count first, then create the array, then fill it.

***

## Session 2: Objects and references

### 1. What is an object?

An **object** bundles **data** (its state) with **operations** (its methods). A **class** is the blueprint, and an object is one concrete **instance** created from it. One class can produce many objects.

You have used objects since week 2:

```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
```

- `Scanner` is a class.
- `new Scanner(System.in)` creates a new object of that class.
- `sc` is a variable that **refers** to the object.
- `sc.nextInt()` calls a method **on that object**. The dot means "ask this object to do something".

### 2. Another library object: `Random`

```java
import java.util.Random;

Random random = new Random(42);
int die = random.nextInt(6) + 1;   // 1 to 6
```

- `nextInt(6)` returns a number from `0` to `5`, so `+ 1` gives a die roll.
- The number `42` is a **seed**. The same seed always produces the same sequence. This makes programs reproducible and testable. `new Random()` without a seed gives a different sequence each run.

Strings are objects, too: `"Hello".length()` asks the string object for its length. Strings get their own week (week 7).

### 3. Arrays are objects

`new int[5]` creates an object in a memory area called the **heap**. The variable does not contain the five numbers. It contains a **reference** to them, like an arrow pointing to the object.

```java
int x = 5;
int[] a = {1, 2, 3};
```

```text
 Variables                     Heap
+-------+-----+
| x     |  5  |
+-------+-----+               +---+---+---+
| a     |  o--|-------------> | 1 | 2 | 3 |
+-------+-----+               +---+---+---+
```

| | Primitive type (`int`, `double`, `boolean`, `char`, ...) | Reference type (arrays, `Scanner`, `String`, your own classes) |
| --- | --- | --- |
| The variable holds | the value itself | a reference to an object |
| Created with | a literal or a calculation | `new` (or a literal for arrays and strings) |
| Default value for fields and array elements | `0`, `0.0`, `false` | `null` |
| `==` compares | the values | whether both refer to the **same** object |
| Passed to a method | a copy of the value | a copy of the **reference**: both point to the same object |

### 4. Aliasing

Assigning a reference copies the arrow, not the object:

```java
int[] a = {1, 2, 3};
int[] b = a;      // b refers to the SAME array
b[0] = 99;
System.out.println(a[0]);   // 99
```

```text
a  o----+
        +---> | 99 | 2 | 3 |
b  o----+
```

`a` and `b` are **aliases**: two names for one object. To get an independent copy, create a new array and copy the elements:

```java
int[] copy = new int[a.length];
for (int i = 0; i < a.length; i++) {
    copy[i] = a[i];
}
```

`Arrays.copyOf(a, a.length)` does the same thing in one line.

**Comparing.** `a == b` is `true` only if both refer to the same object. Two different arrays with equal contents are not `==`. Compare contents element by element, or use `Arrays.equals(a, b)`.

### 5. Arrays and methods

A method can take an array as a parameter and return one:

```java
static int sum(int[] values) {
    int total = 0;
    for (int v : values) {
        total += v;
    }
    return total;
}

static int[] createRange(int n) {
    int[] result = new int[n];
    for (int i = 0; i < n; i++) {
        result[i] = i + 1;
    }
    return result;
}
```

Because the parameter receives a copy of the **reference**, a method **can change the caller's array**:

```java
static void doubleAll(int[] values) {
    for (int i = 0; i < values.length; i++) {
        values[i] *= 2;
    }
}

static void doubleNumber(int x) {
    x *= 2;   // changes only the local copy
}
```

After `doubleAll(a)`, the caller sees the doubled values. After `doubleNumber(n)`, `n` is unchanged.

### 6. A first class of your own

You can define your own types. Put this class in its own file `Point.java`:

```java
public class Point {
    int x;
    int y;
}
```

`x` and `y` are **fields**: variables that belong to each object. Every `Point` object has its own `x` and `y`.

```java
public class PointDemo {
    public static void main(String[] args) {
        Point p = new Point();   // x = 0, y = 0 (default values)
        p.x = 3;
        p.y = 4;

        Point q = new Point();
        q.x = 6;
        q.y = 8;

        print(p);                                 // (3, 4)
        print(q);                                 // (6, 8)
        System.out.println(distance(p, q));       // 5.0
    }

    static void print(Point p) {
        System.out.println("(" + p.x + ", " + p.y + ")");
    }

    static double distance(Point a, Point b) {
        int dx = a.x - b.x;
        int dy = a.y - b.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

Compile both files together: `javac Point.java PointDemo.java`, or simply `javac *.java`.

Objects of your own classes behave exactly like arrays:

```java
Point r = p;   // alias, not a copy
r.x = 100;
print(p);      // (100, 4)
```

Two small helpers make work with `Point` easier and keep printing out of the computation. `createPoint` creates and fills an object and returns it; `format` returns the text instead of printing it:

```java
static Point createPoint(int x, int y) {
    Point p = new Point();
    p.x = x;
    p.y = y;
    return p;
}

static String format(Point p) {
    return "(" + p.x + ", " + p.y + ")";
}

// in main:
Point p = createPoint(3, 4);
System.out.println(format(p));   // (3, 4)
```

A method that returns an object returns a **reference** to it. `createPoint` creates a new object each time; a method like `closestToOrigin(points)` returns a reference to one of the existing objects. In week 9, constructors (`new Point(3, 4)`) will replace `createPoint`.

### 7. `null` and `NullPointerException`

A reference variable can hold `null`, meaning "refers to no object". Using it crashes:

```java
Point p = null;
p.x = 1;   // NullPointerException
```

### 8. Arrays of objects

```java
Point[] points = new Point[3];
```

This creates **one** array with three slots, and every slot is `null`. It does **not** create any `Point` objects. Each element needs its own `new`:

```java
for (int i = 0; i < points.length; i++) {
    points[i] = new Point();
    points[i].x = i;
    points[i].y = i * i;
}
```

```text
points o---> | o | o | o |
               |   |   +--> Point(2, 4)
               |   +------> Point(1, 1)
               +----------> Point(0, 0)
```

### 9. Outlook

Our `Point` class only holds data, and all operations are `static` methods in another class. In weeks 8 and 9 you will move the operations *into* the class (`p.print()`, `p.distanceTo(q)`), write constructors (`new Point(3, 4)`), and protect fields with `private`.

### 10. Common mistakes

| Mistake | Effect |
| --- | --- |
| `int[] b = a;` to make a copy | Changes to `b` also appear in `a` |
| `a == b` to compare contents | `false` for two different arrays with equal contents |
| `Point[] ps = new Point[3]; ps[0].x = 1;` | `NullPointerException`: the slots are still `null` |
| Two classes named `Point` in one folder | Compile error: duplicate class |
| `System.out.println(p)` for a `Point` | Prints `Point@1b6d3586`, not the coordinates |

### 11. Quick reference

```java
int[] a = new int[5];             // five zeros
int[] b = {3, 1, 4};              // initializer list
a.length                          // number of elements
a[0], a[a.length - 1]             // first and last element
for (int i = 0; i < a.length; i++) { ... }
for (int v : a) { ... }           // read-only traversal

java.util.Arrays.toString(a)      // "[0, 0, 0, 0, 0]"
java.util.Arrays.copyOf(a, n)     // new array with the first n elements
java.util.Arrays.equals(a, b)     // compare contents

Random r = new Random(seed);      // reproducible random numbers
r.nextInt(6) + 1                  // die roll 1-6

Point p = new Point();            // new object, fields have default values
p.x = 3;                          // write a field
Point q = p;                      // alias: both refer to one object
```
