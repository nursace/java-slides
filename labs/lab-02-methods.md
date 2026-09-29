# Introduction to Programming with Java

**Lab 03 — Methods**  

## Instructions

- Work in **one class per exercise** (unless an exercise says you may reuse helpers). Suggested class names are given.
- Methods should be `public static` for now (same style as Lecture 03), callable from `main` without objects.
- You may use arrays and `String` methods you already know from Lecture 02 when an exercise needs them.
- **Do not** introduce your own classes/objects beyond the one class with `main` (that is Lecture 04).
- Compile and run. Where sample I/O is shown, match the **labels and line breaks**; exact spacing of numbers is fine if readable.
- Hints are light. **No full solutions** are provided—ask the lecturer/TA if stuck after trying the hint.

**Allowed reminders**

- Header shape: `public static ReturnType name(Type p1, Type p2) { ... }`
- `void` methods print or update via side effects; non-`void` methods should `return` a value
- Overloading: different parameter lists—not return type alone

---

## Exercises

### Exercise 1 — Greet and farewell (`void`)

Write a class `Greeter`.

Implement:

```java
public static void greet(String name)
public static void farewell(String name)
```

- `greet` prints exactly one line: `Hello, <name>!`
- `farewell` prints exactly one line: `Goodbye, <name>!`

From `main`, call both for at least two different names.

**Sample** (if you call with `"Ada"` then `"Alan"` for greet, then farewell for `"Ada"`):

```text
Hello, Ada!
Hello, Alan!
Goodbye, Ada!
```

**Hint:** Parameters receive the argument values; use string concatenation in `println`.

---

### Exercise 2 — Arithmetic helpers (return values)

Write a class `Calc`.

Implement:

```java
public static int add(int a, int b)
public static int multiply(int a, int b)
public static double divide(int a, int b)
```

Rules:

- `add` / `multiply` return the obvious results.
- `divide` returns a **floating** result (`(double) a / b`). If `b == 0`, return `0.0` and also print one line `division by zero` before returning.

In `main`, call each method at least twice with different arguments and print results with clear labels.

**Sample** (illustrative):

```text
add(3,5) = 8
multiply(4,6) = 24
divide(7,2) = 3.5
division by zero
divide(7,0) = 0.0
```

**Hint:** Returning a value is different from printing inside the helper—here `divide` is allowed to print only for the zero case.

---

### Exercise 3 — Predicates: even, in range

Write a class `Predicates`.

Implement:

```java
public static boolean isEven(int n)
public static boolean inRange(int value, int lo, int hi)
```

- `isEven` returns `true` when `n` is divisible by 2.
- `inRange` returns `true` when `lo <= value && value <= hi` (assume `lo <= hi`).

In `main`, test several cases (including boundaries) and print results like:

```text
isEven(10) -> true
isEven(7) -> false
inRange(5, 1, 10) -> true
inRange(0, 1, 10) -> false
```

**Hint:** Return the boolean expression directly; do not print inside these two methods.

---

### Exercise 4 — Array statistics

Write a class `Stats`.

Assume a non-empty `int[]`. Implement:

```java
public static int sum(int[] values)
public static double average(int[] values)
public static int max(int[] values)
```

- `average` should use `sum` (call your own method—do not duplicate the loop).
- `max` returns the largest element.

In `main`, hard-code an array such as `{80, 90, 70, 100}` and print sum, average, and max.

**Sample:**

```text
sum = 340
average = 85.0
max = 100
```

**Hint:** Lecture 03’s grade helper used a similar average loop. Keep `main` thin.

---

### Exercise 5 — String utility: vowels and clamp label

Write a class `TextTools`.

Implement:

```java
public static int countVowels(String s)
public static String gradeLabel(double average)
```

- `countVowels`: count letters `a,e,i,o,u` in either case (`A` counts). Other characters ignored.
- `gradeLabel`: return `"Excellent"` if `average >= 90`, `"Good"` if `average >= 70`, otherwise `"Keep practising"` (same idea as Lecture 03).

In `main`, demonstrate both with at least two different inputs each.

**Sample:**

```text
countVowels("Education") = 5
gradeLabel(85.0) = Good
```

**Hint:** Loop with `charAt`; compare lowercase version of each character, or check both cases.

---

### Exercise 6 — Scope detective (write + explain)

Write a class `ScopeDemo`.

1. Write a method `public static int bump(int n)` that sets `n = n + 10` inside the method and returns `n`.
2. In `main`:

```java
int x = 5;
int y = bump(x);
System.out.println("x = " + x);
System.out.println("y = " + y);
```

3. Below your code (comment block in the source file, 3–5 sentences), answer:
   - Why is `x` still `5` after calling `bump`?
   - Where do the local variables of `bump` live?

**Expected output:**

```text
x = 5
y = 15
```

**Hint:** Lecture 03 — pass-by-value for `int`: the method receives a copy.

---

### Exercise 7 — Overloading `max`

Write a class `MaxOverload`.

Implement three overloaded methods:

```java
public static int max(int a, int b)
public static int max(int a, int b, int c)
public static double max(double a, double b)
```

- Two-argument versions return the larger value.
- Three-argument `int` version should reuse `max(int,int)` (no giant nested `if` tree required).

In `main`, call each overload at least once and print results.

**Sample:**

```text
max(3, 8) = 8
max(3, 8, 5) = 8
max(2.5, 2.7) = 2.7
```

**Hint:** Overloading is distinguished by parameter lists, not by return type alone.

---

### Exercise 8 — Mini program: grade report (put it together)

Write a class `GradeReport`.

Reuse ideas from earlier exercises (you may copy your own methods into this class):

- `average(int[] scores)`
- `gradeLabel(double average)`
- `public static void printReport(String courseName, int[] scores)` — **`void`** method that:
  1. Prints the course name
  2. Prints the average
  3. Prints the label from `gradeLabel`
  4. Prints how many scores are strictly above the average (write a small helper or a loop inside `printReport`)

`main` should create two different courses (two arrays) and call `printReport` for each.

**Sample shape** (numbers depend on your arrays):

```text
Course: CS101
Average: 85.0
Label: Good
Above average: 2

Course: CS102
Average: 92.5
Label: Excellent
Above average: 1
```

**Hint:** Prefer returning values from helpers; keep printing in `printReport` / `main`.
