# Exercises

## Week 1: First Programs

**Goals:** compile and run with `javac` / `java`, read compiler errors, use `System.out`.

**Tiers:** **C** = core (everyone), **E** = extension (fast students / homework), **X** = challenge (optional, no hints).

### Pre-class checklist

1. Install a JDK (latest Version) and VS Code with the "Extension Pack for Java".
2. In a terminal, `java -version` and `javac -version` both print a version.
3. Create the folder `iprog/week01`.

***

### Session 1

Time plan: 0-5 min setup fixes, 5-35 min exercises, 35-42 min quiz, 42-45 min wrap-up.

#### Ex 1.1 (C): Hello World

Create `Hello.java`:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Run `javac Hello.java`, then `java Hello`. Check that `Hello.class` now exists.

#### Ex 1.2 (C): Change it

Print your name and your study program on two separate lines.

#### Ex 1.3 (C): `print` vs. `println`

Print `Java is fun` on one line using three `print` calls. Fix the spacing.

#### Ex 1.4 (C): Break it on purpose

Introduce each error one at a time, compile, and note the message and line number:

* remove a `;`
* write `System.out.printn(...)`
* remove a closing `}`
* change the class name but not the filename

#### Ex 1.5 (C): Escape sequences

Print this exactly, using `\t`, `\"` and `\\`:

```
Name:	Ada
"Quote"
C:\temp
```

#### Ex 1.6 (C): ASCII art

Print a 5-line house or a smiley using only `println`.

#### Ex 1.7 (C): Initials

Print your own initials as big block letters using `*`.

#### Ex 1.8 (C): Indented poem

Print a 3-line poem, each line indented with a different number of spaces.

#### Ex 1.9 (C): Missing class file

Compile `Hello.java`, delete `Hello.class`, then run `java Hello`. Read the error and explain it in a comment.

#### Ex 1.10 (E): Source-file mode

Run `java Hello.java` directly. Compare it with `javac` + `java` and note what is missing afterwards.

#### Ex 1.11 (E): Code outside the class

Add a `println` call after the closing brace of `main` (inside the class, outside the method). Compile it and interpret the error.

#### Ex 1.12 (X): Chessboard

Print a 7 x 7 chessboard-like pattern of `#` and `.` using only `println`.

***

### Session 2

#### Ex 2.1 (C): Comments

Add a `//` comment and a `/* ... */` comment to a program. Confirm they don't change the output. Comment out one `println`.

#### Ex 2.2 (C): Predict, then run

Write down the output before running:

```java
System.out.print("A");
System.out.println("B");
System.out.print("C\n");
System.out.println();
System.out.println("D");
```

#### Ex 2.3 (C): Business card

Print a framed card:

```
+----------------+
| Ada Lovelace   |
| Student, IPROG |
+----------------+
```

#### Ex 2.4 (C): Two classes, one folder

Create `A.java` and `B.java`, each with `main` and a different message. Compile both with `javac *.java` and run each one.

#### Ex 2.5 (C): Find the bugs

This program has 4 errors. Fix them:

```java
public class Broken {
    public static void main(String[] args) {
        System.out.println("Start")
        system.out.println("Middle");
        System.out.println("End);
    }
}
```

#### Ex 2.6 (C): Debugger preview

In VS Code, set a breakpoint on a `println`. Run with "Debug Java" and step over each line.

#### Ex 2.7 (C): Multiplication table

Print the multiplication table for 1 to 3 as text lines. Type the results yourself (no arithmetic yet).

#### Ex 2.8 (C): Date formats

Print today's date in three formats on three lines.

#### Ex 2.9 (C): Escapes combined

Predict the output of a program that uses `\n`, `\t`, `\\` and `\"` together, then verify.

#### Ex 2.10 (E): Text vs. arithmetic

Compare `System.out.println(2 + 3);` and `System.out.println("2 + 3");`. Then try `"2" + 3`.

#### Ex 2.11 (E): `printf`

Use `System.out.printf("%s is %d years old%n", "Ada", 36);`. Change the values and guess what `%s`, `%d` and `%n` mean.

#### Ex 2.12 (E): Folder with a space

Put your program in a folder with a space in its name. What breaks in the terminal? Fix it with quotes.

#### Ex 2.13 (X): Output folder

Find the `javac` option that sets the output folder (`-d`). Compile so that the `.class` files go into `out/`, then run from there with `-cp`.

#### Ex 2.14 (X): Pair debugging

Break a classmate's program with one subtle change. They find it using only the compiler message.

***

### Homework

1. **H1.1:** Write `About.java`, which prints a 6-line self-introduction (name, hometown, hobby, favourite food, why you study this, one fun fact).
2. **H1.2:** Print a table with a header and 3 rows, using `\t` for alignment.
3. **H1.3:** Draw a larger ASCII-art figure (at least 8 lines), such as a tree or a rocket.
4. **H1.4:** Deliberately cause 3 different compile errors. Above each one, write a comment in your file explaining what the compiler said.
5. **H1.5 (bonus):** Print the lyrics of a short song verse using only `println`. Note what you wish you had to reduce the repetition. This leads into variables and loops.
6. Finish any open extension (E) and challenge (X) exercises from the sessions.
