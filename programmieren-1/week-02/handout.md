# Handout

## Week 2 Handout: Variables and Calculations

Read each section before its exercises. Examples assume the class is saved in a file with the same name, for example `Variables.java` for `public class Variables`.

***

### 1. Values and variables

A **value** is a piece of data, such as the number `17` or the text `"Java"`. A **variable** is a named place in a program where a value can be stored. You can read the value later or replace it with another value.

```java
int age = 19;
System.out.println(age);
```

The declaration `int age = 19;` has three parts:

1. `int` is the type: this variable stores a whole number.
2. `age` is the variable name.
3. `= 19` gives the variable its initial value.

The `=` symbol is the **assignment operator**. It stores the value on its right in the variable on its left. It does not mean “is equal to” as it does in ordinary mathematics.

### 2. Declaring, assigning, and updating

Declare a variable once, then assign new values to it as needed:

```java
int score = 0;  // declaration and initial value
score = 5;      // assignment
score = score + 2;
System.out.println(score); // 7
```

For `score = score + 2;`, Java first calculates the right side using the old value of `score`, then stores the result back in `score`.

Common shorthand operators combine an operation and assignment:

```java
score += 2; // same effect as score = score + 2;
score -= 1; // subtract 1 and store the result
score++;    // add 1
score--;    // subtract 1
```

Use a descriptive name such as `itemCount` rather than a vague name such as `x`. Java variable names begin with a letter, `_`, or `$`, and cannot contain spaces. By convention, variable names use **lower camel case**: `totalPrice`, `numberOfStudents`.

### 3. Types

Java checks that a variable is used with values of a compatible type. The type determines what kind of value can be stored.

| Type | Stores | Example |
| --- | --- | --- |
| `int` | Whole numbers | `int count = 12;` |
| `double` | Numbers with a decimal part | `double temperature = 18.5;` |
| `boolean` | `true` or `false` | `boolean isOpen = true;` |
| `char` | One character in single quotes | `char grade = 'A';` |
| `String` | Text in double quotes | `String name = "Ada";` |

`String` starts with a capital letter because it is a Java class name. The primitive types shown above start with lowercase letters. A `char` uses single quotes and holds one character; a `String` uses double quotes and can hold many characters.

The value assigned to a variable must fit its type. For example, `int count = 2.5;` is an error because `2.5` is not a whole number. The compiler catches many type mistakes before the program runs.

### 4. Arithmetic expressions

Java can calculate with numeric values and variables:

| Operator | Meaning | Example |
| --- | --- | --- |
| `+` | addition | `3 + 4` gives `7` |
| `-` | subtraction | `9 - 2` gives `7` |
| `*` | multiplication | `3 * 4` gives `12` |
| `/` | division | `8 / 2` gives `4` |
| `%` | remainder | `9 % 4` gives `1` |

For integer operands, `/` performs **integer division** and discards the fractional part:

```java
System.out.println(7 / 2); // 3
System.out.println(7 % 2); // 1, the remainder
```

If either operand is a `double`, division can produce a decimal result:

```java
System.out.println(7.0 / 2); // 3.5
```

Java follows the usual arithmetic precedence: multiplication, division, and remainder happen before addition and subtraction. Parentheses make the intended order clear:

```java
int result = 2 + 3 * 4;   // 14
int other = (2 + 3) * 4; // 20
```

### 5. Combining text and values

The `+` operator adds numbers, but joins text when one side is a `String`:

```java
int age = 19;
System.out.println("Age: " + age); // Age: 19
System.out.println("2" + 3);       // 23
System.out.println(2 + 3);         // 5
```

As seen in Week 1, Java evaluates a chain of `+` operations from left to right. Once a `String` is involved, the remaining values are joined as text:

```java
System.out.println("Total: " + 2 + 3);   // Total: 23
System.out.println("Total: " + (2 + 3)); // Total: 5
```

### 6. Reading input with `Scanner`

Programs can read values typed by a user. `Scanner` is a Java class, so add an `import` line before the class declaration:

```java
import java.util.Scanner;

public class AskAge {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("How old are you? ");
        int age = input.nextInt();

        System.out.println("Next year you will be " + (age + 1));
        input.close();
    }
}
```

Important parts:

* `import java.util.Scanner;` makes the `Scanner` class available by its short name.
* `new Scanner(System.in)` creates a scanner that reads from the keyboard.
* `nextInt()` reads the next whole number.
* `nextDouble()` reads the next decimal number.
* `next()` reads the next word, stopping at whitespace.
* `close()` closes the scanner after input is finished.

The decimal separator for `nextDouble()` follows the computer's locale. On many German-language systems, enter `1,5`; on many English-language systems, enter `1.5`.

The input type must match the method. If `nextInt()` is waiting for a whole number and the user types `hello`, the program cannot read that text as an integer.

For now, use `next()` when reading a single word. It does not read a full line containing spaces. Mixing `nextInt()` and `nextLine()` can be surprising because `nextInt()` leaves the end of the line behind; we will practice line-based input separately.

### 7. Displaying calculated values

You can print values with concatenation or use `printf` for formatted output. Week 1 introduced `%s`, `%d`, and `%n`; `%f` is used for a decimal number:

```java
double price = 3.5;
System.out.printf("Price: %.2f euros%n", price);
```

`%.2f` prints a decimal number with two digits after the decimal separator. The output separator can depend on the computer's language settings. When checking exercises, focus on the numeric value unless the task explicitly requires a particular format.

### 8. Common mistakes

* Using `==` where an assignment `=` was intended, or using `=` where a comparison is intended. Comparisons come in a later week.
* Writing a decimal value into an `int` variable.
* Expecting `7 / 2` to produce `3.5`; both operands are integers, so the result is `3`.
* Forgetting that `"2" + 3` joins text and produces `23`.
* Forgetting the `import` line or the semicolon after it.
* Calling `nextInt()` when the input is not a valid whole number.
* Writing `scanner` instead of `Scanner`; Java is case-sensitive.

### 9. Workflow

1. Save the file. The public class name and filename must match.
2. Compile with `javac AskAge.java`.
3. Run with `java AskAge`.
4. Type the requested input in the terminal and press Enter.
5. Predict the output before changing a value, then compile and run again.

### 10. Quick reference

| I want to... | I write... |
| --- | --- |
| declare a whole-number variable | `int count = 0;` |
| declare a decimal variable | `double price = 2.5;` |
| assign a new value | `count = 3;` |
| add to a variable | `count += 1;` |
| read an integer | `int value = input.nextInt();` |
| read a decimal | `double value = input.nextDouble();` |
| read one word | `String word = input.next();` |
| print a decimal with two places | `System.out.printf("%.2f%n", value);` |

### 11. Glossary

* **Assignment:** storing a value in a variable.
* **Expression:** values and operators that Java evaluates to produce a result.
* **Primitive type:** one of Java's built-in simple value types, such as `int` or `boolean`.
* **Remainder:** what is left after integer division; calculated with `%`.
* **Variable:** a named place to store a value while a program runs.