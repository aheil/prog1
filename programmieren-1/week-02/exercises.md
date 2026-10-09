# Exercises

## Week 2: Variables and Calculations

**Goals:** declare and update variables, choose basic types, calculate with arithmetic operators, and read simple keyboard input.

**Tiers:** **C** = core (everyone), **E** = extension (fast students / homework), **X** = challenge (optional).

In the examples below, **Input** is what you type and **Output** is what the program displays. Use the shown labels; decorative borders are not needed.

### Session 1

Time plan: 0-5 min recap, 5-32 min exercises, 32-42 min quiz, 42-45 min wrap-up.

#### Ex 1.1 (C): First variables

Create `Student.java`. Declare variables for a first name, age, and whether you have programmed before. Print each value on its own line. Choose an appropriate type for each value.

#### Ex 1.2 (C): Change a value

Create an integer variable `score` with the value `0`. Print it, add 10 using an assignment, then print it again. Predict both output lines before running the program.

Expected output:

```text
0
10
```

#### Ex 1.3 (C): Choose the type

For each value, choose `int`, `double`, `boolean`, `char`, or `String`, then write a declaration: number of books, room temperature, whether a door is open, a grade letter, and a city name.

#### Ex 1.4 (C): Calculate a total

Create variables for the price of three items as whole numbers of cents. Calculate and print their total in cents. Try a second version using `double` values in euros.

For prices of `125`, `250`, and `99` cents, the first version should print `Total: 474 cents`. For prices of `1.25`, `2.50`, and `0.99` euros, the second version should print a total of `4.74` euros. Use a label so it is clear what the number means.

#### Ex 1.5 (C): Integer division and remainder

Before running, predict the results of `17 / 5`, `17 % 5`, `17.0 / 5`, and `17 / 5.0`. Print each result with a label and explain the difference.

Expected values, in order: `3`, `2`, `3.4`, and `3.4`.

#### Ex 1.6 (C): Order of operations

Print the results of `2 + 3 * 4` and `(2 + 3) * 4`. Change the expression to calculate the average of three values. Use parentheses to make the order clear.

The first two results should be `14` and `20`. For the average, use the values `4`, `6`, and `8`; the result should be `6.0`. Use `3.0` as the divisor so Java calculates a decimal result.

#### Ex 1.7 (C): Fix the type errors

This code has three type errors. Fix the declarations so they represent the intended values, then print each variable on its own line:

```java
public class TypeErrors {
    public static void main(String[] args) {
      int temperature = 18.5;
        char initial = "A";
        boolean isReady = "true";
      System.out.println(temperature);
      System.out.println(initial);
      System.out.println(isReady);
    }
}
```

   The corrected program should display:

   ```text
   18.5
   A
   true
   ```

#### Ex 1.8 (E): Swap two values

Create two integer variables, `first` and `second`. Swap their values using a third variable. Print the values before and after the swap.

For example, if `first` starts as `3` and `second` as `8`, print `first: 3` and `second: 8` before the swap, then `first: 8` and `second: 3` after it.

#### Ex 1.9 (X): Predict the expression

Without running the code, write down its exact output. Then run it and explain why the two lines differ.

```java
int number = 4;
System.out.println("Value: " + number + 1);
System.out.println("Value: " + (number + 1));
```

### Session 2

Time plan: 0-5 min retrieval practice, 5-32 min exercises, 32-42 min quiz, 42-45 min wrap-up.

#### Ex 2.1 (C): Read an integer

Create `DoubleIt.java`. Ask the user for a whole number, read it with `Scanner`, and print twice that number. Test with `0`, a positive value, and a negative value.

For input `7`, the output should include `14`. For input `-3`, it should include `-6`.

#### Ex 2.2 (C): Rectangle calculator

Ask the user for the rectangle's width and height as positive whole numbers. Read both values with `Scanner`. Calculate the perimeter with `2 * (width + height)` and the area with `width * height`. Print each result on its own labeled line.

For example, with width `5` and height `3`, the program should display:

```text
Width: 5
Height: 3
Perimeter: 16
Area: 15
```

#### Ex 2.3 (C): Minutes converter

Ask for a non-negative whole number of minutes. Calculate and print how many complete hours and leftover minutes that represents. Use `/` and `%`.

Example: `135` minutes is `2` complete hours with `15` minutes left. Print the results with labels, for example `Hours: 2` and `Leftover minutes: 15`.

#### Ex 2.4 (C): Read two values

Ask for two whole numbers. The second number must not be zero. Print their sum, difference, product, and integer quotient on separate labeled lines. Test with values that divide evenly and values that do not.

For input values `17` and `5`, the results should be `Sum: 22`, `Difference: 12`, `Product: 85`, and `Quotient: 3`.

#### Ex 2.5 (C): One-word greeting

Ask for the user's first name with `next()`, then print a greeting. Try entering a first and last name. Observe which part is read and explain why.

For input `Ada Lovelace`, a greeting such as `Hello, Ada!` is expected. `next()` reads only the first word.

#### Ex 2.6 (C): Tip calculator

Ask for a bill amount in whole euros and a tip percentage as a whole number. Calculate `bill * percentage / 100.0` and print the tip with a label. Test with a bill of `100` euros and a tip rate of `15` percent; the tip should be `15.0` euros.

#### Ex 2.7 (C): Formatted result

Update Ex 2.6 to print the tip using `printf` with two digits after the decimal point, for example `Tip: 15.00` or `Tip: 15,00`. The dot or comma depends on your computer's locale.

#### Ex 2.8 (E): Unit conversion

Ask for a distance in kilometers as a `double`. Convert it to miles by dividing the distance by `1.609`, because `1 mile = 1.609 kilometers`. Print the result with two digits after the decimal point.

For input `1.609` kilometers, the result should be `1.00` mile (or `1,00` if your computer uses a comma as the decimal separator).

#### Ex 2.9 (E): Debug the scanner

The program has two mistakes. Find and fix them, then enter `7` and check the output. The program should display:

```text
Number: 7
14
```

```java
import java.util.Scanner

public class ScannerBug {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.print("Number: ");
        int number = input.nextDouble();
        System.out.println(number * 2);
        input.close();
    }
}
```

#### Ex 2.10 (X): Check your own assumptions

Create a program that reads a whole number and prints the remainder when it is divided by `10`. Test with `27` and `-27`. The results are `7` and `-7`: in Java, the remainder has the sign of the number being divided. Explain why this is not always the same as a non-negative last digit.

### Homework

Create `MonthlyBudget.java`. The program reads four whole numbers from standard input: monthly income, rent, food costs, and other costs. It prints the remaining amount after expenses.

Acceptance criteria:

* Read exactly four integer values using `Scanner`.
* Calculate `income - rent - foodCosts - otherCosts` using named variables.
* Print the result as `Remaining: <amount>` on one line.
* Use no fixed example values in the calculation; different input values must produce the correct result.
* Read the values in this order: income, rent, food costs, and other costs. You may type them on one line separated by spaces or on separate lines.
* Test with input values `2000 800 350 250`; the output should be:

   ```text
   Remaining: 600
   ```

The program can be checked automatically by supplying different input values to standard input and checking the output. Finish any open core exercises; extension and challenge exercises are optional.