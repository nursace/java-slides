# Introduction to Programming with Java

**Lab 04 — Classes and Objects**  
*Aligned with Lecture 04 (`04-classes-and-objects.tex`). Code-writing practice.*

## Learning goals

By finishing this lab you should be able to:

- Distinguish a **class** (blueprint) from an **object** (instance)
- Declare **fields** and initialise them with **constructors**
- Create objects with **`new`** and call **instance methods**
- Work with **several objects**, each with its own state
- Explain **references** and aliasing (`b = a`)

---

## Instructions

- For most exercises you will write **two files**: a model class (e.g. `Book.java`) and a small driver with `main` (e.g. `BookDemo.java`), **or** put `main` in a separate class named in the exercise. Follow the suggested names.
- Use **instance** fields and **instance** methods (not `static` helpers for object state). `main` may be `static` as usual.
- Constructors: same name as the class, **no return type**.
- You may use `this.field = parameter` when names clash (as in Lecture 04).
- **Do not** use inheritance (`extends`), interfaces, or `ArrayList` yet.
- **Do not** require full encapsulation for this lab: fields may be package-visible or `public` unless an exercise asks otherwise. (Private fields + getters are Lecture 05.)
- Compile and run. Match sample output **labels and line breaks** where given.
- Light hints only — **no full solutions**.

**Allowed reminders**

- `Type var = new Type(...);` creates an object and stores a reference
- Instance call: `object.method(...)`
- `=` between object variables copies the **reference**, not a deep copy of fields

---

## Exercises

### Exercise 1 — Minimal class and `new`

Create `Dog.java` with fields:

- `String name`
- `int age`

No constructor yet. Create `DogDemo.java` with `main` that:

1. Creates two dogs with `new Dog()`
2. Sets their fields directly
3. Prints each dog’s name and age on its own line

**Sample** (if you chose Rex/3 and Bella/5):

```text
Rex 3
Bella 5
```

**Hint:** Declaring `Dog d;` does not create an object — you need `new`.

---

### Exercise 2 — Constructor for `Student`

Create `Student.java` with:

- Fields: `String name`, `int id`
- Constructor: `public Student(String name, int id)` that sets both fields (use `this` if parameter names match)

Create `StudentDemo.java` that constructs at least two students and prints  
`name + " #" + id` for each.

**Sample:**

```text
Ada #1001
Alan #1002
```

**Hint:** After you add this constructor, `new Student()` with no arguments will not compile unless you also add a no-arg constructor.

---

### Exercise 3 — Instance method `printSummary`

Extend your `Student` class (or copy into a fresh pair of files) with:

```java
public void printSummary()
```

that prints one line: `<name> (id <id>)`.

In `main`, create two students and call `printSummary()` on each. **Do not** print the fields from `main` directly for this exercise—use the method.

**Sample:**

```text
Ada (id 1001)
Alan (id 1002)
```

**Hint:** Inside an instance method you can use `name` and `id` (or `this.name`) for *this* object’s fields.

---

### Exercise 4 — `Rectangle`: fields, constructor, methods

Create `Rectangle.java` with:

- Fields: `double width`, `double height`
- Constructor `Rectangle(double width, double height)`
- `public double area()` — returns `width * height`
- `public double perimeter()` — returns `2 * (width + height)`
- `public void printInfo()` — prints width, height, area, perimeter on separate labelled lines

In `RectangleDemo.main`, create two different rectangles and call `printInfo()` for each.

**Sample shape** (for 3.0 by 4.0):

```text
width: 3.0
height: 4.0
area: 12.0
perimeter: 14.0
```

**Hint:** `area` / `perimeter` should **return** values; `printInfo` can call them.

---

### Exercise 5 — `Counter`: independent object state

Create `Counter.java` as in Lecture 04:

- Field: `int value`
- Constructor sets `value` to `0`
- `public void hit()` increases `value` by 1
- `public int getValue()` returns `value`
- Optional: `public void reset()` sets `value` back to `0`

In `CounterDemo.main`:

1. Create `c1` and `c2`
2. Call `hit` twice on `c1` and once on `c2`
3. Print both values
4. `reset` `c1` and print again

**Expected after step 3:**

```text
c1: 2
c2: 1
```

**Hint:** Each object has its own `value`. Hitting `c1` must not change `c2`.

---

### Exercise 6 — Aliasing: same object, two variables

Create `AliasDemo.java` (you may reuse `Student`).

In `main`:

```java
Student a = new Student("Ada", 1);
Student b = new Student("Alan", 2);
b = a;
b.name = "Augusta";
System.out.println(a.name);
System.out.println(b.name);
```

1. Run and record the output.
2. In a comment block (4–6 sentences), explain:
   - Why both printed names match after `b = a`
   - What happened to the object that used to be referenced only by `b`
   - How this differs from copying an `int` with `=`

**Expected output:**

```text
Augusta
Augusta
```

**Hint:** Lecture 04 — assignment copies the reference for objects.

---

### Exercise 7 — `BankAccount` (simple instance API)

Create `BankAccount.java` with:

- Field: `double balance` (visibility as you prefer for this lab)
- Constructor `BankAccount(double start)` — if `start < 0`, store `0` instead
- `public void deposit(double amount)` — add only if `amount > 0`
- `public boolean withdraw(double amount)` — subtract and return `true` if `amount > 0` and `amount <= balance`; otherwise leave balance unchanged and return `false`
- `public double getBalance()`

In `BankDemo.main`, demonstrate: start at 100, deposit 50, successful withdraw 30, failed withdraw 1000, print balance and the boolean results.

**Sample shape:**

```text
after deposit: 150.0
withdraw 30: true
withdraw 1000: false
balance: 120.0
```

**Hint:** Keep rules inside the methods so `main` only calls them and prints.

---

### Exercise 8 — Mini project: `Book` + shelf in `main`

Create `Book.java` with:

- Fields: `String title`, `String author`, `int pages`
- Constructor setting all three
- `public String label()` returning `"<title> by <author> (<pages>p)"`
- `public boolean isLong()` returning `true` if `pages >= 300`

Create `LibraryDemo.java` that:

1. Creates an array `Book[] shelf` of length 3 (fixed array is fine)
2. Fills it with three different books
3. Prints every book’s `label()`
4. Prints how many books are long (`isLong`)

**Sample shape:**

```text
Dune by Frank Herbert (412p)
...
Long books: 2
```

**Hint:** Loop over the array; call instance methods on `shelf[i]`.

---

### Exercise 9 — Stretch (optional): two constructors

Add to `Book` (or a class `Movie`):

- A second constructor that only takes `title` and `author`, and sets `pages` to `0`
- In a short comment: what happens to Java’s automatic no-arg constructor once you write any constructor?

Demonstrate both constructors from `main`.

---

Submit `.java` sources. Put your name in a comment at the top of each file.

---

## Mapping to Lecture 04

| Lab focus | Lecture topic |
|-----------|----------------|
| Ex 1 | Class vs object; fields; `new` |
| Ex 2–3 | Constructors; instance methods |
| Ex 4–5 | Per-object state; Counter-style design |
| Ex 6 | References / aliasing |
| Ex 7–8 | Small realistic classes; arrays of objects |
| Ex 9 | Multiple constructors |
