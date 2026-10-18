# Exercises

## Week 3: Decisions and Loops

**Goals:** write conditions, choose between branches, and repeat work with `while` and `for` loops.

**Tiers:** **C** = core (everyone), **E** = extension (fast students / homework), **X** = challenge (optional).

**Input** is what you type; **Output** is what the program displays.

### Session 1: Decisions

Time plan: 0-5 min recap, 5-32 min exercises, 32-42 min quiz, 42-45 min wrap-up.

#### Ex 1.1 (C): Predict the booleans

Predict the value of each expression for `int x = 7;`, then check by printing: `x > 5`, `x == 7`, `x != 7`, `x % 2 == 0`, `x >= 5 && x < 7`, `x < 3 || x > 6`, `!(x > 5)`.

Expected: `true`, `true`, `false`, `false`, `false`, `true`, `false`.

#### Ex 1.2 (C): Adult or minor

Read an age. Print `Adult` if it is 18 or more, otherwise `Minor`.

Input `18` gives `Adult`; input `17` gives `Minor`.

#### Ex 1.3 (C): Even or odd

Read a whole number and print `Even` or `Odd`. Test with `0`, `7`, `-4`, and `-3`.

#### Ex 1.4 (C): Grade letter

Read a score from 0 to 100. Print `A` for 90 or more, `B` for 80-89, `C` for 70-79, `D` for 60-69, otherwise `F`. Test every boundary: `90`, `89`, `80`, `79`, `70`, `69`, `60`, `59`.

#### Ex 1.5 (C): Largest of three

Read three whole numbers and print the largest. Test with all different values, with ties, and with all three equal.

#### Ex 1.6 (C): Fix the bugs

Find and fix three mistakes. For input `5` the program must print `Positive`.

```java
import java.util.Scanner;

public class SignBug {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        if (n = 0) {
            System.out.println("Zero");
        } else if (n > 0)
            System.out.println("Positive");
            System.out.println("Checked");
        } else {
            System.out.println("Negative");
        }
    }
}
```

#### Ex 1.7 (C): Yes or no

Ask `Continue? (yes/no)` and read a word with `next()`. Print `Continuing` for `yes`, `Stopping` for `no`, and `Unknown answer` for anything else. Use `equals`.

#### Ex 1.8 (E): Leap year

A year is a leap year if it is divisible by 4, except years divisible by 100 are not leap years unless they are also divisible by 400. Read a year and print `Leap year` or `Not a leap year`. Test with `2024`, `1900`, `2000`, `2023`.

#### Ex 1.9 (X): Triangle check

Read three side lengths. Print `Equilateral`, `Isosceles`, `Scalene`, or `Not a triangle` (when the sum of any two sides is not greater than the third).

### Session 2: `while` and `for` loops

Time plan: 0-5 min retrieval practice, 5-32 min exercises, 32-42 min quiz, 42-45 min wrap-up.

#### Ex 2.1 (C): Trace first

Without running it, fill in a trace table (pass, `i`, `total`) for the loop below and predict the output. Then run it.

```java
int i = 1;
int total = 0;
while (i <= 5) {
    total += i;
    i++;
}
System.out.println(total);
```

Expected output: `15`.

#### Ex 2.2 (C): Count up and down

Print the numbers `1` to `10` on one line each. Then print `10` down to `1`. Finally print every second number from `0` to `20`.

#### Ex 2.3 (C): Countdown

Read a whole number `n` and print `n`, `n-1`, ..., `1`, then `Liftoff!`. For input `0` print only `Liftoff!`.

#### Ex 2.4 (C): Sum of the first n numbers

Read `n` and print `1 + 2 + ... + n` as `Sum: <value>`. For `n = 100` the result is `Sum: 5050`. Check your result against the formula `n * (n + 1) / 2`.

#### Ex 2.5 (C): Multiplication table

Read `n` and print `n x 1 = ...` up to `n x 10 = ...`.

For `n = 3`, the first line is `3 x 1 = 3` and the last is `3 x 10 = 30`.

#### Ex 2.6 (C): Sum until zero

Read whole numbers until the user enters `0`. Print `Total: <sum>` and `Count: <how many numbers before 0>`.

Input `4 6 10 0` gives `Total: 20` and `Count: 3`. Input `0` gives `Total: 0` and `Count: 0`.

#### Ex 2.7 (C): Validate input

Ask `Enter a number from 1 to 10:` and repeat the question while the number is outside that range. Print `Accepted: <n>` once a valid number is entered.

Input `0 11 5` gives `Accepted: 5`.

#### Ex 2.8 (C): Spot the infinite loop

Why does this loop never end? Fix it so it prints `10` down to `1`, and explain in one sentence how to make sure a loop condition eventually becomes false.

```java
int n = 10;
while (n > 0) {
    System.out.println(n);
    n++;
}
```

#### Ex 2.9 (C): Translate while to for

Rewrite the countdown (Ex 2.3) and the multiplication table (Ex 2.5) using `for`. The output must stay the same. For each header below, predict how many times the body runs, then verify: `for (int i = 0; i < 5; i++)` (5), `for (int i = 1; i <= 5; i++)` (5), `for (int i = 10; i > 0; i -= 3)` (4: `10 7 4 1`), `for (int i = 5; i < 5; i++)` (0). Create `Week03Ex29.java` to run these four loops and print their body counts, one per line: `5`, `5`, `4`, `0`.

#### Ex 2.10 (C): Line of numbers and factorial

Read `n` and print `Numbers: 1 2 ... n` on one line (`Numbers: 1 2 3 4 5` for `5`). Then read another `n` (0 to 12) and print `Factorial: <n!>` with a `for` loop; for `5` print `Factorial: 120`, and for `0` print `Factorial: 1`.

#### Ex 2.11 (C): Statistics of n numbers

Read `n` (at least 1), then `n` whole numbers. Print the minimum, maximum, and how many are positive.

Input `4 -5 -2 -9 -3` gives `Min: -9`, `Max: -2`, `Positive: 0`. Test with a single number.

#### Ex 2.12 (C): Divisors and prime check

Read `n` (at least 2). Print all divisors on one line as `Divisors: <values>` (`Divisors: 1 2 3 4 6 12` for `12`), then print `Prime` or `Not prime`. Test `2`, `9`, `13`, `15`.

#### Ex 2.13 (C): Which loop?

For each task, say whether `for` or `while` fits better and why: (a) print 1 to 100, (b) read numbers until `-1`, (c) ask until the password is correct, (d) sum the digits of a number, (e) print a multiplication table.

#### Ex 2.14 (E): Debug the loops

Each loop has one mistake. Fix them so that the first prints `1` to `5`, the second prints `55`, and the third prints `Max: -2` for input `-5 -2 -9`.

Use three small programs named `Week03Ex214First`, `Week03Ex214Sum`, and `Week03Ex214Max` respectively.

```java
for (int i = 1; i < 5; i++) { System.out.println(i); }

int sum = 0;
for (int i = 1; i <= 10; i++); { sum += i; }
System.out.println(sum);

int max = 0;
for (int i = 0; i < 3; i++) { int v = in.nextInt(); if (v > max) { max = v; } }
System.out.println("Max: " + max);
```

#### Ex 2.15 (E): Digit counter

Read a positive whole number and count its digits by repeatedly dividing by `10`. Print `Digits: <count>`. For `90210` the result is `Digits: 5`. Then compute and print `Digit sum: <sum>` (`Digit sum: 12` for `90210`).

#### Ex 2.16 (E): Guessing game

The secret number is `42` (fixed in the code). Read guesses until the user finds it. After each wrong guess print `Too low` or `Too high`. At the end print `Found it in <n> guesses`.

#### Ex 2.17 (X): Perfect numbers

Print all perfect numbers up to `10000` (equal to the sum of their proper divisors, e.g. `6 = 1 + 2 + 3`) on one line as `Perfect numbers: <values>`. The result is `Perfect numbers: 6 28 496 8128`.

#### Ex 2.18 (X): Collatz sequence

Read a positive `n`. While `n != 1`: if `n` is even, halve it; otherwise replace it with `3 * n + 1`. Print `Sequence: <values>` and `Steps: <count>` (number of transitions). For `n = 6`: `Sequence: 6 3 10 5 16 8 4 2 1` and `Steps: 8`.

### Daily practice (5 days)

One short exercise per day, about 15-20 minutes, in addition to the homework. They mix week 1 and 2 material (output, variables, arithmetic, `Scanner`, `printf`) with this week's decisions and loops. Use the exact labels shown so the programs can be checked automatically.

#### Day 1: Ticket price

Class: `TicketPrice`. Read an age (whole number). The price is `0` euros under 6, `5` euros from 6 to 17, `10` euros from 18 to 64, and `7` euros from 65. Print `Price: <price> euros`. Test every boundary: `5`, `6`, `17`, `18`, `64`, `65`.

Input `18` gives `Price: 10 euros`.

#### Day 2: Change in coins

Class: `ChangeInCoins`. Read an amount in cents (0 to 499). Print how many 200, 100, 50, 20, 10, 5, 2, and 1 cent coins are needed, using `/` and `%`, and only print the lines for coins that are used. Use the format `<coin> cent: <count>`.

Input `288` gives `200 cent: 1`, `50 cent: 1`, `20 cent: 1`, `10 cent: 1`, `5 cent: 1`, `2 cent: 1`, `1 cent: 1`.

#### Day 3: Savings plan

Class: `SavingsPlan`. Read a start amount in whole euros (`start`), a monthly deposit (`deposit`), and a goal. Use a `while` loop to count the months until the savings reach the goal. Print `Months: <n>` and the final balance with `printf("Balance: %.2f%n", ...)`. If the start amount already reaches the goal, print `Months: 0`.

Input `100 50 400` gives `Months: 6` and `Balance: 400.00`.

#### Day 4: Digit-sum table

Class: `DigitSumTable`. Read `n`. For each number from `1` to `n`, print one line `<number>: <digit sum>`; compute the digit sum with a `while` loop inside the `for` loop. At the end print `Highest digit sum: <value>`.

Input `12` prints `10: 1`, `11: 2`, `12: 3` among the lines and ends with `Highest digit sum: 9`.

#### Day 5: Mini quiz

Class: `MiniQuiz`. Write a number-guessing quiz. The secret number is `42`, fixed in the code. Ask `Guess:` up to 5 times. After each wrong guess print `Too low` or `Too high`. Stop as soon as the guess is right and print `Correct in <n> tries`. If all 5 guesses fail, print `Out of tries. The number was <secret>`. Test with a correct first guess, a correct last guess, and five wrong guesses.

### Homework

Two programs. Session 2 is dense, so finish the core exercises first.

#### Part A: `Statistics.java`

Class: `Statistics`. Read a count `n` (at least 1), then `n` whole numbers. Use a `for` loop and read each number once. Print exactly: `Count: <n>`, `Sum: <sum>`, `Min: <min>`, `Max: <max>`, `Average: <avg>` (one decimal digit via `printf("%.1f")`), `Even: <how many are even>`. Negative numbers are valid.

Input `5 4 9 2 8 -3` gives:

```text
Count: 5
Sum: 20
Min: -3
Max: 9
Average: 4.0
Even: 3
```

#### Part B: `AverageUntilZero.java`

Create `AverageUntilZero.java`. The program reads whole numbers from standard input until `0` is entered. It prints the count, sum, largest value, and the average of the numbers before the `0`.

Acceptance criteria:

* Read values with `Scanner` in a `while` loop; `0` ends the input and is not part of the data.
* If no numbers were entered before `0`, print `No numbers` and nothing else.
* Otherwise print exactly four lines: `Count: <n>`, `Sum: <sum>`, `Max: <max>`, `Average: <avg>`, where the average is printed with one decimal digit using `printf("%.1f")`.
* Negative numbers are valid values.
* Test with input `4 9 2 0`; the output should be:

   ```text
   Count: 3
   Sum: 15
   Max: 9
   Average: 5.0
   ```

The program can be checked automatically by supplying different inputs on standard input. Finish any open core exercises; extension and challenge exercises are optional.
