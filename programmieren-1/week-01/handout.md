# Handout

## Week 1 Handout: First Programs

Read the relevant section before you start each exercise. This handout is self-contained: everything you need for Week 1 is explained here.

***

### 1. What is a program?

A **program** is a list of instructions that a computer carries out one after another, from top to bottom. A computer only understands very simple instructions in binary form (machine code). Humans write programs in a **programming language**, which is readable text. A tool then translates that text into something the computer can run.

The text you write is called **source code**. It is stored in an ordinary text file.

### 2. How Java works: source, bytecode, JVM

Java uses two steps:

```
Hello.java  --javac-->  Hello.class  --java-->  output on screen
(source code)  (compiler)  (bytecode)  (JVM)
```

1. **Compiling:** the compiler `javac` reads your `.java` file and checks it for mistakes. If it finds none, it creates a `.class` file containing **bytecode**. If it finds mistakes, it prints error messages and creates **no** `.class` file.
2. **Running:** the command `java` starts the **Java Virtual Machine (JVM)**. The JVM reads the `.class` file and executes it.

Consequences:

* Every time you change the `.java` file, you must compile again. Otherwise `java` runs the old `.class` file.
* `.class` files are generated. You never edit them.
* `javac` takes a **filename** (with `.java`). `java` takes a **class name** (without `.class`).

The **JDK** (Java Development Kit) contains both `javac` and `java`. The "Extension Pack for Java" in VS Code adds editor features such as colouring, error underlines and a debugger. It does not replace the JDK.

### 3. The terminal

A **terminal** lets you type commands instead of clicking. In VS Code, open it with the menu **Terminal > New Terminal**. It starts in your project folder.

Important ideas:

* The terminal always has a **current folder** ("working directory"). Commands such as `javac Hello.java` look for the file **in the current folder**.
* Useful commands (Windows PowerShell / macOS / Linux):

| Purpose                          | Windows         | macOS / Linux   |
| -------------------------------- | --------------- | --------------- |
| Show files in the current folder | `dir`           | `ls`            |
| Change into a folder             | `cd foldername` | `cd foldername` |
| Go one folder up                 | `cd ..`         | `cd ..`         |
| Show the current folder          | `pwd`           | `pwd`           |
| Delete a file                    | `del file`      | `rm file`       |

* If a folder name contains **spaces**, the terminal thinks the space separates two things. Wrap such names in double quotes: `cd "my folder"`.
* Pressing the **Up arrow** key brings back the previous command.
* Check your installation with `java -version` and `javac -version`. Both must print a version number. If one says "command not found" or "not recognized", the JDK is not installed correctly or not in the PATH.

### 4. Anatomy of a Java program

Every Java program in this course starts with this frame:

```java
public class Hello {
    public static void main(String[] args) {
        // instructions go here
    }
}
```

What the parts mean (for now, accept the details and learn them fully in later weeks):

* `public class Hello { ... }` defines a **class** called `Hello`. In Java, all code lives inside classes. Everything between the matching `{` and `}` belongs to the class.
* `public static void main(String[] args) { ... }` is the **main method**. When you run `java Hello`, the JVM looks for exactly this line and starts executing the instructions inside its braces, from top to bottom. You must write it exactly like this, including capitalisation.
* `{ }` **curly braces** group things together. Each `{` needs a matching `}`. Indenting the lines inside braces makes this visible. The compiler does not need indentation, but humans do.
* `;` a **semicolon** ends an instruction (called a **statement**). Think of it as the full stop of a sentence.

#### Rules you must know

1. **Case matters.** `System` and `system` are different words. `Main` and `main` are different.
2. **The filename must match the public class name.** A class `public class Greeter` must be saved as `Greeter.java`, with the same upper and lower case letters.
3. **One statement after the other.** Instructions are executed in the order they are written.
4. **Statements go inside methods.** You cannot put an instruction directly inside the class body outside a method. Only methods (and, later, fields) belong there.
5. **Whitespace is flexible.** Extra spaces and blank lines don't change the meaning. A single statement can even be split over several lines.

### 5. Printing text

To show text on the screen, use:

```java
System.out.println("some text");
System.out.print("some text");
```

* `System.out` is the standard output (the terminal window).
* `println` means "print line": it prints the text and then moves to the **next line**.
* `print` prints the text and stays on the **same line**. The next output continues directly behind it.
* The parentheses `( )` contain what to print. The statement ends with `;`.
* Calling `println()` with nothing between the parentheses prints just an empty line.

Think of the output as a typewriter: `print` types, `println` types and then presses Enter.

#### Strings

Text in quotes is called a **string**. `"Hello"` is a string. The quotes are not part of the text. They mark where it starts and ends. Everything inside the quotes is printed exactly as written, including spaces.

Pay attention to spaces. If you print `"Java"` and then `"is"` with two `print` calls, they are glued together as `Javais`, because nothing adds a space for you.

#### Text art and monospace fonts

The terminal uses a **monospace font**: every character, including space, has the same width. This is why you can build pictures and tables from characters. To draw something:

1. Sketch it on paper, character by character, in a grid.
2. Each row becomes one `println`.
3. Count spaces carefully. Leading spaces at the start of a string are printed too.

### 6. Escape sequences

Some characters cannot be written directly inside a string. For example, a double quote would end the string. For these cases Java uses a **backslash `\`** followed by a letter or symbol. The two characters together stand for one special character:

| Written in code | Meaning                                                       |
| --------------- | ------------------------------------------------------------- |
| `\n`            | new line (like pressing Enter)                                |
| `\t`            | tab (jumps to the next tab stop, useful for aligning columns) |
| `\"`            | a double quote character                                      |
| `\\`            | one single backslash                                          |

Key points:

* The backslash is special in strings. To print a backslash itself, you need to "escape" it with another backslash.
* `\n` inside `print` has the same effect as ending a line.
* Escape sequences are only interpreted **inside quotes**.
* A tab does not always equal the same number of spaces. It aligns to columns, so `\t` is good for simple tables.

### 7. Comments

A **comment** is text for humans. The compiler ignores it completely.

```java
// This is a single-line comment. It ends at the end of the line.

/* This is a block comment.
   It can span several lines. */
```

Uses:

* explaining why code does something
* **commenting out** code: temporarily disabling a statement by putting `//` in front of it. The program then behaves as if the line did not exist.

In VS Code, select lines and press **Ctrl + /** to toggle `//` comments.

### 8. Errors

Mistakes are normal and every programmer makes them constantly. Learning to read error messages is one of the most important skills in this course.

#### Kinds of errors

* **Compile-time error (syntax error):** found by `javac` before the program runs. No `.class` file is created.
* **Runtime error:** the program starts but crashes while running. Example: `java` cannot find the class you named.
* **Logic error:** the program runs but does something other than what you wanted. The computer cannot detect this. You find it by testing.

#### Reading a compiler message

A compiler message typically looks like this:

```
Hello.java:3: error: ';' expected
        System.out.println("Hi")
                                ^
1 error
```

It tells you:

1. the **file** and **line number** (`Hello.java:3`)
2. a short **description** of the problem
3. the **line itself**, with a `^` marking the position where the compiler noticed the problem
4. the **number of errors**

Tips:

* Always read the **first** error first. Later errors are often follow-ups of the first. Fix it, recompile, and the others often vanish.
* The reported line is where the compiler **noticed** the problem. The real cause is sometimes the line before.
* Check the usual suspects: missing `;`, missing or extra `{` / `}`, missing closing `"`, wrong capitalisation, misspelled word.

#### Common messages and their general meaning

| Message (shortened)                                            | Typical cause                                                                  |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `';' expected`                                                 | a statement is not ended with a semicolon                                      |
| `cannot find symbol`                                           | Java does not know a name. Often a typo or wrong capitalisation                |
| `reached end of file while parsing`                            | a `}` is missing                                                               |
| `unclosed string literal`                                      | an opening `"` has no closing `"`                                              |
| `class X is public, should be declared in a file named X.java` | the filename does not match the class name                                     |
| `class, interface, enum, or record expected`                   | something is written outside a class, or there are too many `}`                |
| `illegal start of expression` / `not a statement`              | the line is not a valid statement                                              |
| `Could not find or load main class X` (when running)           | wrong class name given to `java`, wrong folder, or no `.class` file exists yet |
| `Error: Main method not found`                                 | the `main` line is missing or misspelled                                       |

When you deliberately create an error in an exercise, compare what you see with this table, then note what you observed in your own words.

### 9. The workflow, step by step

1. Write the code in VS Code and **save** (Ctrl + S). Unsaved changes are not seen by `javac`.
2. In the terminal, make sure you are in the folder containing the file (check with `dir` or `ls`).
3. Compile: `javac Filename.java`
   * No output means success.
   * Messages mean errors. Fix them and repeat.
4. Run: `java ClassName`
5. Change the code, save, compile again, run again.

Quick check: after a successful compile, `dir` / `ls` shows a new `.class` file next to your `.java` file.

#### Several files in one folder

* You may have several `.java` files in the same folder, each with its own class and its own `main` method.
* Compile one: `javac A.java`. Compile all at once with a wildcard: `javac *.java` (`*` means "anything").
* Run each class separately: `java A`, then `java B`.

#### Running a source file directly

Since newer Java versions, you can skip the compile step for a single-file program:

```
java Hello.java
```

Here `java` is given the **source file** (with `.java`). It compiles in memory and runs immediately. This is convenient for quick tests, but afterwards no `.class` file exists on disk. This differs from the normal two-step workflow.

#### Choosing where the compiled files go

`javac` has **options** that are written between the command and the filename. Options start with `-`:

* `-d foldername` puts the generated `.class` files into the given folder instead of next to the source.
* `java -cp foldername ClassName` tells the JVM where to look for class files. `-cp` stands for **class path**.

You can ask the tools for their options with `javac --help` and `java --help`. Reading such help text is a skill you will need.

### 10. Printing with a format (`printf`)

Besides `println`, there is `System.out.printf`. It prints a **template** text with **placeholders** that are filled from the values after it.

```java
System.out.printf("template with placeholders", value1, value2);
```

* A placeholder starts with `%` and a letter that says what kind of value goes there:

| Placeholder | Kind of value                                                |
| ----------- | ------------------------------------------------------------ |
| `%s`        | a string (text)                                              |
| `%d`        | a whole number (integer)                                     |
| `%n`        | not a value. It stands for a platform-independent line break |

* Values are inserted **in order**: the first placeholder takes the first value, the second takes the second, and so on.
* The number of placeholders should equal the number of values.
* `printf` does not add a line break by itself. You have to write `%n` where you want one.

### 11. Text versus numbers

Java distinguishes **text** from **numbers**:

* `2` (no quotes) is a number. `"2"` (with quotes) is text that happens to contain a digit.
* The operator `+` between two numbers **adds** them.
* The operator `+` where at least one side is a string **joins** them (concatenation) into one longer text.
* Java evaluates `+` from left to right. So the order of numbers and strings in an expression matters.
* Anything inside quotes is never calculated. It is just text.

A number given directly to `println` is printed as its value.

### 12. Using the VS Code debugger

A **debugger** lets you run a program step by step and watch what happens. This is helpful for understanding the order of execution.

Concepts:

* A **breakpoint** is a marker on a line. When the program reaches that line, it **pauses before executing it**. Set one by clicking in the margin to the left of the line number. A red dot appears.
* When paused, the highlighted line is the **next** one to be executed.
* **Step Over** (F10) executes the current line and pauses on the next.
* **Continue** (F5) runs until the next breakpoint or the end.
* **Stop** (Shift + F5) ends the debug session.

To start: open the file, then use the **Run and Debug** option in VS Code, or the "Debug" action that appears above the `main` method. Watch the Terminal / Debug Console panel to see output appear line by line as you step.

### 13. Working habits

* **Type the code yourself.** Don't copy and paste. Typing teaches you the syntax.
* **Make small changes, then compile.** Don't write 50 lines before compiling.
* **Read the error message**, aloud if needed. It usually tells you where to look.
* **Predict before you run.** Before executing, guess what the output will be. Compare afterwards. Differences are where you learn.
* **Keep your files organised.** One folder per week, filenames that match the class names.

### 14. Quick reference

| I want to...                                     | I write...                                        |
| ------------------------------------------------ | ------------------------------------------------- |
| compile a file                                   | `javac Name.java`                                 |
| run a class                                      | `java Name`                                       |
| compile all files in the folder                  | `javac *.java`                                    |
| run a single source file directly                | `java Name.java`                                  |
| print and continue on the same line              | `System.out.print("...");`                        |
| print and go to the next line                    | `System.out.println("...");`                      |
| write a comment                                  | `// ...` or `/* ... */`                           |
| show a quote / backslash / tab / newline in text | `\"`, `\\`, `\t`, `\n`                            |
| print with placeholders                          | `System.out.printf("... %s ... %d ...%n", a, b);` |
| see my files                                     | `dir` (Windows), `ls` (macOS / Linux)             |
| show tool options                                | `javac --help`, `java --help`                     |

### 15. Glossary

* **Bytecode:** the compiled form of Java code, stored in `.class` files.
* **Class:** the container for Java code. In Java, every program is made of classes.
* **Compiler:** the tool that translates and checks source code (`javac`).
* **Debugger:** the tool to run code step by step.
* **JDK:** the Java Development Kit, which includes `javac` and `java`.
* **JVM:** the Java Virtual Machine, which executes bytecode (`java`).
* **Method:** a named block of instructions. `main` is the starting method.
* **Statement:** one instruction, ended with `;`.
* **String:** text in double quotes.
* **Syntax:** the grammar rules of the language.
* **Terminal:** the text window where you type commands.
