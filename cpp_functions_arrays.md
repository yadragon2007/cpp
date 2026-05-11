# C++ Programming Concepts — Complete Reference
> Based on SlideSet 6 (Functions) and SlideSet 7 (Arrays)

---

## Table of Contents
1. [Top-Down Design](#1-top-down-design)
2. [Functions Overview](#2-functions-overview)
3. [Predefined (Library) Functions](#3-predefined-library-functions)
4. [User-Defined Functions](#4-user-defined-functions)
5. [Function Declaration (Prototype)](#5-function-declaration-prototype)
6. [Function Definition](#6-function-definition)
7. [The Return Statement](#7-the-return-statement)
8. [Function Calls](#8-function-calls)
9. [Argument Order](#9-argument-order)
10. [void Functions](#10-void-functions)
11. [How a Function Call Works (The Stack)](#11-how-a-function-call-works-the-stack)
12. [Pass by Value vs Pass by Reference](#12-pass-by-value-vs-pass-by-reference)
13. [Variable Scope](#13-variable-scope)
14. [Global Constants](#14-global-constants)
15. [One-Dimensional Arrays](#15-one-dimensional-arrays)
16. [Array Initialization](#16-array-initialization)
17. [Array Input / Output](#17-array-input--output)
18. [Arrays as Function Arguments](#18-arrays-as-function-arguments)
19. [Two-Dimensional Arrays](#19-two-dimensional-arrays)
20. [Practical Examples Summary](#20-practical-examples-summary)

---

## 1. Top-Down Design

**Top-Down Design** (also called *stepwise refinement*) is a problem-solving strategy:

- Break the overall algorithm into smaller **subtasks**.
- Break each subtask into even smaller subtasks.
- Continue until every subtask is simple enough to write directly in code.

In C++, each subtask becomes a **function**.

**Why bother?** Functions make programs:
- Easier to **understand** (each function does one thing)
- Easier to **change** (fix one function without touching others)
- Easier to **test and debug** (test functions individually)
- Easier for **teams** to develop in parallel

---

## 2. Functions Overview

C++ has two categories of functions:

| Category | Where it comes from | Example |
|---|---|---|
| **Predefined (Library)** | Comes with C++ standard libraries | `sqrt()`, `pow()` |
| **User-Defined** | Written by the programmer | `total_cost()`, `findMax()` |

User-defined functions are further divided into:

- **Value-returning functions** — compute and return a single value.
- **void functions** — perform a task but return no value (or return more than one value via references).

---

## 3. Predefined (Library) Functions

C++ ships with libraries full of ready-to-use functions. You just `#include` the right header.

```cpp
#include <cmath>   // for sqrt, pow
#include <iostream> // for cout, cin

double root = sqrt(9.0);    // returns 3.0
double p    = pow(2.5, 3.0); // returns 15.625
```

- The value passed to the function (e.g. `9.0`) is called the **argument**.
- The function **returns** a computed value that can be used in expressions.

```cpp
bonus = sqrt(sales) / 10;
cout << "Side = " << sqrt(area);
```

---

## 4. User-Defined Functions

Every user-defined function has two required parts:

1. **Declaration (Prototype)** — tells the compiler the function exists.
2. **Definition** — the actual code that does the work.

---

## 5. Function Declaration (Prototype)

A prototype tells the compiler:
- The **return type** (what type of value it gives back)
- The **function name**
- The **number and types of parameters**

**Syntax:**
```cpp
ReturnType FunctionName(ParameterType param1, ParameterType param2);
```

**Example:**
```cpp
double total_cost(int number_par, double price_par);
// Computes total cost including 5% sales tax
```

Two valid prototype styles:
```cpp
double total_cost(int number_par, double price_par); // with names
double total_cost(int, double);                      // types only
```

> **Rule:** The prototype must appear **before** any call to the function. The function definition can come after `main()`.

---

## 6. Function Definition

The definition provides the full implementation — the **header** plus the **body**.

**Syntax:**
```cpp
ReturnType FunctionName(ParameterType param1, ParameterType param2)
{
    // local variable declarations
    // statements
    return expression;
}
```

**Example:**
```cpp
double total_cost(int number_par, double price_par)
{
    const double TAX_RATE = 0.05;
    double subtotal;
    subtotal = price_par * number_par;
    return subtotal + subtotal * TAX_RATE;
}
```

- Variables declared inside the function body are **local** — they exist only while the function runs.
- Every non-void function must have at least one `return` statement.

---

## 7. The Return Statement

The `return` statement does two things:
1. **Ends** the function call.
2. **Sends a value back** to the caller.

**Syntax:**
```cpp
return expression;
```

**Examples:**
```cpp
return subtotal + subtotal * TAX_RATE;
return 'P';   // returning a char
return 0;     // returning an int
```

- Each branch of an `if-else` may have its own `return`.
- In a `void` function, `return;` (with no value) is optional — the function ends automatically when it reaches the closing `}`.

---

## 8. Function Calls

To use a function, you **call** it by name with the required arguments.

```cpp
double bill = total_cost(number, price);
```

What happens step by step:
1. Argument values (`number`, `price`) are copied onto **the stack**.
2. Control jumps to the function body.
3. The function executes.
4. The return value is placed on the stack.
5. Control returns to the calling code, and the return value replaces the call expression.

**A function call can be used anywhere an expression of the return type is valid:**
```cpp
cout << total_cost(5, 9.99);          // inside cout
double x = total_cost(n, p) * 1.1;   // inside arithmetic
if (total_cost(n, p) > 100) ...       // inside a condition
```

---

## 9. Argument Order

The compiler checks that argument **types** match, but **not** logical order.

```cpp
char grade(int received, int min_score);

// Correct call:
letter = grade(score, need_to_pass);

// WRONG — compiler won't catch this logical mistake:
letter = grade(need_to_pass, score); // swapped!
```

> Always double-check that arguments are passed in the correct logical order.

---

## 10. void Functions

Use a `void` function when a subtask:
- Produces **no return value** (e.g. just prints something), or
- Needs to **modify multiple variables** (via pass-by-reference).

**Definition:**
```cpp
void show_results(double f_degrees, double c_degrees)
{
    cout << f_degrees << " F = " << c_degrees << " C" << endl;
    return; // optional
}
```

**Call:**
```cpp
show_results(32.5, 0.3);  // standalone statement — correct
```

Important rules for void function calls:
- They are **standalone statements** ending with `;`.
- They **cannot** be used inside expressions.
- They **cannot** appear inside `cout <<` because they return nothing.

```cpp
// WRONG:
cout << show_results(32.5, 0.3);  // compile error!
```

---

## 11. How a Function Call Works (The Stack)

The **stack** is a region of memory used to transfer data between the calling code and functions.

When you call a function:
1. Argument **copies** are pushed onto the stack.
2. A slot for the **return value** is reserved on the stack.
3. The function runs using those stack copies.
4. The return value is written to its slot.
5. Stack data is **automatically deleted** when the function returns.

```
Memory (main):      Stack (inside findMax):
a = 50              x = 50   ← copy of a
b = 75              y = 75   ← copy of b
Mx = 75  ←─────────Max = 75  ← return value
```

Because only **copies** are on the stack, modifying a parameter inside the function does **not** change the original variable in the caller.

---

## 12. Pass by Value vs Pass by Reference

### Pass by Value (default)
A copy of the argument is passed. The original is safe.

```cpp
int findMax(int x, int y)
{
    // x and y are copies; changing them doesn't affect a and b in main
    int Max;
    if (x > y) Max = x;
    else Max = y;
    return Max;
}
```

### Pass by Reference (`&`)
The function receives the **memory address** of the original variable — it works directly on it.

Use `&` after the type in the parameter list:

```cpp
void swap(float& x1, float& x2)
{
    float z = x1;
    x1 = x2;
    x2 = z;
}

// In main:
float a = 50, b = 75;
swap(a, b);   // a and b are actually swapped
```

**Why use pass-by-reference?**
- To modify the caller's variables.
- To return **more than one value** from a function (since `return` can only send back one value).

**Example — returning two values:**
```cpp
void RealRoots(double a, double b, double c, double& r1, double& r2)
{
    double d = sqrt(b*b - 4*a*c);
    r1 = (-b + d) / (2*a);
    r2 = (-b - d) / (2*a);
}

// In main:
double x1, x2;
RealRoots(1, -3, 2, x1, x2);  // x1 and x2 are filled in
```

---

## 13. Variable Scope

**Scope** is the region of a program where a variable is accessible.

### Local Variables
Declared **inside** a function or block (`{}`). Only accessible within that block.

```cpp
void func1() {
    int x = 4;       // local to func1
    cout << x;
}

void func2() {
    int x = 5;       // different x, local to func2
    cout << x;
}
```

Formal parameters are also local to their function:
```cpp
int multiply(int a, int b) {
    return a * b;  // a and b are local
}
```

Variables inside a nested block are local to that block:
```cpp
void f() {
    int x = 1;          // local to f
    {
        int a = 2;      // local to this inner block only
        cout << a;      // OK
        cout << x;      // OK — x is visible from outer scope
    }
    cout << x;          // OK
    // cout << a;       // ERROR — a is out of scope here
}
```

### Global Variables
Declared **outside all functions**. Accessible from any function in the file.

```cpp
int g = 10;   // global

void func1() {
    g = 20;         // modifies the global g
    cout << g;      // prints 20
}

int main() {
    func1();
    g = 30;
    cout << g;      // prints 30
    return 0;
}
```

### Name Conflict: Local hides Global
If a local variable has the same name as a global, the local one takes precedence inside that scope. Use `::` to access the global explicitly:

```cpp
int g = 20;   // global

int main() {
    int g = 10;        // local g shadows global g
    cout << g;         // prints 10  (local)
    cout << ::g;       // prints 20  (global, using scope resolution)
    return 0;
}
```

> **Best practice:** Avoid global variables for mutable data. Use global **constants** instead.

---

## 14. Global Constants

It is good practice to use `const` global identifiers shared across multiple functions:

```cpp
const double PI = 3.14159;

double area(double radius) {
    return PI * pow(radius, 2);
}

double volume(double radius) {
    return (4.0/3.0) * PI * pow(radius, 3);
}
```

This avoids magic numbers and keeps the codebase consistent.

---

## 15. One-Dimensional Arrays

An **array** is a collection of related values of the **same data type**, stored under a single name and accessed by an **index**.

### Declaration
```cpp
const int NUMELS = 5;
int grade[NUMELS];          // array of 5 integers

const int ARRAYSIZE = 4;
char code[ARRAYSIZE];       // array of 4 characters

const int NUMELS2 = 6;
double prices[NUMELS2];     // array of 6 doubles
```

Memory is allocated **sequentially**:
```
grade[0]  grade[1]  grade[2]  grade[3]  grade[4]
   85        90        78        75        92
```

### Accessing Elements
Use the array name followed by the **index** (subscript) in brackets. Indices start at **0**.

```cpp
grade[0] = 95;
grade[1] = grade[0] - 11;   // 84
cout << grade[2];
```

Any integer expression can be used as an index:
```cpp
grade[i]
grade[2*i]
grade[j - i]
```

> **Warning:** C++ does **not** check bounds. Accessing `grade[10]` on an array of size 5 causes undefined behavior and may crash your program.

---

## 16. Array Initialization

Arrays can be initialized at declaration using `{ }`:

```cpp
int gallons[5] = {19, 16, 14, 19, 20};
```

The size can be omitted when initializing:
```cpp
char code[] = {'s', 'a', 'm', 'p', 'l', 'e'};   // size = 6
char code[] = "sample";                           // size = 7 (includes '\0')
```

### The Null Character `\0`
String literals stored in `char` arrays are automatically terminated with the **null character** `\0`:
```
code[0]='s'  code[1]='a'  code[2]='m'  code[3]='p'  code[4]='l'  code[5]='e'  code[6]='\0'
```

### 2D Array Initialization
```cpp
int val[3][4] = { {8,16,9,52}, {3,15,27,6}, {14,25,2,10} };
// Inner braces optional:
int val[3][4] = { 8,16,9,52, 3,15,27,6, 14,25,2,10 };
```
Values are assigned row by row, starting at `[0][0]`.

---

## 17. Array Input / Output

### Reading into an array with a loop
```cpp
const int NUMELS = 5;
int grade[NUMELS];

for (int i = 0; i < NUMELS; i++) {
    cout << "Enter a grade: ";
    cin >> grade[i];
}
```

### Printing an array with a loop
```cpp
for (int i = 0; i < NUMELS; i++)
    cout << "grade[" << i << "] = " << grade[i] << endl;
```

### Partial range
```cpp
for (int k = 5; k < 20; k++)
    cout << k << " " << amount[k];
```

---

## 18. Arrays as Function Arguments

### Passing a single element
Just like passing a scalar variable:
```cpp
findMax(grades[2], grades[6]);
```

### Passing the entire array
Pass the array name (no brackets, no index). The function receives **direct access** to the original array — no copy is made.

```cpp
int nums[5] = {2, 18, 1, 27, 16};
cout << findMax(nums);
```

Function prototype and definition:
```cpp
int findMax(int vals[5]);   // or int findMax(int vals[])

int findMax(int vals[MAXELS])
{
    int max = vals[0];
    for (int i = 1; i < MAXELS; i++)
        if (max < vals[i]) max = vals[i];
    return max;
}
```

> Because the entire array is passed by reference (not copied), any changes made inside the function **affect the original array**.

### Passing 2D arrays
```cpp
void display(int nums[ROWS][COLS])
{
    for (int r = 0; r < ROWS; r++) {
        for (int c = 0; c < COLS; c++)
            cout << "\t" << nums[r][c];
        cout << endl;
    }
}
```

---

## 19. Two-Dimensional Arrays

A **2D array** is a table (matrix) with rows and columns.

### Declaration
```cpp
int val[3][4];          // 3 rows, 4 columns
double prices[10][5];   // 10 rows, 5 columns
char code[6][26];       // 6 rows, 26 columns
```

### Accessing Elements
`array[row][col]` — first index is the row, second is the column.

```cpp
val[1][3] = 6;                    // row 1, column 3
int sumRow0 = val[0][0] + val[0][1] + val[0][2] + val[0][3];
```

### Printing with nested loops
```cpp
const int NUMROWS = 3, NUMCOLS = 4;
for (int i = 0; i < NUMROWS; i++) {
    cout << endl;
    for (int j = 0; j < NUMCOLS; j++)
        cout << "\t" << val[i][j];
}
```

Output:
```
8    16    9    52
3    15    27    6
14   25    2    10
```

---

## 20. Practical Examples Summary

| Problem | Key Concept Used |
|---|---|
| Compute total cost with tax | Value-returning function |
| Determine pass/fail grade | Value-returning function with `char` return |
| Convert Fahrenheit to Celsius | void function |
| Swap two values | Pass by reference |
| Find real roots of quadratic | void + pass-by-reference (multiple outputs) |
| Max of 3 integers | Value-returning function |
| Factorial of N | Value-returning function with loop |
| Leap year check | Boolean return function |
| Array max/min | 1D array + loop |
| Sum of array elements | 1D array + loop |
| Matrix trace & determinant | 2D array + functions |
| Matrix addition | 2D arrays passed to functions |
| Newton's method root finding | Arrays + functions combined |

---

## Quick Reference Cheat Sheet

```cpp
// ── FUNCTION PROTOTYPE ──────────────────────────────
double total_cost(int n, double price);

// ── FUNCTION DEFINITION ─────────────────────────────
double total_cost(int n, double price) {
    return n * price * 1.05;
}

// ── VOID FUNCTION ───────────────────────────────────
void printResult(double val) {
    cout << "Result: " << val << endl;
}

// ── PASS BY REFERENCE ───────────────────────────────
void swap(int& a, int& b) {
    int tmp = a; a = b; b = tmp;
}

// ── 1D ARRAY ────────────────────────────────────────
int arr[5] = {1, 2, 3, 4, 5};
for (int i = 0; i < 5; i++) cout << arr[i];

// ── 2D ARRAY ────────────────────────────────────────
int mat[3][4];
mat[1][2] = 99;

// ── ARRAY TO FUNCTION ───────────────────────────────
void process(int data[], int size);
process(arr, 5);

// ── GLOBAL CONSTANT ─────────────────────────────────
const double PI = 3.14159;

// ── LOCAL VS GLOBAL SCOPE ───────────────────────────
int g = 10;  // global
int main() {
    int g = 5;   // local — shadows global
    cout << g;   // 5
    cout << ::g; // 10 (global)
}
```
