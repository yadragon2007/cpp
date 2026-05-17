# C++ Programming — Selection (Chapter 4)

---

## 1. Flow of Control

**Flow of control** is the order in which a program's statements are executed. By default, execution is **sequential** (top to bottom).

Two mechanisms let you alter this default flow:

- **Selection** — picks which statement to execute next (covered here)
- **Repetition** — repeats a set of statements (loops, covered later)

Both mechanisms rely on **Boolean expressions** built with relational and logical operators.

---

## 2. Operators & Precedence

### Relational Operators

| Operator | Meaning |
|----------|---------|
| `<`  | Less than |
| `<=` | Less than or equal to |
| `>`  | Greater than |
| `>=` | Greater than or equal to |
| `==` | Equal to |
| `!=` | Not equal to |

### Logical Operators

| Operator | Meaning |
|----------|---------|
| `&&` | Logical AND |
| `\|\|` | Logical OR |
| `!`  | Logical NOT |

### Precedence Table (high → low)

| Operators | Associativity |
|-----------|---------------|
| `!`  `unary -`  `++`  `--` | Right to left |
| `*`  `/`  `%` | Left to right |
| `+`  `-` | Left to right |
| `<`  `<=`  `>`  `>=` | Left to right |
| `==`  `!=` | Left to right |
| `&&` | Left to right |
| `\|\|` | Left to right |
| `=`  `+=`  `-=`  `*=`  `/=` | Right to left |

---

## 3. Resolving Negations (De Morgan's Laws)

Use these rules to simplify or eliminate `!` operators:

```
!(E1 && E2)  →  (!E1) || (!E2)
!(E1 || E2)  →  (!E1) && (!E2)
!(E1 <= E2)  →  E1 > E2
!(E1 >= E2)  →  E1 < E2
```

---

## 4. Compound Statement (Block)

A **block** groups multiple statements so they are treated as one unit.

```cpp
{
    statement1;
    statement2;
    // ...
    statementN;
}
```

- Enclosed in `{ }` (curly braces)
- Each statement inside ends with `;`
- Statements execute **sequentially**

---

## 5. The `if` Statement

### Syntax

```cpp
if (boolean_expression)
{
    statement1;
    statement2;
    // ...
}
```

### How It Works

- If the expression is **true** → the body executes
- If the expression is **false** → the body is **skipped**
- Either way, execution continues at the next statement after the `if`

### Examples

```cpp
// Simple (single statement — braces optional but recommended)
if (count <= 100)
    count++;

// Compound (swap x and y if x > y)
x = 50; y = 20;
if (x > y)
{
    temp = x;
    x = y;
    y = temp;
}

// Divisibility check
if (x % y == 0)
    cout << "x is divisible by y" << endl;
```

---

## 6. The `if-else` Statement

### Syntax

```cpp
if (boolean_expression)
{
    // true branch
    statement1;
}
else
{
    // false branch
    statement2;
}
```

### How It Works

- Expression **true** → true branch executes, false branch skipped
- Expression **false** → false branch executes, true branch skipped
- Control always continues after the entire `if-else`

### Example

```cpp
if (x % y == 0)
    cout << "x is divisible by y";
else
    cout << "x is not divisible by y";
```

### Rewriting `if-else` Using Only `if`

```cpp
// Equivalent to the if-else above
if (x % y == 0)
    cout << "x is divisible by y" << endl;
if (x % y != 0)
    cout << "x is not divisible by y" << endl;
```

> ⚠️ This approach is **less efficient** — both conditions are always evaluated. Prefer `if-else` when the two branches are mutually exclusive.

---

## 7. Translating Inequalities Correctly

In mathematics you can write `x < y < z`, but **not in C++**.

```cpp
// WRONG — evaluates left to right in unexpected ways
if (x < y < z)

// CORRECT
if ((x < y) && (y < z))
```

---

## 8. Common Pitfall: `=` vs `==`

| Operator | Purpose | Example |
|----------|---------|---------|
| `=`  | Assignment | `x = 3;` |
| `==` | Equality comparison | `if (x == 3)` |

Using `=` inside an `if` condition compiles but causes a **logic error**:

```cpp
// BUG: assigns 3 to x, then tests if 3 is non-zero (always true!)
if (x = 3)
    cout << "Happy Birthday";

// CORRECT
if (x == 3)
    cout << "Happy Birthday";
```

---

## 9. Nested `if` Statements

An `if` or `if-else` can appear inside another `if` or `if-else`.

### Example — with braces (unambiguous)

```cpp
if (hours < 9)
{
    if (hours > 6)
        cout << "snap";
}
else
    cout << "pop";
```

### The "dangling else" problem

Without braces the `else` **binds to the nearest unmatched `if`**:

```cpp
// Ambiguous — else belongs to inner if
if (hours < 9)
    if (hours > 6)
        cout << "snap";
    else
        cout << "pop";   // ← belongs to "hours > 6", NOT "hours < 9"
```

Always use braces with nested `if` statements to avoid this pitfall.

### Larger Nested Example

```cpp
if (x > y)
{
    if (z > x)
    {
        k = 10;
        cout << k;          // outputs 10 when x>y AND z>x
    }
    else
    {
        k = 11;
        cout << k;          // outputs 11 when x>y AND z<=x
    }
}
else
{
    k = 12;
    cout << k;              // outputs 12 when x<=y
}
```

---

## 10. The `if-else` Chain

Used to choose among **more than two** alternatives.

### Syntax

```cpp
if (expression_1)
    statement1;
else if (expression_2)
    statement2;
else if (expression_3)
    statement3;
else
    statementDefault;
```

- Conditions are tested **top to bottom**
- The **first true** branch executes; the rest are skipped
- The final `else` is the default (optional but recommended)

### Example — Marital Status

```cpp
char marcode;
cin >> marcode;

if (marcode == 'M')
    cout << "Individual is married." << endl;
else if (marcode == 'S')
    cout << "Individual is single." << endl;
else if (marcode == 'D')
    cout << "Individual is divorced." << endl;
else if (marcode == 'W')
    cout << "Individual is widowed." << endl;
else
    cout << "An invalid code was entered." << endl;
```

### Example — Letter Grades

```cpp
int score;
char grade;
cin >> score;

if (score >= 85)
    grade = 'A';
else if (score >= 75)
    grade = 'B';
else if (score >= 65)
    grade = 'C';
else if (score >= 50)
    grade = 'D';
else
    grade = 'F';

cout << "Grade: " << grade << endl;
```

> ⚠️ **Order matters!** In the chain above, `>= 85` is checked first. If you reverse the order (start from low), every score would match the first condition.

### Example — Salesman Commission

| Sales (S)       | Commission Rate |
|-----------------|-----------------|
| S ≤ 1000        | 2%              |
| 1000 < S ≤ 1500 | 5%              |
| S > 1500        | 8%              |

```cpp
double s, c;
cin >> s;

if (s <= 1000)
    c = 0.02 * s;
else if (s <= 1500)
    c = 0.02 * 1000 + (s - 1000) * 0.05;
else
    c = 0.02 * 1000 + 0.05 * 500 + 0.08 * (s - 1500);

cout << "Commission = " << c << endl;
```

---

## 11. Common Programming Errors Summary

| # | Error | Example | Fix |
|---|-------|---------|-----|
| 1 | Using `=` instead of `==` | `if (x = 3)` | `if (x == 3)` |
| 2 | Misidentifying which branch runs | Checking condition but wrong variable has unexpected value | Print variable values to debug |
| 3 | Dangling `else` in nested `if` | `else` binds to wrong `if` | Always use `{ }` braces |

---

## 12. Quick Reference — When to Use Each Structure

| Situation | Best Structure |
|-----------|---------------|
| Do something only when condition is true | `if` |
| Choose between exactly two outcomes | `if-else` |
| Choose among three or more outcomes | `if-else` chain |
| Conditions depend on each other | Nested `if` |

---

## 13. Practice Exercises

### Exercise A
Write a code segment using `if-else` that:
- Prints `"High"` if `score > 100`
- Prints `"Low"` if `score <= 100`

```cpp
if (score > 100)
    cout << "High";
else
    cout << "Low";
```

### Exercise B
Print `"Warning"` if `temperature >= 100` **or** `pressure >= 200`; otherwise print `"OK"`.

```cpp
if (temperature >= 100 || pressure >= 200)
    cout << "Warning";
else
    cout << "OK";
```

### Exercise C — Speed Fine
```cpp
// Chain (i) — correct order
if (speed > 75)
    fee = 60;
else if (speed > 50)
    fee = 40;
else if (speed > 35)
    fee = 20;

// Chain (ii) — WRONG order (fee=20 for any speed>35, never reaches higher fees)
if (speed > 35)
    fee = 20;
else if (speed > 50)   // unreachable if speed>35 already matched
    fee = 40;
else if (speed > 75)   // unreachable
    fee = 60;
```
