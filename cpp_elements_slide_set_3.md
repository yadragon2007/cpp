# C++ Elements — Complete Reference
> Based on SlideSet 3: C++ Elements (Introduction to Programming)

---

## Table of Contents
1. [The C++ Development Environment](#1-the-c-development-environment)
2. [A First C++ Program](#2-a-first-c-program)
3. [Comments](#3-comments)
4. [Preprocessor Directives](#4-preprocessor-directives)
5. [Output with cout](#5-output-with-cout)
6. [Namespaces](#6-namespaces)
7. [Data Types Overview](#7-data-types-overview)
8. [The int Data Type](#8-the-int-data-type)
9. [The char Data Type](#9-the-char-data-type)
10. [Escape Sequences](#10-escape-sequences)
11. [The bool Data Type](#11-the-bool-data-type)
12. [Floating-Point Types](#12-floating-point-types)
13. [Signed vs Unsigned Data Types](#13-signed-vs-unsigned-data-types)
14. [The sizeof() Operator](#14-the-sizeof-operator)
15. [Arithmetic Operators](#15-arithmetic-operators)
16. [Integer Division and Modulus](#16-integer-division-and-modulus)
17. [Operator Precedence and Associativity](#17-operator-precedence-and-associativity)
18. [Formatted Output with cout](#18-formatted-output-with-cout)
19. [Identifiers (Naming Variables)](#19-identifiers-naming-variables)
20. [Variables and Declaration Statements](#20-variables-and-declaration-statements)
21. [Constant Declarations](#21-constant-declarations)
22. [Assignment Operators](#22-assignment-operators)
23. [Coercion (Type Conversion)](#23-coercion-type-conversion)
24. [Abbreviated Assignment Operators](#24-abbreviated-assignment-operators)
25. [Increment and Decrement Operators](#25-increment-and-decrement-operators)
26. [Expressions](#26-expressions)
27. [Boolean Expressions](#27-boolean-expressions)
28. [Relational Operators](#28-relational-operators)
29. [Logical Operators](#29-logical-operators)
30. [Complete Operator Precedence Table](#30-complete-operator-precedence-table)
31. [Mathematical Library Functions](#31-mathematical-library-functions)
32. [Type Casting](#32-type-casting)
33. [Interactive Input with cin](#33-interactive-input-with-cin)
34. [Symbolic Constants](#34-symbolic-constants)
35. [Statement Placement Rules](#35-statement-placement-rules)
36. [Common Programming Errors](#36-common-programming-errors)

---

## 1. The C++ Development Environment

Before a C++ program can run, it goes through 6 phases:

| Phase | Tool | What Happens |
|---|---|---|
| 1. **Edit** | Editor | You write source code; saved to disk as a `.cpp` file |
| 2. **Preprocess** | Preprocessor | Handles `#include`, `#define` directives before compiling |
| 3. **Compile** | Compiler | Translates C++ code into machine object code (`.obj`) |
| 4. **Link** | Linker | Combines object code with libraries → creates executable (`a.out`) |
| 5. **Load** | Loader | Puts the executable program into memory |
| 6. **Execute** | CPU | Runs instructions one by one |

---

## 2. A First C++ Program

```cpp
// A first program in C++.
#include <iostream>

// function main begins program execution
int main()
{
    std::cout << "Welcome to C++!\n";

    return 0; // indicate that program ended successfully
} // end function main
```

**Output:**
```
Welcome to C++!
```

Key parts of this program:

- `#include <iostream>` — preprocessor directive that gives access to input/output
- `int main()` — every C++ program must have exactly **one** `main()` function; this is where execution starts
- `{ }` — curly braces mark the beginning and end of the function body
- `std::cout << "..."` — sends text to the screen
- `return 0;` — exits `main()` and tells the OS the program finished successfully
- Each executable statement ends with a **semicolon** `;`

---

## 3. Comments

Comments are notes for humans — the compiler completely ignores them.

**Single-line comment** — starts with `//`, continues to end of line:
```cpp
// This is a single-line comment
int x = 5; // This comment is after a statement
```

**Good practice:** Use comments to describe what your code does, not *how* — the code itself shows the how.

---

## 4. Preprocessor Directives

Lines that begin with `#` are **preprocessor directives** — handled before the compiler runs.

```cpp
#include <iostream>   // include the standard I/O library
#include <cmath>      // include the math library
```

- They do **not** end with a semicolon.
- They tell the preprocessor to find and paste the contents of library files into your code.

---

## 5. Output with cout

`cout` is the **standard output stream object** — it's "connected" to the screen.

**Syntax:**
```cpp
cout << value1 << value2 << ...;
```

- `<<` is the **stream insertion operator** ("put to")
- Multiple items can be chained on one `cout` line

**Examples:**
```cpp
cout << "Hello!";                             // prints a string
cout << 42;                                   // prints an integer
cout << "The answer is " << 42 << "\n";       // prints string + number + newline
cout << "Sum = " << (6 + 15) << endl;         // evaluates expression inline
```

- `endl` flushes the stream and moves to a new line (same effect as `"\n"` for most purposes)
- `"\n"` is faster since it doesn't flush the buffer

---

## 6. Namespaces

`cout`, `cin`, and `endl` belong to the **`std` namespace** (standard library).

**Two ways to use them:**

Option 1 — prefix every use with `std::`:
```cpp
std::cout << "Hello";
std::cin >> x;
```

Option 2 — add `using namespace std;` at the top (most common in beginner code):
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello";   // no std:: needed
    return 0;
}
```

---

## 7. Data Types Overview

Every piece of data in C++ must have a **type**. A data type defines:
- The **set of valid values** (e.g. integers, true/false)
- The **operations** that can be applied (e.g. `+`, `-`)
- The **storage size** (how many bytes in memory)

Key terms:
- **Literal**: A value that directly represents itself in code: `5`, `3.14`, `'A'`, `"Hello"`
- **Built-in (primitive) type**: Provided by C++ itself, no extra code needed
- **Atomic**: Cannot be broken into a smaller type (all built-in types are atomic)

**The four main categories:**

| Category | Types |
|---|---|
| Integer | `int`, `short int`, `long int`, `char`, `bool` |
| Floating-point | `float`, `double`, `long double` |
| Character | `char` |
| Boolean | `bool` |

---

## 8. The int Data Type

Stores **whole numbers** (no decimal point).

```cpp
int age = 25;
int temperature = -10;
int count = 0;
```

Valid `int` literals: `0`, `5`, `-10`, `+25`, `1000`, `-26351`

Invalid: `$255.62`, `2,523`, `3.0`, `6,243,982` (no commas, no decimals, no special symbols)

**Storage:** Most systems allocate **4 bytes** for `int`, giving a range of roughly −2.1 billion to +2.1 billion.

---

## 9. The char Data Type

Stores a **single character** — a letter, digit, or symbol — enclosed in **single quotes**.

```cpp
char grade = 'A';
char symbol = '$';
char digit = '7';
```

Valid `char` literals: `'A'`, `'$'`, `'b'`, `'7'`, `'!'`

> Note: `'7'` is the character seven, not the number 7. They have different types.

Characters are stored internally as **ASCII codes** (American Standard Code for Information Interchange):
- Each character maps to a number 0–255
- One byte of storage
- Uppercase `'A'` = 65, lowercase `'a'` = 97, digit `'0'` = 48

```cpp
char ch = 100;    // Valid — stores 'd' (ASCII 100)
cout << ch;       // prints: d
cout << (int)ch;  // prints: 100
```

---

## 10. Escape Sequences

The **backslash `\`** is the **escape character** — it tells the compiler to treat the next character specially rather than literally.

**Complete escape sequence table:**

| Escape Sequence | Character | Effect |
|---|---|---|
| `\n` | Newline | Move to the next line |
| `\t` | Horizontal tab | Move to next tab stop |
| `\v` | Vertical tab | Move to next vertical tab |
| `\b` | Backspace | Move back one space |
| `\r` | Carriage return | Move cursor to start of current line |
| `\f` | Form feed | Issue a form feed |
| `\a` | Alert | Issue a beep sound |
| `\\` | Backslash | Insert a literal `\` character |
| `\'` | Single quote | Insert a `'` inside single-quoted char |
| `\"` | Double quote | Insert a `"` inside a string |
| `\?` | Question mark | Insert a `?` character |
| `\0` | Null character | Character with value 0 (string terminator) |
| `\nnn` | Octal number | Character with octal value *nnn* |
| `\xhhhh` | Hex number | Character with hex value *hhhh* |

**Usage examples:**
```cpp
cout << "Hello\nWorld\n";   // Hello on one line, World on next
cout << "Name:\tYousef\n";  // Name:   Yousef (tab-separated)
cout << "Say \"Hi\"";       // Say "Hi"
cout << "Path: C:\\file";   // Path: C:\file
```

Both `'\n'` (char literal) and `"\n"` (string literal) produce a newline.

**Good practice:** Always end the last line of output with `\n` or `endl`.

---

## 11. The bool Data Type

Stores **boolean (logical)** values — only `true` or `false`.

```cpp
bool isRaining = true;
bool isLoggedIn = false;
```

Internally, C++ stores booleans as integers:
- `true` = **1** (or any non-zero value)
- `false` = **0**

```cpp
bool b = true;
cout << b;        // prints: 1

int i = false + true;   // i = 0 + 1 = 1
```

> **Note:** Any non-zero value is treated as `true`. You can perform arithmetic on booleans, but `cin` cannot read boolean values directly — only print them.

---

## 12. Floating-Point Types

Store numbers **with a decimal point** (real numbers).

```cpp
float  price = 9.99f;
double pi    = 3.14159265358979;
```

Valid floating-point literals: `+10.625`, `5.`, `-6.2`, `3521.92`, `0.0`
> `5.` and `5` are different: `5.` is a float, `5` is an integer.

**Three floating-point types:**

| Type | Storage | Significant Digits | Typical Range |
|---|---|---|---|
| `float` | 4 bytes | ~7 | ±3.4 × 10³⁸ |
| `double` | 8 bytes | ~15–16 | ±1.7 × 10³⁰⁸ |
| `long double` | 10–16 bytes | ~18–19 | extended range |

**Precision** = number of significant (correct) digits. Example: if a value has 5 significant digits, `687.45678921` is only accurate to `687.46`.

**Exponential (scientific) notation:**
```cpp
double x = 1.5e3;    // 1.5 × 10³ = 1500.0
double y = 2.5e-4;   // 2.5 × 10⁻⁴ = 0.00025
double z = 2E3;      // 2000.0
```

> **Rule:** The exponent must be an integer. `2E3.5` is invalid.

---

## 13. Signed vs Unsigned Data Types

- **Signed**: can store negative, zero, and positive values (default for most types)
- **Unsigned**: stores only zero and positive values — doubles the positive range

**Integer data type storage table:**

| Type | Bytes | Range |
|---|---|---|
| `char` | 1 | 256 characters |
| `bool` | 1 | `true` (nonzero) or `false` (0) |
| `short int` | 2 | −32,768 to +32,767 |
| `unsigned short int` | 2 | 0 to 65,535 |
| `int` | 4 | −2,147,483,648 to +2,147,483,647 |
| `unsigned int` | 4 | 0 to 4,294,967,295 |
| `long int` | 4 | −2,147,483,648 to +2,147,483,647 |
| `unsigned long int` | 4 | 0 to 4,294,967,295 |

`char` and `bool` are unsigned (no negative codes).

---

## 14. The sizeof() Operator

`sizeof()` tells you how many bytes a data type or variable occupies in memory.

```cpp
cout << sizeof(int);     // typically 4
cout << sizeof(double);  // typically 8
cout << sizeof(char);    // always 1
cout << sizeof(bool);    // typically 1

int x;
cout << sizeof(x);       // same as sizeof(int)
```

Useful for writing platform-independent code where sizes may vary.

---

## 15. Arithmetic Operators

**Binary operators** — require two operands (left and right):

| Operation | Operator | Example | Result |
|---|---|---|---|
| Addition | `+` | `5 + 3` | `8` |
| Subtraction | `-` | `5 - 3` | `2` |
| Multiplication | `*` | `5 * 3` | `15` |
| Division | `/` | `5 / 2` | `2` (integer!) |
| Modulus | `%` | `5 % 2` | `1` |

**Unary negation** — reverses the sign of one operand:
```cpp
int x = 5;
int y = -x;   // y = -5
```

**Mixed-mode expressions** — what type is the result?
- Both operands are **integers** → result is **integer**
- At least one operand is **floating-point** → result is **floating-point**

```cpp
10 / 3       // = 3    (integer division — truncates)
10.0 / 3     // = 3.333...  (one is float → float result)
10 / 3.0     // = 3.333...
```

---

## 16. Integer Division and Modulus

**Integer division** always truncates (drops the fractional part):
```cpp
15 / 2   // = 7  (not 7.5)
2 / 15   // = 0  (not 0.13...)
```

**Modulus `%`** gives the **remainder** after integer division:
```cpp
12 % 5   // = 2  (12 ÷ 5 = 2 remainder 2)
5 % 12   // = 5  (5 ÷ 12 = 0 remainder 5)
7 % 3    // = 1
```

> `%` can only be used with integer operands.

**Practical uses of modulus:**
- Check if a number is even: `n % 2 == 0`
- Extract the last digit of a number: `n % 10`
- Wrap around (cycling through values 0 to N-1): `value % N`

---

## 17. Operator Precedence and Associativity

When an expression has multiple operators, the order of evaluation follows **precedence rules**:

| Precedence | Operator | Associativity |
|---|---|---|
| 1 (highest) | `()` parentheses | Innermost first |
| 2 | `++` `--` (unary) | Right to left |
| 3 | `*` `/` `%` | Left to right |
| 4 | `+` `-` | Left to right |
| 5 (lowest) | `=` `+=` `-=` `*=` `/=` `%=` | Right to left |

**Rules:**
- Two binary operators cannot be placed side-by-side: `a * - b` needs parentheses → `a * (-b)`
- Parentheses override all precedence: use them freely for clarity
- `*` does **not** mean multiplication when used as `(a)(b)` — you must write `a * b`

**Example — step-by-step evaluation:**
```
17 % 5 + (++7) / 2 + 10 - 3
Step 1: ++7 → 8
Step 2: 17 % 5 → 2
Step 3: 8 / 2 → 4
Step 4: 2 + 4 → 6
Step 5: 6 + 10 → 16
Step 6: 16 - 3 → 13   ← Final result
```

---

## 18. Formatted Output with cout

`cout` can display numbers and text. Use `endl` or `"\n"` to move to a new line.

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << 6   << endl
         << 18  << endl
         << 124 << endl
         << "---\n"
         << (6 + 18 + 124) << endl;
    return 0;
}
```

**Output:**
```
6
18
124
---
148
```

**Field-width manipulators** (requires `#include <iomanip>`):

```cpp
#include <iomanip>
cout << setw(10) << 42;          // right-align 42 in a field of 10 chars
cout << fixed << setprecision(2) << 3.14159; // prints 3.14
cout << left << setw(10) << "Hi"; // left-align
```

---

## 19. Identifiers (Naming Variables)

An **identifier** is the name you give to a variable, function, or constant.

**Rules for valid identifiers:**
- Must **not** start with a digit
- Can contain letters, digits, and underscores `_`
- **No special characters** (no `$`, `@`, `*`, etc.)
- **Not a reserved keyword** (`while`, `int`, `if`, etc.)
- **Case-sensitive**: `MyVar` and `myvar` are different

**Valid examples:**
```
grosspay    taxCalc    addNums    degToRad
multByTwo   salesTax   netPay     bessel_j
```

**Invalid examples:**
```
4ab3    → starts with a digit
e*6     → contains special character *
while   → is a reserved keyword
```

**Good practice:** Use descriptive, camelCase or snake_case names:
```cpp
int studentAge;       // camelCase
double tax_rate;      // snake_case
```

---

## 20. Variables and Declaration Statements

A **variable** is a named memory location whose stored value can change during program execution.

### Declaration Syntax
```cpp
dataType variableName;
dataType var1, var2, var3;   // multiple variables of same type
```

**Examples:**
```cpp
int sum;
double grade1, grade2, total, average;
char letter;
bool isValid;
```

### Initialization at Declaration
```cpp
int count = 0;
double price = 9.99;
char grade = 'A';
bool flag = true;
```

**Rules:**
- A variable **must be declared before use**
- A variable can only store **one value at a time** (new assignments overwrite old ones)
- Variables should be assigned a value before being used in any expression

### Typical placement inside `main()`:
```cpp
int main() {
    // 1. symbolic constants
    const double TAX = 0.05;
    // 2. variable declarations
    int num;
    double price;
    // 3. executable statements
    cin >> num >> price;
    cout << num * price * (1 + TAX);
    return 0;
}
```

---

## 21. Constant Declarations

A **constant** is a named value that **cannot be changed** after it is set. Use the `const` keyword.

**Syntax:**
```cpp
const dataType NAME = value;
```

**Examples:**
```cpp
const float PI       = 3.14159f;
const double SALESTAX = 0.05;
const int    PSUM    = 300;
const char   STAR    = '*';
const string MONTH   = "may";
const bool   FLAG    = true;
```

Constants are also called **symbolic constants** or **named constants**. They can be used anywhere the literal value would be used:
```cpp
circum = 2 * PI * radius;
amount = SALESTAX * purchase;
```

**Invalid constant declarations:**
```cpp
// a) Duplicate identifier — a already declared
int a, b, c;
float a, d;       // ERROR: a declared twice

// b) const cannot be re-declared
const int k = 10;
int i, j, k;      // ERROR: k already declared as const

// c) 'else' is a reserved word
const float else = 13.6;  // ERROR

// d) "May" is a string, ch is a char — type mismatch
char ch = "May";  // ERROR
```

---

## 22. Assignment Operators

The **basic assignment operator** `=` stores a value in a variable.

**Syntax:**
```cpp
variable = expression;
```

- The **right side** (rvalue) is evaluated first
- The result is stored in the **left side** (lvalue)
- Only a **variable** can be an lvalue — a literal cannot be on the left

```cpp
int sum = 3 + 7;          // sum = 10
double avg = sum / 2.0;   // avg = 5.0
int tally = count + 1;    // tally = count + 1
double slope = (y2 - y1) / (x2 - x1);
```

**Invalid assignments:**
```cpp
6.8 = rate;       // ERROR: literal on left side
num + 5 = mark;   // ERROR: expression on left side
```

**Four ways to assign a value to a variable:**
```cpp
int number = 10;       // 1. Initialization at declaration
cin >> number;         // 2. Input from user (cin)
number = number * 3;   // 3. Direct calculation
number = 0;            // 4. Direct assignment
```

---

## 23. Coercion (Type Conversion)

**Coercion** happens automatically when you assign a value of one type to a variable of a different type. The value on the right is converted to the type of the variable on the left.

```cpp
int temp = 25.89;   // coercion: 25.89 → 25 (decimal part dropped!)
float x = 5;        // coercion: int 5 → float 5.0 (safe, no data loss)
```

> **Warning:** Assigning a float to an int silently truncates the decimal — the compiler may not warn you.

```cpp
int result = 7.9;    // result = 7  (not rounded, just truncated)
```

---

## 24. Abbreviated Assignment Operators

These shortcut operators combine an arithmetic operation with assignment:

| Operator | Example | Equivalent |
|---|---|---|
| `+=` | `x += 3;` | `x = x + 3;` |
| `-=` | `x -= 3;` | `x = x - 3;` |
| `*=` | `x *= y;` | `x = x * y;` |
| `/=` | `x /= y;` | `x = x / y;` |
| `%=` | `x %= y;` | `x = x % y;` |

**Examples:**
```cpp
sum += 10;       // add 10 to sum
total -= tax;    // subtract tax from total
price *= 1.05;   // increase price by 5%
count %= 10;     // keep only the remainder when divided by 10
```

---

## 25. Increment and Decrement Operators

Special unary operators for adding or subtracting **exactly 1**:

| Operator | Name | Effect |
|---|---|---|
| `++` | Increment | Adds 1 to variable |
| `--` | Decrement | Subtracts 1 from variable |

These can appear as **prefix** (before the variable) or **postfix** (after the variable):

### Prefix vs Postfix — Critical Difference

```cpp
int n = 5, k;

// PREFIX: increment first, then use
k = ++n;   // n becomes 6, then k = 6

// POSTFIX: use first, then increment
k = n++;   // k = 5, then n becomes 6
```

**Step-by-step breakdown:**
```
Prefix  ++n:   n = n + 1;  k = n;    (increment then assign)
Postfix n++:   k = n;      n = n + 1; (assign then increment)
```

**Examples with m=25, n=7:**
```
m % n++   →  25 % 7  = 4   (then n becomes 8)
m % ++n   →  25 % 8  = 1   (n incremented first to 8)
++m - n-- →  26  - 7 = 19  (m incremented to 26, then n decremented to 6)
```

> **Warning:** Never use `++` or `--` on an expression: `(count + n)++` is **invalid**. These operators can only be applied to individual variables.

---

## 26. Expressions

An **expression** is any combination of constants, variables, and operators that produces a value.

**Simple arithmetic expressions:**
```cpp
3 + 7           // value: 10
15 - 6          // value: 9
.05 * 14.6      // value: 0.73
count + 1       // value: count's value + 1
```

**Compound arithmetic expressions** (multiple operators):
```cpp
(y2 - y1) / (x2 - x1)    // slope formula
a * x * x + b * x + c     // quadratic
```

**Taxonomy of expressions:**

```
Expressions
├── Arithmetic expressions   → evaluate to a number
│   ├── Simple               → one operator
│   └── Compound             → multiple operators (precedence matters)
└── Boolean expressions      → evaluate to true or false
```

**Assignment is also an expression** in C++ — it evaluates to the value assigned:
```cpp
int x, y;
x = y = 5;   // valid: assigns 5 to y, then 5 to x (right-to-left)
```

---

## 27. Boolean Expressions

A **Boolean expression** evaluates to either `true` or `false`. They are formed using:
- **Relational operators** (compare two values)
- **Logical operators** (combine multiple Boolean values)

---

## 28. Relational Operators

Used to compare two values. Result is always `true` or `false`.

| Operator | Meaning | Example (i=5, j=-3) | Result |
|---|---|---|---|
| `==` | Equal to | `i == 5` | `true` |
| `!=` | Not equal to | `j != -2` | `true` |
| `<` | Less than | `j < i` | `true` |
| `<=` | Less than or equal | `i <= 5` | `true` |
| `>` | Greater than | `i > j` | `true` |
| `>=` | Greater than or equal | `j >= 0` | `false` |

> **Common mistake:** Use `==` to compare (two equal signs), not `=` (assignment).

```cpp
if (x = 5)   // WRONG — this assigns 5 to x, always true!
if (x == 5)  // CORRECT — this compares x to 5
```

**Arithmetic operators have higher precedence than relational operators**, so you usually don't need extra parentheses:
```cpp
i + 2.5 < j + 11    // arithmetic evaluated first, then <
i * j == -15        // * before ==
```

---

## 29. Logical Operators

Combine or negate Boolean values to form more complex conditions.

| Operator | Name | Type | Meaning |
|---|---|---|---|
| `&&` | AND | Binary | True only if **both** sides are true |
| `\|\|` | OR | Binary | True if **at least one** side is true |
| `!` | NOT | Unary | Reverses the truth value |

**Truth Tables:**

**AND (`&&`):**

| x | y | x && y |
|---|---|---|
| true | true | **true** |
| true | false | false |
| false | true | false |
| false | false | false |

**OR (`||`):**

| x | y | x \|\| y |
|---|---|---|
| true | true | **true** |
| true | false | **true** |
| false | true | **true** |
| false | false | false |

**NOT (`!`):**

| x | !x |
|---|---|
| true | false |
| false | true |

**Examples:**
```cpp
// x and y are both greater than z
(x > z) && (y > z)

// z is greater than x or y
(z > x) || (z > y)

// x is between 0 and 13 but not even
(x > 0) && (x < 13) && (x % 2 != 0)

// y is neither equal to z nor x
(y != z) && (y != x)

// x < z <= y
(x < z) && (z <= y)
```

---

## 30. Complete Operator Precedence Table

Full precedence from highest to lowest:

| Precedence | Operator(s) | Associativity |
|---|---|---|
| 1 (highest) | `()` | Innermost first |
| 2 | `++` `--` `!` (unary) | Right to left |
| 3 | `*` `/` `%` | Left to right |
| 4 | `+` `-` | Left to right |
| 5 | `<` `<=` `>` `>=` | Left to right |
| 6 | `==` `!=` | Left to right |
| 7 | `&&` | Left to right |
| 8 | `\|\|` | Left to right |
| 9 (lowest) | `=` `+=` `-=` `*=` `/=` `%=` | Right to left |

**Example evaluation (x=4, y=7, z=3, test=false):**
```
!test || ((y + z) <= (x - z))
Step 1: !false → true
Step 2: y + z → 10
Step 3: x - z → 1
Step 4: 10 <= 1 → false
Step 5: true || false → true   ← Final result
```

---

## 31. Mathematical Library Functions

Standard math functions available by including `<cmath>`:

| Function | Description | Return Type |
|---|---|---|
| `abs(x)` | Absolute value | Same as argument |
| `pow(x1, x2)` | x1 raised to the x2 power | `double` |
| `sqrt(x)` | Square root of x | `double` |
| `sin(x)` | Sine of x (x in radians) | `double` |
| `cos(x)` | Cosine of x (x in radians) | `double` |
| `tan(x)` | Tangent of x (x in radians) | `double` |
| `log(x)` | Natural logarithm of x | `double` |
| `log10(x)` | Base-10 logarithm of x | `double` |
| `exp(x)` | e raised to the x power | `double` |

**Usage:**
```cpp
#include <cmath>
#include <iostream>
using namespace std;

int main() {
    double area = 25.0;
    cout << sqrt(area);           // 5.0

    double result = pow(2.5, 3.0); // 15.625

    double t = sqrt(800.0 / 16.0);
    cout << "Time = " << t << " seconds"; // 7.0711 seconds

    return 0;
}
```

**Before using any math function, know:**
1. The function's **name**
2. **What it does**
3. The **input data type** required
4. The **return data type**

---

## 32. Type Casting

**Casting** forces a value to be treated as a different data type.

### Compile-Time Cast (C-style)
```cpp
dataType(expression)
```

### Run-Time Cast (C++ style — preferred)
```cpp
static_cast<dataType>(expression)
```

**Examples:**
```cpp
int a = 5, b = 2;

// Without cast: integer division
double result1 = a / b;                    // = 2.0 (truncated first!)

// With cast: forces floating-point division
double result2 = static_cast<double>(a) / b;  // = 2.5
double result3 = (double)a / b;               // = 2.5 (C-style)
```

**Why casting matters — the integer division trap:**
```cpp
// WRONG: 5/9 = 0 in integer division!
double celsius = (5/9) * (fahrenheit - 32);   // always 0!

// CORRECT: force floating-point division
double celsius = (5.0/9.0) * (fahrenheit - 32);
// OR
double celsius = static_cast<double>(5) / 9 * (fahrenheit - 32);
```

---

## 33. Interactive Input with cin

`cin` is the **standard input stream object** — connected to the keyboard.

**Syntax:**
```cpp
cin >> variable;
cin >> var1 >> var2;   // read multiple values
```

- `>>` is the **stream extraction operator** ("get from")
- Execution **pauses** and waits for the user to type
- User presses **Enter** to signal end of input
- Values are stored in the variables to the right of `>>`

**Example:**
```cpp
#include <iostream>
using namespace std;

int main() {
    double num1, num2;
    cout << "Please type in a number: ";
    cin >> num1;
    cout << "Please type in another number: ";
    cin >> num2;
    cout << num1 << " times " << num2 << " is " << num1 * num2 << endl;
    return 0;
}
```

**Output/interaction:**
```
Please type in a number: 2.5
Please type in another number: 5
2.5 times 5 is 12.5
```

The `cout` message before `cin` is called a **prompt** — it tells the user what to type.

**Reading multiple values at once:**
```cpp
cin >> score >> need_to_pass;   // user types: 98 60
```

---

## 34. Symbolic Constants

**Magic numbers** are literal values scattered through code with no explanation. Use named constants instead.

```cpp
// BAD — what does 0.05 mean?
total = price * 1.05;

// GOOD — self-documenting
const double SALES_TAX = 0.05;
total = price * (1 + SALES_TAX);
```

**Common examples:**
```cpp
const float  PI       = 3.14159f;
const double EULER    = 2.71828;
const double SALESTAX = 0.05;
const int    MAX_SIZE = 100;
```

Using constants:
```cpp
circum = 2 * PI * radius;
amount = SALESTAX * purchase;
```

**Benefits:**
- Code is easier to read (self-documenting)
- Easier to change: update once, takes effect everywhere
- Prevents accidental modification

---

## 35. Statement Placement Rules

### Recommended order inside `main()`:

```cpp
#include <iostream>      // preprocessor directives (outside main)
using namespace std;

int main()
{
    // 1. Symbolic constants
    const double TAX_RATE = 0.05;

    // 2. Variable declarations
    int quantity;
    double price, total;

    // 3. Executable statements
    cout << "Enter quantity: ";
    cin >> quantity;
    cout << "Enter price: ";
    cin >> price;
    total = quantity * price * (1 + TAX_RATE);
    cout << "Total: " << total << endl;

    // 4. Return value
    return 0;
}
```

**Rules:**
- A variable or constant must be **declared before** it is used
- C++ technically allows declarations anywhere in the function, but placing them at the top is best practice

---

## 36. Common Programming Errors

| Error | Description | Example |
|---|---|---|
| Undeclared variable | Using a variable without declaring it | `z = 5;` (z never declared) |
| Wrong type stored | Storing mismatched types | `char ch = "May";` (string → char) |
| Uninitialized variable | Using a variable before giving it a value | `int x; cout << x;` (undefined behavior) |
| Integer division | Expecting float result from int/int | `5/9 * F` always gives 0 |
| Mixed type confusion | Not understanding implicit conversion | `int x = 7.9;` → `x = 7` (truncated) |
| Missing `<<` separators | Forgetting `<<` between cout items | `cout << x y;` → error |
| Missing `>>` separators | Forgetting `>>` between cin items | `cin >> x y;` → error |
| Applying `++` to expression | `++` only works on single variables | `(count + n)++` is invalid |
| Assignment in condition | Using `=` instead of `==` | `if (x = 5)` — always true! |
| Swapped arguments | Logically wrong order (compiler won't catch) | `grade(min, received)` instead of `grade(received, min)` |

---

## Quick Reference Cheat Sheet

```cpp
// ── PROGRAM SKELETON ────────────────────────────────
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    // declarations
    int x = 0;
    const double PI = 3.14159;

    // input
    cin >> x;

    // processing
    double area = PI * pow(x, 2);

    // output
    cout << "Area = " << area << endl;

    return 0;
}

// ── DATA TYPES ───────────────────────────────────────
int    i = 42;
double d = 3.14;
float  f = 3.14f;
char   c = 'A';
bool   b = true;

// ── ARITHMETIC ───────────────────────────────────────
int q = 17 / 5;     // = 3 (integer division)
int r = 17 % 5;     // = 2 (remainder)
double x = 17.0/5;  // = 3.4 (float division)

// ── ASSIGNMENT SHORTCUTS ─────────────────────────────
x += 5;   x -= 5;   x *= 2;   x /= 2;   x %= 3;

// ── INCREMENT / DECREMENT ────────────────────────────
++i;   i++;   --i;   i--;
k = ++n;   // increment n first, assign to k
k = n++;   // assign to k first, then increment n

// ── BOOLEAN / RELATIONAL ─────────────────────────────
bool test = (x == 5) && (y > 0) || !(z <= 10);

// ── ESCAPE SEQUENCES ─────────────────────────────────
"\n"  // newline       "\t"  // tab
"\\"  // backslash     "\""  // double quote

// ── MATH FUNCTIONS ───────────────────────────────────
sqrt(x)       pow(x, 2)     abs(x)
sin(x)        cos(x)        log(x)

// ── TYPE CASTING ─────────────────────────────────────
double result = static_cast<double>(5) / 9;  // = 0.555...

// ── INPUT ────────────────────────────────────────────
cout << "Enter value: ";
cin >> x;
```
