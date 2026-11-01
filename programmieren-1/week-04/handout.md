# Handout

## Week 4 Handout: Git and More Language Features

***

## Session 1: Introduction to Git

### 1. Why version control?

Git records snapshots of your project over time. It lets you see what changed and why, go back to a working state, work on several ideas in parallel, and collaborate without sending ZIP files around. In this course you will use it for all your code.

Git is the tool; **GitLab** is a website that hosts Git repositories. In this course, GitLab also checks your exercises automatically.

### 2. Key terms

| Term | Meaning |
| --- | --- |
| Repository (repo) | A project folder plus its full history, stored in a hidden `.git` folder |
| Working directory | The files as you see and edit them |
| Staging area | Changes you have selected for the next commit |
| Commit | A saved snapshot with an author, date, and message |
| Remote | A copy of the repo on a server, usually called `origin` |
| Branch | A named line of commits; the default is `main` |
| Pipeline | The automatic checks GitLab runs after every push |

Flow: edit files, then `git add` (stage), then `git commit` (save), then `git push` (upload).

### 3. One-time setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git --version
```

### 4. The daily commands

```bash
git clone <url>                # copy your GitLab project to your computer
git init                       # alternatively: create a repository in the current folder
git status                     # what changed? what is staged?
git add src/Hello.java         # stage one file
git add .                      # stage everything that changed
git commit -m "Add Hello world program"
git log --oneline              # compact history
git diff                       # unstaged changes
git diff --staged              # staged changes
```

A good commit is small, does one thing, and has a message in the imperative: `Add loop exercise 2.2`, not `stuff` or `changes`.

### 5. Ignoring files

Compiled files should not be committed. Create a file named `.gitignore`:

```text
*.class
out/
.idea/
.vscode/
```

A file that is already committed stays tracked. Remove it from Git (but keep it on disk) with `git rm --cached <file>`.

### 6. Undoing simple mistakes

```bash
git restore src/Hello.java            # discard unstaged edits to a file
git restore --staged src/Hello.java   # unstage a file, keep the edits
git commit --amend -m "Better message"   # fix the last commit (only if not pushed)
```

`git restore` on unstaged changes cannot be undone. Check `git status` first.

### 7. Working with a remote

```bash
git remote -v                  # show the remote (origin)
git push                       # upload your commits
git pull                       # download and merge new commits
git push -u origin main        # first upload of a new local repo
git remote add origin <url>    # connect a local repo to a remote
```

Typical workflow for an exercise: `git pull`, edit, `git status`, `git add`, `git commit`, `git push`.

### 8. Automatic checks with GitLab CI

After each `git push`, GitLab starts a **pipeline** (project page, menu *Build > Pipelines*). The file `.gitlab-ci.yml` in your repository defines it. For this course there is one job per exercise:

- A green check means the exercise passes.
- A red cross means a check failed. Open the job and read the message, for example `Wrong output for input: 7` or `Commit message too vague`.
- Fix the problem, commit, and push again. The pipeline runs again.

The checks run your program with prepared input and compare its output with the expected text, so class names, file names, and output text must match the exercise exactly. Test locally first, as shown in [tests/README.md](tests/README.md).

### 9. Common mistakes

- Running Git commands outside the repository folder (`fatal: not a git repository`).
- Forgetting to `git add` before `git commit`, so the commit is empty or incomplete.
- Forgetting to `git push`: GitLab only checks what you pushed.
- Committing generated files such as `.class` files.
- Vague messages like `fix` or `update`.
- Never committing until everything works. Commit small steps often.

***

## Session 2: More language features

### 1. The `do-while` loop

`while` tests the condition **before** the body, so the body may run zero times. `do-while` tests **after** the body, so it always runs at least once. Note the semicolon at the end.

```java
int number;
do {
    System.out.print("Enter a number (1-10): ");
    number = in.nextInt();
} while (number < 1 || number > 10);
```

Typical use: input validation and menus, where you must ask at least once. The variable must be declared **before** the loop, otherwise the condition cannot see it.

| Loop | Condition tested | Minimum runs | Use when |
| --- | --- | --- | --- |
| `for` | before | 0 | the number of repetitions is known |
| `while` | before | 0 | repeat until something happens |
| `do-while` | after | 1 | the body must run once first |

### 2. `break` and `continue`

`break` leaves the innermost loop immediately. `continue` skips the rest of the current pass and goes to the next one (in a `for` loop, the update still runs).

```java
for (int i = 1; i <= 100; i++) {
    if (i % 7 == 0) {
        System.out.println("First multiple of 7: " + i);
        break;
    }
}

for (int i = 1; i <= 10; i++) {
    if (i % 2 == 0) {
        continue;       // skip even numbers
    }
    System.out.println(i);
}
```

Use them sparingly. If a plain loop condition expresses the same idea clearly, prefer it.

### 3. Compound operators and increments

| Short form | Long form |
| --- | --- |
| `x += 3` | `x = x + 3` |
| `x -= 3` | `x = x - 3` |
| `x *= 2` | `x = x * 2` |
| `x /= 2` | `x = x / 2` |
| `x %= 5` | `x = x % 5` |
| `x++` / `++x` | `x = x + 1` |
| `x--` / `--x` | `x = x - 1` |

Use `x++` as a statement on its own. Avoid using the value inside larger expressions: `int y = x++;` stores the old value, `int y = ++x;` the new one.

### 4. `switch`

`switch` selects one of many branches by comparing one value (`int`, `char`, `String`, enum) with constants.

```java
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 6:
    case 7:
        System.out.println("Weekend");
        break;
    default:
        System.out.println("Another weekday");
}
```

Without `break`, execution **falls through** into the next case. This is a common bug. The `default` branch handles all other values.

Since Java 14 there is an arrow form with no fall-through:

```java
switch (day) {
    case 6, 7 -> System.out.println("Weekend");
    case 1 -> System.out.println("Monday");
    default -> System.out.println("Another weekday");
}
```

Use `switch` for equality against constants. Use `if` / `else if` for ranges.

### 5. Common mistakes

- Forgetting the `;` after `while (...)` in a `do-while`.
- Declaring the variable inside the `do { }` block and using it in the condition.
- Forgetting `break` in an old-style `switch`.
- Using `break` when you meant `continue`, or the reverse.
- An endless loop because the loop variable is never updated (or `continue` skips the update in a `while`).
- Printing extra text: the GitLab check compares the output exactly.
