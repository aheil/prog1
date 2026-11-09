# Handout

## Week 5 Handout: Nested Loops and Methods

Examples use the default package. Save each complete example in a file whose name matches its public class.

### Suggested two-session sequence

| Session | Main topics |
| --- | --- |
| 1 | Nested loops, tracing, and combining loops with conditions |
| 2 | Methods, parameters, return values, `void`, scope, and decomposition |

By the end of the week, you should be able to trace nested loops, choose which repetition belongs in each loop, write a method with parameters and a return value, call methods, and divide a small program into clear steps.

***

## Session 1: Nested loops

### 1. A loop inside a loop

A **nested loop** is a loop inside the body of another loop. For every pass of the outer loop, the inner loop runs from beginning to end.

```java
for (int row = 1; row <= 3; row++) {
    for (int column = 1; column <= 4; column++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

Output:

```text
* * * *
* * * *
* * * *
```

The outer loop selects a row. The inner loop prints all four columns in that row. The inner loop starts over for each new row.

### 2. Trace the order

For small loops, list each pair of loop-variable values:

```java
for (int row = 1; row <= 2; row++) {
    for (int column = 1; column <= 3; column++) {
        System.out.println(row + "," + column);
    }
}
```

The pairs are `(1,1)`, `(1,2)`, `(1,3)`, `(2,1)`, `(2,2)`, `(2,3)`. The inner loop completes all its passes before the outer loop advances.

For an outer loop with `r` passes and an inner loop with `c` passes each time, the body runs `r * c` times. If the inner loop's limit depends on the outer loop, count the passes row by row instead.

### 3. A changing inner-loop limit

The inner loop can use the outer loop's variable:

```java
for (int row = 1; row <= 4; row++) {
    for (int column = 1; column <= row; column++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

Output:

```text
*
* *
* * *
* * * *
```

On row 1, the inner loop runs once; on row 4, it runs four times. This pattern is useful for simple tables and printed shapes.

### 4. Combining loops and conditions

Use an `if` inside a loop when only some combinations should be processed. For example, print the pairs from 1 to 3 whose values add up to 4:

```java
for (int first = 1; first <= 3; first++) {
    for (int second = 1; second <= 3; second++) {
        if (first + second == 4) {
            System.out.println(first + " + " + second);
        }
    }
}
```

The condition is checked once for every pair. Here it prints `1 + 3`, `2 + 2`, and `3 + 1`.

### 5. Choosing loop variables and boundaries

- Give each loop its own variable, such as `row` and `column`.
- Decide what one pass of the outer loop represents, then what one pass of the inner loop represents.
- Check the first and last values of both loops to avoid off-by-one errors.
- Keep the inner loop's initialization inside its header so it restarts for every outer pass.
- Use braces to make the loop nesting clear.

### 6. Common mistakes

- Putting the inner loop after, rather than inside, the outer loop.
- Forgetting that the inner loop runs again for every outer-loop pass.
- Reusing or changing the outer loop variable in the inner loop.
- Using a fixed inner-loop limit when it should depend on the outer variable (or the reverse).
- Printing a newline inside the inner loop when each row should stay on one line.
- Miscounting total iterations; trace the loops before trying a large input.

***

## Session 2: Methods

### 1. Why use methods?

A **method** is a named block of code that can be called when needed. Methods let you give a task a clear name, avoid repeating the same code, and split a larger program into smaller steps.

In the examples this week, methods are `static`, because they are called from the `static` `main` method. Classes and objects will be covered later.

### 2. A method with parameters and a return value

```java
static int rectangleArea(int width, int height) {
    return width * height;
}
```

This method has:

| Part | Meaning |
| --- | --- |
| `static` | This method can be called from `main` in the same class |
| `int` | The method returns a whole number |
| `rectangleArea` | The method name |
| `int width, int height` | Parameters: the input values the method receives |
| `return width * height;` | The result sent back to the caller |

Call the method by writing its name and providing arguments:

```java
int area = rectangleArea(5, 3);
System.out.println(area); // 15
```

The values `5` and `3` are **arguments**. They are assigned to the parameters `width` and `height` while the method runs. The returned value is stored in `area`.

### 3. A complete program

```java
import java.util.Scanner;

public class Rectangle {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int width = input.nextInt();
        int height = input.nextInt();

        int area = rectangleArea(width, height);
        System.out.println("Area: " + area);
        input.close();
    }

    static int rectangleArea(int width, int height) {
        return width * height;
    }
}
```

For input `5` and `3`, the program prints `Area: 15`. Execution starts in `main`, calls `rectangleArea`, uses the returned result, and then continues in `main`.

### 4. `void` methods

A method that performs an action but does not return a value uses `void`:

```java
static void printRectangle(int rows, int columns) {
    for (int row = 1; row <= rows; row++) {
        for (int column = 1; column <= columns; column++) {
            System.out.print("* ");
        }
        System.out.println();
    }
}
```

Call it as a statement:

```java
printRectangle(2, 3);
```

Do not try to assign the result of a `void` method to a variable. It has no result to assign.

### 5. Methods can combine this week's topics

Methods can contain loops and conditions, and can call other methods. For example:

```java
static int countEvenNumbers(int limit) {
    int count = 0;
    for (int number = 1; number <= limit; number++) {
        if (number % 2 == 0) {
            count++;
        }
    }
    return count;
}
```

`countEvenNumbers(6)` returns `3`. The loop checks each number, the condition selects even numbers, and the method returns the final count.

### 6. Local variables and scope

A method's parameters and variables declared inside it are **local** to that method. They can be used there, but not directly from another method.

```java
static int doubleValue(int value) {
    int result = value * 2;
    return result;
}
```

Here, `value` and `result` belong to `doubleValue`. In `main`, use the returned value by assigning it to a variable:

```java
int answer = doubleValue(7);
```

The variable `answer` is separate from the method's local variable `result`.

### 7. Decomposing a program

When a `main` method becomes long, split its distinct tasks into methods. A small program might:

1. Read input in `main`.
2. Call a method that calculates a result.
3. Print the result in `main`.

Choose names that describe what a method does, such as `rectangleArea`, `countEvenNumbers`, or `printRectangle`. Prefer one clear task per method. Pass needed values as parameters instead of relying on variables declared in another method.

### 8. Common mistakes

- Defining a method inside `main`. Define methods inside the class but outside other methods.
- Calling a method with the wrong number or type of arguments.
- Forgetting to capture or use a returned value.
- Declaring a method as `void` when the caller needs a result, or declaring a return type but not returning a value on every path.
- Printing a result inside a calculation method when the caller should decide what to do with it.
- Trying to use a local variable from another method.
- Writing code after a `return` statement that can never be reached.

### 9. Quick reference

| Goal | Example |
| --- | --- |
| Return an integer | `static int square(int number) { return number * number; }` |
| Return a boolean | `static boolean isEven(int number) { return number % 2 == 0; }` |
| Perform an action | `static void printLine() { System.out.println("---"); }` |
| Call a method that returns a value | `int result = square(4);` |
| Call a `void` method | `printLine();` |
