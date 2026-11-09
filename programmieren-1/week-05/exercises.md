# Exercises

## Week 5: Nested Loops and Methods

**Homework:** See the separate [homework and daily exercises](homework.md).

**Goals:** trace nested loops, combine loops with conditions, and write methods that accept parameters, return values, or perform an action.

**Tiers:** **C** = core (everyone), **E** = extension (fast students / homework), **X** = challenge (optional).

**Input** is what you type; **Output** is what the program displays. Unless an exercise gives a method signature, use a separate class with a `main` method to read input and display output. Define `static` methods inside the class but outside `main`.

***

### Session 1: Nested loops and conditions

Time plan: 0-5 min retrieve loop patterns, 5-30 min exercises, 30-40 min compare traces and outputs, 40-45 min wrap-up.

#### Ex 1.1 (C): Trace the pairs

Without running the code, list each `(row, column)` pair printed and predict how many lines there will be. Then run it and check your prediction.

```java
for (int row = 1; row <= 2; row++) {
    for (int column = 1; column <= 3; column++) {
        System.out.println(row + "," + column);
    }
}
```

#### Ex 1.2 (C): Print a rectangle

Read two whole numbers, `rows` and `columns`. Print a rectangle with `rows` lines and `columns` asterisks on each line, separated by one space.

Input `3` and `4`:

```text
* * * *
* * * *
* * * *
```

Test a `1 x 1` rectangle and a rectangle with one row.

#### Ex 1.3 (C): Growing triangle

Read a positive whole number `n`. Print `n` lines: line 1 has one asterisk, line 2 has two, and so on, up to line `n`.

Input `4`:

```text
*
* *
* * *
* * * *
```

Use the outer loop for the row and make the inner loop's limit depend on that row.

#### Ex 1.4 (C): Multiplication grid

Read a positive whole number `n`. Print the products for rows and columns from `1` to `n`, with each product followed by one space.

Input `3`:

```text
1 2 3
2 4 6
3 6 9
```

Use nested loops. The row number is multiplied by each column number.

#### Ex 1.5 (C): Pairs with a target sum

Read `n` and `target`. Consider all ordered pairs `(first, second)` where both values are from `1` to `n`. Print each pair whose sum equals `target`, one per line, in the order the nested loops visit them.

Input `4` and `5`:

```text
1 + 4
2 + 3
3 + 2
4 + 1
```

Use an `if` inside the inner loop. Try a target that produces no pairs.

#### Ex 1.6 (E): Checkerboard

Read positive integers `rows` and `columns`. Print a checkerboard using `X` and `O`, starting with `X` in the top-left cell. Separate symbols with one space.

Input `3` and `4`:

```text
X O X O
O X O X
X O X O
```

Hint: the symbol depends on whether `row + column` is even or odd. Choose whether your row and column variables start at `0` or `1`, and make the condition match.

#### Ex 1.7 (X): Right-aligned triangle

Read a positive integer `n`. Print a right-aligned triangle of height `n`, using spaces followed by asterisks. Do not print trailing spaces.

Input `4`:

```text
   *
  **
 ***
****
```

Use nested loops for both the leading spaces and the asterisks. Decide how many of each to print on every row.

***

### Session 2: Methods and decomposition

Time plan: 0-5 min recap, 5-30 min method exercises, 30-40 min combine methods and loops, 40-45 min wrap-up.

#### Ex 2.1 (C): Trace a method call

Without running the code, write down the value returned by each call and the final output. Then run it.

```java
static int addAndDouble(int first, int second) {
    int total = first + second;
    return total * 2;
}

public static void main(String[] args) {
    int result = addAndDouble(3, 4);
    System.out.println(result);
}
```

Explain which values are arguments and which names are parameters.

#### Ex 2.2 (C): Square method

Write this method and call it from `main`:

```java
static int square(int number)
```

It returns the number multiplied by itself. Read an integer, call the method, and print the returned value.

Input `-4` gives `16`. Also test `0` and a positive number.

#### Ex 2.3 (C): Larger of two

Write and use this method:

```java
static int maxOfTwo(int first, int second)
```

It returns the larger argument. If both arguments are equal, it returns that value. Read two integers and print the result.

Test `3, 9`, `9, 3`, and `5, 5`.

#### Ex 2.4 (C): Count even numbers

Write and call this method:

```java
static int countEvenNumbers(int limit)
```

It returns how many even numbers are in the range from `1` through `limit`, inclusive. Use a loop, an `if`, and a local counter.

Read `limit` in `main` and print the returned count. For input `6`, print `3`; for input `1`, print `0`.

#### Ex 2.5 (C): Print a rectangle method

Write this `void` method:

```java
static void printRectangle(int rows, int columns)
```

It prints the asterisk rectangle from Ex 1.2. Call it from `main` after reading the two dimensions. Do not make the method return a value.

#### Ex 2.6 (E): Number report

Read a positive integer `n`. Write and use both methods:

```java
static int sumTo(int limit)
static int countEvenNumbers(int limit)
```

`sumTo` returns `1 + 2 + ... + limit`; `countEvenNumbers` returns the number of even values from `1` through `limit`. Print:

```text
Sum: <sum>
Even numbers: <count>
```

For input `6`, print `Sum: 21` and `Even numbers: 3`. Keep input and output in `main`; let each method calculate and return its own result.

#### Ex 2.7 (E): Find and explain scope errors

The code below does not compile. Identify why `result` cannot be printed from `main`, fix the program by returning a value from `doubleValue`, and print the returned value.

```java
public class ScopeBug {
    public static void main(String[] args) {
        doubleValue(7);
        System.out.println(result);
    }

    static void doubleValue(int value) {
        int result = value * 2;
    }
}
```

The corrected program should print `14`. Do not move `result` into a shared field; use a return value.

#### Ex 2.8 (X): Prime-checking method

Write and use this method:

```java
static boolean isPrime(int number)
```

It returns `true` when `number` is prime and `false` otherwise. A prime is an integer greater than 1 with no positive divisors other than 1 and itself. Use a loop and a condition to check for divisors.

Read an integer and print `Prime` or `Not prime`. Test `2`, `9`, `1`, and a negative number. You may stop checking as soon as a divisor is found.

***

### Homework

Complete the separate [Week 5 homework and daily exercises](homework.md).

1. **Factor pairs (`Week05Homework1.java`, core).** Read a positive integer `n`. Print all positive factor pairs `(first, second)` such that `first * second == n`, with `first` increasing from `1` to `n`. Print each pair as `first x second = n`, one per line. Put the pair-printing logic in `static void printFactorPairs(int number)`. For input `12`, the output is:

   ```text
   1 x 12 = 12
   2 x 6 = 12
   3 x 4 = 12
   4 x 3 = 12
   6 x 2 = 12
   12 x 1 = 12
   ```

2. **Number report (`Week05Homework2.java`, extension).** Read a positive integer `n`. Print the sum from `1` to `n` and the count of even numbers from `1` to `n`, using the format from Ex 2.6. Implement and call `static int sumTo(int limit)` and `static int countEvenNumbers(int limit)`. For input `6`, print `Sum: 21` and `Even numbers: 3`.

**Acceptance criteria:** both classes compile; the sample outputs match exactly; the required methods have the specified names, parameter types, and return types; calculations are performed by the methods rather than duplicated in `main`.
