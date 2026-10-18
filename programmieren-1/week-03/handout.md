# Handout

## Week 3 Handout: Decisions and Loops

Examples assume a class saved in a file with the same name, for example `Decisions.java`.

***

### 1. Boolean values and comparisons

A `boolean` is either `true` or `false`. Comparisons produce booleans:

| Operator | Meaning | Example (`age = 19`) | Result |
| --- | --- | --- | --- |
| `==` | equal to | `age == 18` | `false` |
| `!=` | not equal to | `age != 18` | `true` |
| `<`, `<=` | less than, at most | `age < 20` | `true` |
| `>`, `>=` | greater than, at least | `age >= 19` | `true` |

`=` assigns, `==` compares. Writing `if (age = 18)` is a compile error.

```java
boolean isAdult = age >= 18;
System.out.println(isAdult); // true
```

### 2. Logical operators

| Operator | Meaning | Example |
| --- | --- | --- |
| `&&` | and: both must be true | `age >= 18 && age < 65` |
| `\|\|` | or: at least one is true | `day == 6 \|\| day == 7` |
| `!` | not: flips the value | `!isOpen` |

Use parentheses when mixing operators: `&&` binds tighter than `||`.

### 3. `if`, `else if`, `else`

```java
if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else {
    System.out.println("Keep practicing");
}
```

Java checks the conditions from top to bottom and runs only the first branch whose condition is true. Always use braces, even for one statement. Order matters: check the most specific condition first.

Compare text with `equals`, never with `==`:

```java
if (answer.equals("yes")) { ... }
```

### 4. The `while` loop

A loop repeats a block while its condition is true.

```java
int count = 1;              // 1. initialise
while (count <= 3) {        // 2. test the condition
    System.out.println(count);
    count++;                // 3. update so the loop can end
}
```

Output: `1`, `2`, `3`. The condition is tested **before every pass**, so a loop can run zero times. If the update is missing, the loop never ends (an **infinite loop**; stop it with Ctrl+C).

### 5. Tracing a loop

To understand a loop, write a table with one row per pass:

```java
int sum = 0;
int i = 1;
while (i <= 4) {
    sum = sum + i;
    i++;
}
```

| Pass | `i` at test | Condition | `sum` after body | `i` after body |
| --- | --- | --- | --- | --- |
| 1 | 1 | true | 1 | 2 |
| 2 | 2 | true | 3 | 3 |
| 3 | 3 | true | 6 | 4 |
| 4 | 4 | true | 10 | 5 |
| test | 5 | false | | |

The loop ends with `sum == 10`.

### 6. Common loop patterns

**Accumulate** (sum, product): start with a neutral value (`0` for sum, `1` for product) and update it in each pass.

**Count** how many times something happens: `if (condition) { count++; }`.

**Read until a stop value (sentinel):**

```java
Scanner in = new Scanner(System.in);
int total = 0;
int value = in.nextInt();
while (value != 0) {
    total += value;
    value = in.nextInt();
}
System.out.println("Total: " + total);
```

**Validate input:** repeat the question while the answer is invalid.

```java
int age = in.nextInt();
while (age < 0) {
    System.out.print("Age must not be negative. Try again: ");
    age = in.nextInt();
}
```

### 7. From `while` to `for`

A counting `while` loop has three parts: initialise, test, update. The `for` loop puts them in one line:

```java
for (int i = 1; i <= 3; i++) {
    System.out.println(i);
}
```

This is equivalent to the `while` loop in section 4 and prints `1 2 3`. The header is `for (initialise; condition; update)`. Execution order: initialise once, test, run the body, run the update, test again. A variable declared in the header (`int i`) exists only inside the loop.

**Choosing the loop:** use `for` when the number of repetitions is known or computable (count to `n`); use `while` when you repeat until something happens (stop value, valid input, found).

| Goal | Header |
| --- | --- |
| `1` to `n` | `for (int i = 1; i <= n; i++)` |
| `0` to `n-1` (n passes) | `for (int i = 0; i < n; i++)` |
| `n` down to `1` | `for (int i = n; i >= 1; i--)` |
| every second number | `for (int i = 0; i <= 20; i += 2)` |

**Off-by-one check:** `i < 5` starting at `0` runs 5 times; `i <= 5` runs 6 times. Always test the first and last pass.

### 8. Patterns with `for` and `if`

**Count matches**

```java
int evens = 0;
for (int i = 1; i <= n; i++) {
    if (i % 2 == 0) {
        evens++;
    }
}
```

**Minimum / maximum:** start with the first value, not with `0`.

```java
int max = in.nextInt();
for (int i = 1; i < n; i++) {
    int value = in.nextInt();
    if (value > max) {
        max = value;
    }
}
```

**Search with a flag:** set `boolean found = false;` before the loop and set it to `true` inside an `if` when the target is seen.

Print on one line with `System.out.print(x + " ")` and finish with `System.out.println()`.

### 9. Common mistakes

- Putting a `;` right after `for (...)`, which makes the body empty.
- Initialising `max` or `min` with `0` when values can be negative.
- Changing the loop variable inside a `for` body.
- Using the loop variable after the loop (it is out of scope).
- Using `=` instead of `==` in a condition.
- Forgetting the update, which creates an infinite loop.
- Off-by-one errors: `<` versus `<=` in the loop condition.
- Comparing strings with `==` instead of `equals`.
- Declaring a variable inside the loop when it is needed after it.
