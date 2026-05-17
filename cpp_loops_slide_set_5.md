# C++ Repetitions (Loops) — Complete Reference

> Based on *A First Book of C++: From Here To There, Third Edition* — SlideSet 5

---

## Table of Contents

1. [Selections vs. Loops](#selections-vs-loops)
2. [The `while` Statement](#the-while-statement)
   - [Syntax](#while-syntax)
   - [Execution Steps](#while-execution-steps)
   - [Loop Control Variable](#loop-control-variable)
   - [Fixed-Count Loops](#fixed-count-loops)
   - [cin Within a while Loop](#cin-within-a-while-loop)
   - [Event-Controlled Loops](#event-controlled-loops)
   - [Infinite Loops](#infinite-loops)
   - [Common Mistakes](#common-while-mistakes)
3. [The `for` Statement](#the-for-statement)
   - [Syntax](#for-syntax)
   - [Equivalence with while](#for-to-while-equivalence)
   - [cin Within a for Loop](#cin-within-a-for-loop)
   - [Count Progressions](#count-progressions)
4. [The `do-while` Statement](#the-do-while-statement)
5. [break and continue](#break-and-continue)
6. [Validity Checks](#validity-checks)
7. [Nested Loops](#nested-loops)
8. [Complete Examples](#complete-examples)
9. [Common Programming Errors](#common-programming-errors)
10. [Summary Comparison](#summary-comparison)

---

## Selections vs. Loops

A **selection** (if/else) executes a block **once** based on a condition.  
A **loop** (while/for/do-while) executes a block **repeatedly** as long as a condition holds.

```
Selection flowchart:              Loop flowchart:
  read X                            read X
     |                                 |
  X >= 0 ?  --N--> write "Invalid"   X < 0 ? --N--> Z=sqrt(X) --> write Z --> write "End"
     |T                               |T
  Z=sqrt(X)                        read X (loop back)
  write Z
  write "End"
```

Key difference: the loop **feeds back** into the condition check, repeating until the condition fails.

---

## The `while` Statement

### while Syntax

```cpp
while (expression)
{
    statement1;
    statement2;
    // ...
}
```

- The expression is evaluated like an `if-else` condition.
- The body executes **repeatedly** as long as the expression is **nonzero (true)**.
- **Do NOT place a semicolon after the closing parenthesis** — that creates an empty loop.
- For a single statement, braces are optional but strongly recommended.

### while Execution Steps

1. **Test** the expression.
2. If the expression is **true (nonzero)**:
   - Execute the body.
   - Go back to step 1.
3. If the expression is **false (zero)**:
   - **Exit** the while statement.

```
Enter while
      |
   [Test expression]
      |
   true ──> [Execute body] ──> (back to Test)
      |
   false ──> Exit while
```

### Loop Control Variable

The variable used in the condition (that controls when the loop stops) is called the **loop control variable**.

```cpp
int count;
count = 1;                    // initialize count
while (count <= 10)
{
    cout << count << " ";
    count++;                  // increment count (loop control variable)
}
// count == 11 when the loop exits
```

Output: `1 2 3 4 5 6 7 8 9 10`

> **Note:** After the loop, `count` holds the value **11**, not 10 — because the condition `count <= 10` fails when count becomes 11.

### Fixed-Count Loops

The condition tests a counter that checks for a **fixed number of repetitions**.

```cpp
// Celsius to Fahrenheit: 5 to 50 degrees in steps of 5
int celsius = 5;
while (celsius <= 50)
{
    double fahren = (9.0 / 5.0) * celsius + 32.0;
    cout << celsius << " C = " << fahren << " F" << endl;
    celsius = celsius + 5;    // increment by 5, not 1
}
```

### cin Within a while Loop

**Program 5.5 — Reading N numbers:**

```cpp
const int MAXNUMS = 4;
int count;
double num;

cout << "This program will ask you to enter " << MAXNUMS << " numbers.\n";
count = 1;

while (count <= MAXNUMS)
{
    cout << "\nEnter a number: ";
    cin >> num;
    cout << "The number entered is " << num;
    count++;
}
cout << endl;
```

**Program 5.6 — Computing a running total:**

```cpp
const int MAXNUMS = 4;
int count;
double num, total;

count = 1;
total = 0;

while (count <= MAXNUMS)
{
    cout << "\nEnter a number: ";
    cin >> num;
    total = total + num;
    cout << "The total is now " << total;
    count++;
}
cout << "\n\nThe final total is " << total << endl;
```

**Sample interest calculation** — how many months to grow $50 to over $100 at 2%/month:

```cpp
float balance = 50;
int count = 0;

while (balance <= 100)
{
    balance += balance * 0.02;
    count++;
}
cout << "Number of months= " << count;
```

### Event-Controlled Loops

Instead of a fixed count, the loop stops when a **specific event** occurs (e.g., a sentinel value or a flag).

```cpp
int n, k, sum, value;
bool test;
cin >> n;
sum = 0; k = 1; test = false;

while ((k <= n) && !(test))
{
    cin >> value;
    if (value > 0)       sum = sum + value;
    else if (value < 0)  sum = sum - value;
    else                 test = true;   // zero found — stop
    k++;
}
cout << "at k=" << k << " sum= " << sum << " value= " << value << endl;
```

For input `6 7 -3 -5 10 0 9`, the loop stops at the `0`.

### Infinite Loops

A loop that **never terminates** because the condition never becomes false.

```cpp
// DANGEROUS — if x starts at 1 and increments by 2, it skips 12 entirely
x = 1;
while (x != 12)     // x goes: 1, 3, 5, 7, 9, 11, 13 ... never equals 12!
{
    cout << x << endl;
    x = x + 2;
}

// SAFE — use < instead of !=
while (x < 12)      // stops correctly when x = 13
```

**Rule:** The loop body must contain code that will eventually make the Boolean expression **false**.

### Common while Mistakes

```cpp
// MISTAKE 1: Semicolon after while condition → empty loop (infinite)
k = 1;
while (k <= 10);      // <-- semicolon here! loop body is empty, runs forever
{
    cout << k << endl;
    k = k + 1;
}

// MISTAKE 2: No braces — only first statement is in the loop
k = 1;
while (k <= 10)
    cout << k << endl;   // inside loop
    k = k + 1;           // OUTSIDE loop — k never increments → infinite loop

// MISTAKE 3: Wrong initial condition → loop never runs
k = 1;
while (k >= 10)     // 1 >= 10 is false immediately → body never executes
{
    cout << k << endl;
    k = k + 1;
}

// MISTAKE 4: Decrement instead of increment → infinite loop (going away from condition)
k = 1;
while (k <= 10)
{
    cout << k << endl;
    k = k - 1;      // k gets smaller: 1, 0, -1, -2 ... never reaches 10
}
```

---

## The `for` Statement

### for Syntax

```cpp
for (initializing_list; expression; altering_list)
{
    statement;
}
```

| Component | Purpose |
|---|---|
| `initializing_list` | Sets the starting value of the loop variable |
| `expression` | Condition tested before each iteration |
| `altering_list` | Executed at the **end** of each iteration |

All three components are **optional**, but the two semicolons are **mandatory**.

```cpp
for ( ; count <= 20 ; )   // valid — no initializer or altering
for ( ; ; )               // valid — infinite loop (like while(1))
```

### for to while Equivalence

Every `for` loop can be rewritten as a `while` loop:

```cpp
// for version
int j;
for (j = 1; j <= 3; j++)
{
    cout << j << endl;
}

// Equivalent while version
int j;
j = 1;                    // initializer
while (j <= 3)            // expression
{
    cout << j << endl;
    j++;                  // altering list
}
```

### for Examples

**Basic count loop (even numbers 2–20):**

```cpp
int count;
for (count = 2; count <= 20; count = count + 2)
    cout << count << " ";
// Output: 2 4 6 8 10 12 14 16 18 20
```

**Printing -9 to 12 in steps of 3:**

```cpp
for (int i = -9; i <= 12; i += 3)
    cout << i << endl;
// Output: -9 -6 -3 0 3 6 9 12
```

**Counter-controlled loop (N iterations):**

```cpp
int count = 1, N;
cin >> N;
while (count <= N)
{
    cout << "Count " << count << " " << (count * count) << endl;
    count++;
}
```

### cin Within a for Loop

**Program 5.11 — Average of MAXCOUNT numbers:**

```cpp
const int MAXCOUNT = 5;
int count;
double num, total, average;

total = 0.0;

for (count = 0; count < MAXCOUNT; count++)
{
    cout << "Enter a number: ";
    cin >> num;
    total = total + num;
}

average = total / count;
cout << "The average of the data entered is " << average << endl;
```

**Initialization variations:**

```cpp
// Alt 1: total outside, count inside for
total = 0.0;
for (count = 0; count < MAXCOUNT; count++) { ... }

// Alt 2: both initialized inside for
for (total = 0.0, count = 0; count < MAXCOUNT; count++) { ... }

// Alt 3: both declared AND initialized inside for
for (double total = 0.0, int count = 0; count < MAXCOUNT; count++) { ... }
```

### Count Progressions

| for Statement | Count Sequence |
|---|---|
| `for(i=2; i<=10; i=i+2)` | 2, 4, 6, 8, 10 |
| `for(i=1; i<10; i=i+2)` | 1, 3, 5, 7, 9 |
| `for(i=10; i<=50; i=i+10)` | 10, 20, 30, 40, 50 |
| `for(i=10; i>=0; i-=2)` | 10, 8, 6, 4, 2, 0 |

---

## The `do-while` Statement

### Syntax

```cpp
do {
    statement;
} while (condition);   // <-- semicolon is REQUIRED here
```

### Key Difference from while

| Feature | `while` | `do-while` |
|---|---|---|
| Condition tested | **Before** the body | **After** the body |
| Minimum executions | **0** (may never run) | **1** (always runs at least once) |

### Flowchart

```
[Loop body]
      |
  [condition] --true--> (back to loop body)
      |
   false --> Exit
```

### Example

```cpp
int counter = 1;
do {
    cout << counter << " ";
} while (++counter <= 10);

// Output: 1 2 3 4 5 6 7 8 9 10
```

Note the **pre-increment** `++counter` — the increment happens before the condition is tested.

---

## break and continue

### break

- **Immediately exits** the nearest enclosing `while`, `for`, or `do-while`.
- Execution continues at the first statement **after** the loop.

```cpp
for (int x = 1; x <= 10; x++)
{
    if (x == 5)
        break;          // exits loop when x is 5
    cout << x << " ";
}
// Output: 1 2 3 4
// x == 5 when we exit
```

### continue

- **Skips the rest of the current iteration** and moves to the next one.
- In a `for` loop: the altering expression runs, then the condition is re-tested.
- In `while`/`do-while`: the condition is re-tested immediately.

```cpp
for (int x = 1; x <= 10; x++)
{
    if (x == 5)
        continue;       // skip printing 5, go to next iteration
    cout << x << " ";
}
// Output: 1 2 3 4 6 7 8 9 10
```

### break vs. continue Side-by-Side

```cpp
// break:                        // continue:
for (i = 1; i <= 10; i++)        for (i = 1; i <= 10; i++)
{                                 {
    if (i == 5)                       if (i == 5)
        break;                            continue;
    cout << i << endl;                cout << i << endl;
}                                 }
// Output: 1 2 3 4               // Output: 1 2 3 4 6 7 8 9 10
```

---

## Validity Checks

### Using do-while for Input Validation

```cpp
int idNum;
do
{
    cout << "\nEnter an identification number: ";
    cin >> idNum;
    if (idNum < 100 || idNum > 1999)
        cout << "\nAn invalid number was entered. Please reenter.";
    else
        break;              // valid input — exit loop
} while (1);                // always true — only exit via break
```

### Infinite Loop + break Pattern

```cpp
int num;
double squared;
do
{
    cout << "Enter a number (Enter 0 to quit): ";
    cin >> num;
    if (num == 0) break;        // sentinel value exits the loop
    squared = num * num;
    cout << num << " squared is " << squared << endl;
} while (1);
```

### Using while for Validation

```cpp
cout << "Enter a positive number -> ";
cin >> Num;
while (Num <= 0)
{
    cout << "The number entered must be positive" << endl;
    cout << "Enter a positive number -> " << endl;
    cin >> Num;
}
// Program continues here with a valid positive number in Num
```

### Sentinel-Value Loop (Employee Salaries Example)

```cpp
cout << "Enter the hours worked (Enter -1 when done): ";
cin >> hours;

while (hours != -1)
{
    cout << "Enter the rate of pay\n";
    cin >> rate;
    float Salary = hours * rate;
    cout << hours << ' ' << rate << ' ' << Salary << endl;
    cout << "Enter the hours worked (Enter -1 when done): ";
    cin >> hours;
}
```

---

## Nested Loops

A loop placed **inside** another loop.

### Syntax

```cpp
for (i = 1; i <= 5; i++)           // outer loop
{
    cout << "\ni is now " << i << endl;
    for (j = 1; j <= 4; j++)       // inner loop
    {
        cout << " j = " << j;
    }
}
```

### Rules

- Each single trip through the **outer** loop causes the **inner** loop to run through its **entire** sequence.
- Use a **different variable** to control each loop.
- Inner loop statements must be **contained within** the outer loop braces.

### Multiplication Table Example

```cpp
for (i = 1; i <= 3; i++)
{
    for (j = 1; j <= 3; j++)
        cout << i * j << " ";
    cout << endl;
}
```

Output:
```
1 2 3
2 4 6
3 6 9
```

### Student Average Example

```cpp
int i, j;
float x, sum;
cin >> m >> n;          // m students, n exams each

for (i = 1; i <= m; i++)
{
    sum = 0;
    for (j = 1; j <= n; j++)
    {
        cin >> x;
        sum = sum + x;
    }
    cout << "Student " << i << " avg= " << sum / n << endl;
}
```

---

## Complete Examples

### Find Max and Min in N Numbers

```cpp
#include <iostream>
using namespace std;

int main()
{
    int n, i;
    float x, min, max;

    cin >> n >> x;
    max = x; min = x; i = 2;

    while (i <= n)
    {
        cin >> x;
        if (x > max)       max = x;
        else if (x < min)  min = x;
        i = i + 1;
    }

    cout << "max= " << max << " min= " << min;
    return 0;
}
```

### Factorial: n! = 1 × 2 × … × n

```cpp
int n, i, fact;
cin >> n;
i = 1; fact = 1;

while (i <= n)
{
    fact = fact * i;
    i = i + 1;
}
cout << "factorial = " << fact << endl;
```

Trace for n=4:

| Iteration | i | fact |
|---|---|---|
| (initial) | 1 | 1 |
| 1 | 1 | 1 |
| 2 | 2 | 2 |
| 3 | 3 | 6 |
| 4 | 4 | 24 |

### Sum of Odd and Even Numbers in First N Integers

```cpp
int sumeven, sumodd, i, n;
cin >> n;
i = 1; sumeven = 0; sumodd = 0;

while (i <= n)
{
    if (i % 2 == 0)  sumeven = sumeven + i;
    else             sumodd  = sumodd + i;
    i = i + 1;
}

cout << "sumeven= " << sumeven << endl;
cout << "sumodd= "  << sumodd  << endl;
```

### Series Sum with Accuracy E

Compute: `sum = x + x²/2! + x³/3! + …` until the term is smaller than E.

Using the recurrence `T(k+1) = T(k) * x / (k+1)`:

```cpp
#include <iostream>
#include <cmath>        // for fabs()
using namespace std;

int main()
{
    int k;
    float x, e, sum, t;

    cin >> x >> e;
    t = x; sum = x; k = 1;

    while (fabs(t) >= e)
    {
        t   = t * x / (k + 1);
        sum = sum + t;
        k   = k + 1;
    }

    cout << "sum = " << sum;
    return 0;
}
```

### Half-Until-1 Loop

```cpp
int num;
cout << "Please enter the number to divide: ";
cin >> num;

while (num > 1)
{
    cout << num << endl;
    num /= 2;
}
```

---

## Common Programming Errors

### Off-by-One Errors

The loop runs one time **too many** or one time **too few**.

```cpp
// Should print 1..10 but...
for (i = 0; i < 10; i++)    // runs for i = 0,1,...,9 → prints 0..9 (off by one)
for (i = 1; i <= 10; i++)   // correct: prints 1..10
for (i = 1; i < 10; i++)    // runs for i = 1,...,9 → misses 10
```

### Assignment Instead of Equality

```cpp
while (x = 5)    // WRONG: assigns 5 to x (always true → infinite loop)
while (x == 5)   // correct: tests if x equals 5
```
The compiler will **not** catch this error.

### Floating-Point Equality

```cpp
// WRONG — floating-point numbers are imprecise
while (fnum != 0.01) { ... }

// CORRECT — use a tolerance (epsilon)
while (fabs(fnum - 0.01) > 1e-6) { ... }
```

### Semicolon After for Parentheses

```cpp
for (count = 0; count < 10; count++);   // <-- semicolon here!
total = total + num;                     // this line is NOT in the loop
```
Creates a loop that increments `count` 10 times but does nothing else.

### Commas Instead of Semicolons in for

```cpp
for (count = 1, count < 10, count++)    // WRONG — commas not valid here
for (count = 1; count < 10; count++)    // CORRECT
```

Commas are only valid **within** the initializing or altering lists (e.g., `for (i=0, j=10; ...)`).

### Missing Semicolon After do-while

```cpp
do
{
    statement;
} while (expression)    // WRONG — missing semicolon
} while (expression);   // CORRECT
```

---

## Summary Comparison

| Feature | `while` | `for` | `do-while` |
|---|---|---|---|
| Condition tested | Before body | Before body | **After** body |
| Min. iterations | 0 | 0 | **1** |
| Best use case | Unknown # of iterations / event-controlled | Known # of iterations (count-controlled) | Must execute at least once (menus, validation) |
| Initializer location | Before the statement | Inside parentheses | Before the statement |
| Altering expression | Inside loop body | Inside parentheses | Inside loop body |

### Quick Conversion: for ↔ while

```cpp
// for:
for (init; condition; alter) { body; }

// Equivalent while:
init;
while (condition) { body; alter; }
```

### Loop Selection Guide

- Use **`for`** when you know exactly how many times to loop (fixed-count).
- Use **`while`** when the number of iterations depends on user input or a runtime condition.
- Use **`do-while`** when the loop body **must** execute at least once (e.g., input validation menus).
- Use **`break`** to exit a loop early based on a condition inside the body.
- Use **`continue`** to skip the rest of the current iteration and proceed to the next.
