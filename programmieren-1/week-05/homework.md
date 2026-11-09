# Week 5 Homework: Nested Loops and Methods

Use the exercises below to practise this week's nested loops, conditions, and methods. Save each public class in a file with the matching class name. Unless an exercise says otherwise, read input and print results in `main`; put calculations or repeated actions in `static` methods.

The corresponding JUnit checks are documented in [tests/README.md](tests/README.md).

## Daily exercises

Try one exercise each day. Trace or predict the result before running your program, then test it with the examples and one additional input of your own.

### Day 1: Trace nested loops

Create `Week05Daily1.java`. Without running the code, write down every line it prints and how many times the innermost statement runs. Then run it and compare.

```java
for (int row = 1; row <= 3; row++) {
    for (int column = 1; column <= row; column++) {
        System.out.print(row + "," + column + " ");
    }
    System.out.println();
}
```

In your own words, explain when the inner loop starts over and why it runs a different number of times on each row.

### Day 2: Print a pattern

Create `Week05Daily2.java`. Read a positive integer `n` and print a right triangle with `n` rows. Row 1 has one `*`, row 2 has two, and each following row has one more than the previous row.

For input `4`, print:

```text
*
* *
* * *
* * * *
```

Use an outer loop for the rows and an inner loop for the symbols. Test `n = 1`.

### Day 3: Find pairs with a condition

Create `Week05Daily3.java`. Read positive integers `n` and `target`. Check every ordered pair of numbers from `1` through `n` and print the pairs whose sum is `target`, in the order checked. Use nested loops and an `if`.

For input `4` and `5`, print:

```text
1 + 4
2 + 3
3 + 2
4 + 1
```

Also test a target that has no matching pairs.

### Day 4: Write and call methods

Create `DailyMethods.java`. Read two integers and implement these methods:

```java
static int square(int number)
static int maxOfTwo(int first, int second)
```

Print the square of the first input and the larger of the two inputs, each with a label. For inputs `-4` and `9`, print:

```text
Square: 16
Larger: 9
```

Test equal inputs and zero. Keep the input and output in `main`; each method should return its result.

### Day 5: Combine loops and methods

Create `DailyCount.java`. Read a positive integer `limit`. Write a method `static int countMultiplesOfThree(int limit)` that uses a loop and an `if` to count the numbers divisible by 3 from `1` through `limit`. Call it from `main` and print `Multiples of 3: <count>`.

For input `10`, print:

```text
Multiples of 3: 3
```

Test `limit = 2` and `limit = 12`. The method should return the count; it should not print it.

## Homework assignments

Complete the core assignment. The extension is optional. Compile and run each program with the examples and at least one additional test of your own.

1. **Factor pairs (`Week05Homework1.java`, core).** Read a positive integer `n`. Print all positive factor pairs `(first, second)` such that `first * second == n`, with `first` increasing from `1` to `n`. Print each pair as `first x second = n`, one per line. Put the pair-printing logic in `static void printFactorPairs(int number)`. For input `12`, the output is:

   ```text
   1 x 12 = 12
   2 x 6 = 12
   3 x 4 = 12
   4 x 3 = 12
   6 x 2 = 12
   12 x 1 = 12
   ```

2. **Number report (`Week05Homework2.java`, extension).** Read a positive integer `n`. Print the sum from `1` to `n` and the count of even numbers from `1` to `n`, using this format:

   ```text
   Sum: <sum>
   Even numbers: <count>
   ```

   Implement and call `static int sumTo(int limit)` and `static int countEvenNumbers(int limit)`. For input `6`, print `Sum: 21` and `Even numbers: 3`.

**Acceptance criteria:** the core class compiles and its sample output matches exactly; the extension class does too if completed. Required methods have the specified names, parameter types, and return types. Perform calculations in the methods rather than duplicating them in `main`.
