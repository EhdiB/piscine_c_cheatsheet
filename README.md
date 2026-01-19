# Beginner C Pattern Sheet (Piscine Edition)

## 📖 Introduction: What Is This Document?

### Who Is This For?

This guide is designed for **absolute beginners** starting their first 2 weeks of the **42 Piscine** (a 26-day intensive coding bootcamp). If you:
- Have never written C code before
- Are learning programming for the first time
- Need help understanding basic C concepts
- Want to see patterns used in 42 exercises

**Then this document is for you!**

### What This Document Covers

This is a **practical, pattern-based learning guide** that teaches you:

1. **Basic C syntax** (variables, loops, conditionals, functions)
2. **How to structure C files** for 42 exercises
3. **String manipulation** (the most common task in early exercises)
4. **Pointers** (explained step-by-step with visual examples)
5. **Common code patterns** you'll reuse constantly
6. **How to avoid beginner mistakes**

**Everything is based on actual exercises** from the first 2 weeks of piscine (C00, C01, C02, C03 modules).

### What This Document Does NOT Cover

This is **not** a complete C programming textbook. It does not cover:
- Advanced topics (linked lists, file I/O, system calls beyond `write()`)
- Memory allocation (`malloc`/`free`) - not needed in first 2 weeks
- Header files (`.h` files) - covered briefly at the end as "next steps"
- Complex data structures
- Full C language reference

**Focus:** Practical patterns for solving 42 piscine exercises in your first 2 weeks.

### How to Use This Document

1. **Read sections in order** - concepts build on each other
2. **Keep it open while coding** - use as a quick reference
3. **Study the examples** - they're from real exercises
4. **Practice the patterns** - try modifying the code examples
5. **Check the glossary** - if you see an unfamiliar term, look it up

### About the Examples

All code examples in this document come from analyzing actual exercise solutions from a 42 piscine repository (a collection of exercise files). The patterns shown are what you'll actually use to solve similar problems.

**Note:** Some examples may contain bugs - we'll point these out so you can learn from mistakes!

---

## 📚 Quick Lexicon (Glossary)

**Before you start, here are key terms you'll encounter:**

| Term | Definition |
|------|------------|
| **42 / 42 Piscine** | A 26-day intensive coding bootcamp where you learn C programming through daily exercises |
| **Repository (repo)** | A folder containing code files - in this case, exercise solutions organized by module (C00, C01, etc.) |
| **Module** | A group of related exercises (e.g., C00 = basic output, C01 = pointers introduction) |
| **Exercise** | A single programming task (e.g., "write a function that prints a character") |
| **Function** | A reusable block of code that performs a specific task |
| **Variable** | A named storage location that holds a value (like a labeled box) |
| **Pointer** | A variable that stores a memory address (like a street address) |
| **String** | A sequence of characters (text) in C, always ending with `'\0'` |
| **Array** | A collection of items stored in consecutive memory locations |
| **NUL terminator** | The `'\0'` character that marks the end of a string |
| **Dereference** | Using `*` to get the value at a memory address |
| **Address-of** | Using `&` to get the memory address of a variable |
| **Compile** | Converting your C code into an executable program |
| **Syntax** | The rules for writing valid C code (like grammar for a language) |
| **Header file** | A file (`.h`) that declares functions for use in other files |
| **Include** | Adding code from another file using `#include` |
| **Function signature** | The declaration showing return type, name, and parameters |
| **Parameter** | A value passed to a function |
| **Return value** | The result a function gives back |
| **Loop** | Code that repeats until a condition is met |
| **Conditional** | Code that runs only if a condition is true (`if`/`else`) |
| **Index** | A number used to access a specific position in an array/string |
| **Buffer** | A temporary storage area in memory |
| **Buffer overflow** | Writing past the end of allocated memory (dangerous bug) |
| **NULL pointer** | A pointer that doesn't point to anything (value: `NULL`) |
| **Undefined behavior** | Code that might work sometimes but isn't guaranteed (dangerous) |
| **ASCII** | A system where each character has a number (e.g., 'A' = 65) |
| **File descriptor** | A number representing an open file/stream (1 = screen output) |
| **Stdout** | Standard output - where your program prints (usually the screen) |

**Don't worry if you don't understand all terms yet - they'll be explained as you read!**

---

## A. File Anatomy

### What Goes in a `.c` File

**What is a `.c` file?** A `.c` file is a **source code file** containing C programming code. It's the file you write your program in, which gets compiled (converted) into an executable program.

Every `.c` file in this repository (collection of exercise files) follows this structure:

```c
/* ************************************************************************** */
/*                                                                            */
/*                                                        :::      ::::::::   */
/*   filename.c                                          :+:      :+:    :+:   */
/*                                                    +:+ +:+         +:+     */
/*   By: author <email@42.fr>                         +#+  +:+       +#+        */
/*                                                +#+#+#+#+#+   +#+           */
/*   Created: YYYY/MM/DD HH:MM:SS by author            #+#    #+#             */
/*   Updated: YYYY/MM/DD HH:MM:SS by author            ###   ########.fr       */
/*                                                                            */
/* ************************************************************************** */
#include <unistd.h>

void	ft_function_name(parameters)
{
	// Your code here
}
```

**Key points:**
- **Header block**: Required 42-style header (author, dates, etc.) - a comment block at the top of every file
- **Includes**: At the top, after header - `#include` statements that add library functions
- **Function**: One main function matching the filename - the code that does the work
- **Style**: Tabs (not spaces), braces on new lines - formatting rules required by 42

**Minimal example:**
```c
#include <unistd.h>

void	ft_hello(void)
{
	write(1, "Hello", 5);
}
```

---

## B. Importing / Includes

### What an Include Is

**What is `#include`?** `#include` is a **preprocessor directive** (special instruction) that copies code from another file into yours before compilation. Think of it like importing a toolbox - you're adding tools (functions) you can use.

```c
#include <unistd.h>  // Gives you write() function
```

**What is a library?** A library is a collection of pre-written functions you can use. `<unistd.h>` is a standard library that provides the `write()` function for output.

### Headers Observed in This Repository

**What is a header?** A header file (`.h` file) contains declarations of functions. When you `#include` it, you're telling your program "these functions exist and you can use them."

| Header | Purpose | Evidence | When to Use |
|--------|---------|----------|-------------|
| `<unistd.h>` | Provides `write()` function | Used in **all** files | **Always** - for output |
| `<stdio.h>` | Provides `printf()`, etc. | Only in **commented test code** | **Likely forbidden** in submissions |
| `<string.h>` | String functions | Found once (`c_03/ex04/ft_strstr.c:14`) | **Likely mistake** - forbidden |

**Rule of thumb:** Use `<unistd.h>` for `write()`. Avoid `<stdio.h>` (use `write()` instead of `printf()`).

**Example:**
```c
#include <unistd.h>  // Good - needed for write()

void	ft_example(void)
{
	write(1, "Hello", 5);  // write() comes from unistd.h
}
```

---

## C. Variables & Types (Beginner-Friendly)

### Basic Types You'll Use

**What is a type?** A **type** tells the computer what kind of data a variable can hold and how much memory it needs.

| Type | Stores | Example | Size |
|------|--------|---------|------|
| `int` | Whole numbers (integers) | `42`, `-5`, `0` | Usually 4 bytes |
| `char` | Single character | `'a'`, `'0'`, `'\0'` | 1 byte |
| `char*` | String (pointer to characters) | `"Hello"`, `str` | 8 bytes (pointer) |

**What is a byte?** A byte is a unit of memory. One byte can store one character. Larger types use more bytes.

### Declaration + Initialization

**What is declaration?** **Declaration** means telling the computer "I want a variable with this name and type."  
**What is initialization?** **Initialization** means giving a variable its first value.

**Declare then assign:**
```c
int	age;
age = 25;
```

**Declare and initialize:**
```c
int	age = 25;
char	c = 'a';
char	*str = "Hello";
```

**Multiple variables:**
```c
int	i;
int	j;
int	k;

// Or:
int	i, j, k;
```

### Common Mistakes

**1. Uninitialized variable:**
```c
int	i;  // Wrong: Value is garbage
while (i < 10)  // Undefined behavior!

// Fix:
int	i = 0;
while (i < 10)
```

**2. Wrong type:**
```c
char	c = 65;  // Works, but confusing
char	c = 'A';  // Better - same value (65)
```

**3. Mixing signed/unsigned:**
```c
int		len = -1;
unsigned int	size = 10;
if (len < size)  // -1 becomes huge unsigned number!

// Fix: Use consistent types
int	len = -1;
int	size = 10;
```

---

## D. Loops (Patterns You'll Use Constantly)

### while Loop Template (Especially for Strings)

**What is a loop?** A **loop** repeats code multiple times until a condition becomes false.

**Most common pattern in the repository:**
```c
int	i;

i = 0;
while (str[i] != '\0')
{
	// Do something with str[i]
	i++;
}
```

**Why this works:** Strings end with `'\0'`. Loop until you hit it.

**Example (from the repository):**
```c
void	ft_putstr(char *str)
{
	int	i;

	i = 0;
	while (str[i] != '\0')  // Loop until end of string
	{
		write(1, &str[i], 1);
		i++;  // Move to next character
	}
}
```

### for Loop Template (If Used)

**Less common in the repository, but useful:**
```c
for (initialization; condition; increment)
{
	// Body
}
```

**Example:**
```c
int	i;

for (i = 0; i < 10; i++)
{
	write(1, &i, 1);
}
```

**Equivalent while:**
```c
int	i;

i = 0;
while (i < 10)
{
	write(1, &i, 1);
	i++;
}
```

**Repository preference:** `while` loops are more common in these exercises.

### Common Loop Mistakes

**1. Off-by-one:**
```c
// Wrong: Goes one too far
int	i = 0;
while (i <= size)  // Accesses arr[size] (out of bounds!)
{
	arr[i] = 0;
	i++;
}

// Correct:
int	i = 0;
while (i < size)  // Stops at size-1
{
	arr[i] = 0;
	i++;
}
```

**2. Infinite loop (forgetting increment):**
```c
// Wrong: i never changes!
int	i = 0;
while (i < 10)
{
	write(1, "loop", 4);
	// Forgot i++!
}

// Correct:
int	i = 0;
while (i < 10)
{
	write(1, "loop", 4);
	i++;  // Don't forget!
}
```

---

## E. Conditionals

### if / else Basics

```c
if (condition)
{
	// Do this if true
}
else
{
	// Do this if false
}
```

**Common patterns in the repository:**

**1. Simple check:**
```c
if (n < 0)
	write(1, "N", 1);
else
	write(1, "P", 1);
```

**2. Multiple conditions:**
```c
if (c >= 'a' && c <= 'z')  // AND
	return (1);
if (c >= 'A' && c <= 'Z')  // OR (separate if)
	return (1);
return (0);
```

**3. Nested if:**
```c
if (nb == -2147483648)
{
	write(1, "-2147483648", 11);
}
else if (nb < 0)
{
	write(1, "-", 1);
	nb = -nb;
}
```

### Common Comparison Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| `==` | Equal | `if (x == 5)` |
| `!=` | Not equal | `if (str[i] != '\0')` |
| `<` | Less than | `if (i < size)` |
| `<=` | Less or equal | `if (c <= 'z')` |
| `>` | Greater than | `if (x > 0)` |
| `>=` | Greater or equal | `if (c >= 'a')` |
| `&&` | AND | `if (x > 0 && x < 10)` |
| `\|\|` | OR | `if (c == 'a' \|\| c == 'A')` |

**Character range checks (very common):**
```c
if (c >= 'a' && c <= 'z')  // Lowercase letter
if (c >= 'A' && c <= 'Z')  // Uppercase letter
if (c >= '0' && c <= '9')  // Digit
```

---

## F. Functions

### Function Signature Basics

**What is a function signature?** A **function signature** is the declaration that shows:
- **Return type**: What kind of value the function gives back (or `void` if nothing)
- **Function name**: What you call it
- **Parameters**: What values you pass to it

```c
return_type	function_name(parameter_type parameter_name)
{
	// Body - the code that does the work
	return (value);  // If return_type is not void
}
```

**What is a parameter?** A **parameter** (also called "argument") is a value you pass to a function when you call it.

**Example:**
```c
int	ft_strlen(char *str)  // Returns int, takes char* parameter
{
	int	i;

	i = 0;
	while (str[i] != '\0')
		i++;
	return (i);  // Return the length
}
```

**Return types:**
- `void` = returns nothing
- `int` = returns a number
- `char*` = returns a pointer (often the string you modified)

### Passing by Value (Copy)

**By value (copy):**
```c
void	ft_add_one(int n)
{
	n = n + 1;  // Only changes local copy
}

int	main(void)
{
	int	x = 5;
	ft_add_one(x);
	// x is still 5! (not changed)
}
```

**Why this happens:** Function gets a **copy** of the value. Changes don't affect original.

### Write Small Helpers Pattern

**Observed in the repository:** Functions call other helper functions.

**Example:**
```c
void	ft_putchar(char c)  // Helper
{
	write(1, &c, 1);
}

void	ft_putnbr(int nb)  // Uses helper
{
	if (nb >= 10)
	{
		ft_putnbr(nb / 10);
		ft_putchar((nb % 10) + '0');  // Uses helper
	}
	else
		ft_putchar(nb + '0');
}
```

**Why:** Break problems into smaller pieces. Reuse code.

---

## G. Strings (NUL-Terminated)

### What a C String Is

**What is a string?** A **string** is text - a sequence of characters. In C, a string is an **array of characters ending with `'\0'`** (NUL terminator).

**What is an array?** An **array** is a collection of items stored in consecutive memory locations. You access items by their position (index).

```c
char	str[] = "Hello";
// Actually: ['H', 'e', 'l', 'l', 'o', '\0']
//           [ 0,   1,   2,   3,   4,   5  ]
```

**Key point:** The `'\0'` (NUL terminator) marks the end of the string. It's not printed, but must be there. Without it, the computer doesn't know where the string ends!

### How to Traverse Safely

**What is traversing?** **Traversing** means going through each element of a string or array, one by one.

**Standard pattern (from the repository):**
```c
int	i;

i = 0;
while (str[i] != '\0')  // Stop at terminator
{
	// Process str[i]
	i++;
}
```

**Why safe:** Stops at `'\0'`, won't go past end.

### Typical Edge Cases

**1. NULL pointer:**
**What is NULL?** `NULL` is a special value meaning "this pointer doesn't point to anything." Trying to use a NULL pointer crashes your program.

```c
// Crashes if str is NULL:
int	i = 0;
while (str[i] != '\0')  // Dereferences NULL! (tries to access invalid memory)

// Check first (if required by exercise):
if (str == NULL)
	return (0);
int	i = 0;
while (str[i] != '\0')
```

**2. Empty string:**
```c
char	*str = "";  // Contains only '\0'
// Length is 0, but str[0] == '\0' is true
```

**3. Missing terminator:**
```c
char	arr[5] = {'H', 'e', 'l', 'l', 'o'};  // No '\0'!
// This is NOT a valid string - undefined behavior when reading

// Fix:
char	arr[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
// Or:
char	arr[] = "Hello";  // Automatically includes '\0'
```

---

## H. Pointers (EXPANDED - Step by Step)

> **This is where many beginners get stuck. Read this carefully!**

### What is a Pointer? (The Address Analogy)

**What is a pointer?** A **pointer** is a variable that stores a memory address instead of a value. Think of it as a piece of paper with a street address written on it, rather than the house itself.

**What is memory?** **Memory** (RAM) is where your computer stores data while your program runs. Think of memory like a street with numbered houses (addresses). A variable is a house with a value inside. A pointer is a piece of paper with the house address written on it.

```
Memory (the street):
┌─────────┬─────────┬─────────┬─────────┐
│ Address │  1000   │  1004   │  1008   │
│ Value   │   42    │   ???   │   ???   │
│ Name    │  value  │         │   ptr   │
└─────────┴─────────┴─────────┴─────────┘
```

**In code:**
```c
int	value = 42;      // House at address 1000 contains 42
int	*ptr = &value;   // ptr is a paper saying "address 1000"
```

### The Two Operators: `&` and `*`

**What is an operator?** An **operator** is a symbol that performs an operation (like `+` for addition).

**`&` (address-of operator):** "Give me the address of this variable"  
**What does `&` do?** The `&` operator gets the memory address where a variable is stored.
```c
int	x = 5;
int	*ptr = &x;  // ptr now holds the address of x
```

**`*` (dereference operator):** "Go to this address and get/change the value"  
**What does `*` do?** The `*` operator (when used with a pointer) follows the address to get or modify the value stored there. This is called **dereferencing**.
```c
int	x = 5;
int	*ptr = &x;  // ptr points to x
*ptr = 10;      // Go to address in ptr, change value to 10
// Now x is 10!
```

### Visual Step-by-Step Example

```c
int	value = 42;
int	*ptr = &value;
*ptr = 100;
```

**Step 1:** `int value = 42;`
```
Memory:
┌─────────┐
│ Address: 1000
│ Value:   42
│ Name:    value
└─────────┘
```

**Step 2:** `int *ptr = &value;`
```
Memory:
┌─────────┐     ┌─────────┐
│ Address: 1000 │ Address: 2000
│ Value:   42   │ Value:   1000  ← address of value!
│ Name:    value│ Name:    ptr
└─────────┘     └─────────┘
                 (points to)
```

**Step 3:** `*ptr = 100;`
```
Memory:
┌─────────┐     ┌─────────┐
│ Address: 1000 │ Address: 2000
│ Value:   100  │ Value:   1000
│ Name:    value│ Name:    ptr
└─────────┘     └─────────┘
   ↑ Changed!   (still points here)
```

### Why Do We Need Pointers?

**Why use pointers?** Pointers let functions modify variables that are passed to them. Without pointers, functions only get copies of values.

**Problem:** Functions can't modify variables passed by value.

```c
void	ft_change(int n)
{
	n = 100;  // Only changes local copy
}

int	main(void)
{
	int	x = 5;
	ft_change(x);
	// x is still 5! ❌
}
```

**Solution:** Pass the address (pointer), so function can modify original.

```c
void	ft_change(int *n)  // Receives address
{
	*n = 100;  // Go to address, change value
}

int	main(void)
{
	int	x = 5;
	ft_change(&x);  // Pass address of x
	// x is now 100! ✅
}
```

### First Pointer Exercise Pattern (from the repository)

**`ft_ft` - Simplest pointer example:**
```c
void	ft_ft(int *nbr)  // Receives pointer (address)
{
	*nbr = 42;  // Dereference: go to address, set value to 42
}
```

**How to call it:**
```c
int	number = 0;
ft_ft(&number);  // Pass address of number
// number is now 42!
```

**What happens:**
1. `&number` gives address of `number`
2. Function receives that address in `nbr`
3. `*nbr = 42` goes to that address and changes value
4. Original `number` is now 42

### Swap Pattern (Classic Pointer Example)

**From the repository:** `c_01/ex02/ft_swap.c`

```c
void	ft_swap(int *a, int *b)
{
	int	temp;

	temp = *a;   // Save value at address a
	*a = *b;     // Copy value from b to a
	*b = temp;   // Copy saved value to b
}
```

**Visual explanation:**
```
Before swap:
a → [5]  (address 1000)
b → [10] (address 1004)

After temp = *a:
temp = 5
a → [5]
b → [10]

After *a = *b:
temp = 5
a → [10]  ← changed!
b → [10]

After *b = temp:
temp = 5
a → [10]
b → [5]   ← changed!
```

### Pointers and Strings

**Important:** In C, strings are pointers to characters!

```c
char	*str = "Hello";
// str is a pointer to the first character 'H'
```

**Why this works:**
- `str[0]` is same as `*str` (first character)
- `str[1]` is same as `*(str + 1)` (next character)
- String functions receive `char *` (pointer to first char)

**Example from repo:**
```c
void	ft_putstr(char *str)  // Receives pointer to first char
{
	int	i;

	i = 0;
	while (str[i] != '\0')  // Can use indexing with pointer
	{
		write(1, &str[i], 1);
		i++;
	}
}
```

### Common Pointer Mistakes (Beginners Make These!)

**1. Forgetting `&` when passing address:**
```c
void	ft_change(int *n)
{
	*n = 100;
}

int	main(void)
{
	int	x = 5;
	ft_change(x);  // ❌ Wrong! Passes value, not address
	// Compiler error or crash

	ft_change(&x);  // ✅ Correct! Passes address
}
```

**2. Using `*` when you shouldn't:**
```c
int	x = 5;
int	*ptr = &x;

int	y = *ptr;   // ✅ Correct: get value
int	y = ptr;    // ❌ Wrong: assigns address (wrong type)
```

**3. Dereferencing NULL or uninitialized pointer:**
```c
int	*ptr;        // ❌ Not initialized!
*ptr = 5;        // Crash! ptr points to random memory

int	*ptr = NULL;  // ❌ Points to nothing
*ptr = 5;        // Crash! Can't write to NULL

// ✅ Fix:
int	*ptr;
int	value = 5;
ptr = &value;    // Now ptr points to valid memory
*ptr = 10;       // Safe!
```

**4. Confusing `*` in declaration vs usage:**
```c
int	*ptr;        // Declaration: * means "pointer to int"
*ptr = 5;        // Usage: * means "dereference (get value)"
```

**5. Wrong type when passing:**
```c
void	ft_swap(int *a, int *b)  // Expects pointers
{
	// ...
}

int	main(void)
{
	int	x = 5, y = 10;
	ft_swap(x, y);     // ❌ Wrong: passing values
	ft_swap(&x, &y);   // ✅ Correct: passing addresses
}
```

### Pointer Declaration Patterns

**Single pointer:**
```c
int	*ptr;        // Pointer to int
char	*str;       // Pointer to char (string)
```

**Multiple pointers (each needs *):**
```c
int	*a, *b, *c;  // Three pointers to int
// NOT: int *a, b, c;  (only a is pointer!)
```

**Pointer to pointer (advanced - seen in `ft_ultimate_ft`):**
```c
int	**ptr;       // Pointer to pointer to int
// Used when you need to modify a pointer itself
```

### Quick Reference: Pointer Rules

| Situation | Syntax | Meaning |
|-----------|--------|---------|
| Declare pointer | `int *ptr;` | `ptr` is a pointer to int |
| Get address | `&variable` | Address of `variable` |
| Get value | `*ptr` | Value at address in `ptr` |
| Change value | `*ptr = 5;` | Set value at address to 5 |
| Pass to function | `func(&x)` | Pass address of `x` |
| Receive in function | `void func(int *n)` | Function receives address |

---

## I. Arrays & Pointers (Connecting the Concepts)

### Arrays vs Pointers (Practical Viewpoint)

**Arrays:**
```c
int	arr[5] = {1, 2, 3, 4, 5};
// arr[0] = 1, arr[1] = 2, etc.
```

**Pointers to arrays:**
```c
int	arr[5] = {1, 2, 3, 4, 5};
int	*ptr = arr;  // Points to first element
// ptr[0] = 1, ptr[1] = 2 (same as arr)
```

**For strings:**
```c
char	*str = "Hello";  // str is a pointer
// str[0] = 'H', str[1] = 'e', etc.
```

**Key insight:** Arrays and pointers work similarly for indexing. `arr[i]` and `ptr[i]` both work.

### Indexing Patterns You'll See

**1. Sequential access:**
```c
int	i = 0;
while (i < size)
{
	arr[i] = 0;  // Set each element to 0
	i++;
}
```

**2. Reverse access:**
```c
int	i = size - 1;  // Start from last element
while (i >= 0)
{
	arr[i] = 0;
	i--;
}
```

**3. Pair swapping (from the repository):**
```c
int	i = 0;
while (i < (size / 2))  // Only swap half
{
	temp = arr[size - 1 - i];  // Last element
	arr[size - 1 - i] = arr[i];  // Move first to last
	arr[i] = temp;  // Move last to first
	i++;
}
```

---

## J. Output / Debugging

### How Output Is Done in This Repository

**Evidence:** All output uses `write()`, never `printf()`.

**`write()` function:**
**What is `write()`?** `write()` is a function that outputs data. It's the only output function you're allowed to use in 42 exercises (not `printf()`).

```c
write(fd, buffer, count);
// fd = file descriptor (1 = stdout/screen, 2 = stderr/error output)
// buffer = what to write (address of data)
// count = how many bytes to write
```

**What is stdout?** **Stdout** (standard output) is where your program normally prints - usually the screen/terminal.

**Examples from the repository:**
```c
write(1, &c, 1);           // Write 1 character
write(1, "Hello", 5);      // Write 5 characters
write(1, "\n", 1);         // Write newline
write(1, "-2147483648", 11);  // Write 11 characters
```

**Why `&c` for single char?**
- `write()` needs an **address**, not the value
- `&c` gives address of `c`
- For strings, the name is already an address: `"Hello"` or `str`

### Tiny Debugging Tricks

**1. Print a character:**
```c
char	debug = 'X';
write(1, &debug, 1);  // See if code reaches here
```

**2. Print a number (simple):**
```c
int	n = 42;
char	c = n + '0';  // Only works for 0-9!
write(1, &c, 1);
```

**3. Print a string marker:**
```c
write(1, "DEBUG: reached here\n", 20);
```

---

## K. Common Patterns Index

> **The core of this sheet.** Quick lookup for reusable code patterns.

---

### Pattern: Iterate String

**When to use:** Process each character in a string.

**Template:**
```c
int	i;

i = 0;
while (str[i] != '\0')
{
	// Process str[i]
	i++;
}
```

**Pitfalls:**
- Forgetting `i++` → infinite loop
- Not handling NULL pointer
- Accessing `str[i]` after loop without checking

**Example:** `c_01/ex05/ft_putstr.c:16-24`

---

### Pattern: Copy String

**When to use:** Copy one string to another.

**Template:**
```c
int	i;

i = 0;
while (src[i] != '\0')
{
	dest[i] = src[i];
	i++;
}
dest[i] = '\0';  // CRITICAL: Add terminator!
```

**Pitfalls:**
- Forgetting NUL terminator
- No size check (buffer overflow risk)
- Not handling NULL pointers

**Example:** `c_02/ex00/ft_strcpy.c:19-26`

---

### Pattern: String Length

**When to use:** Count characters in string.

**Template:**
```c
int	i;

i = 0;
while (str[i] != '\0')
	i++;
return (i);  // Not i+1! (NUL not counted)
```

**Pitfalls:**
- Returning `i + 1` (wrong - NUL not included in length)
- Not handling NULL

**Example:** `c_01/ex06/ft_strlen.c:14-24`

---

### Pattern: Compare Strings

**When to use:** Check if two strings are equal or compare lexicographically.

**Template:**
```c
while (*s1 == *s2 && *s1 != '\0')
{
	s1++;
	s2++;
}
return (*s1 - *s2);  // Negative if s1 < s2, 0 if equal, positive if s1 > s2
```

**Pitfalls:**
- Returning `s2 - s1` (wrong order)
- Not handling NULL
- Signed char overflow (rare)

**Example:** `c_03/ex00/ft_strcmp.c:15-23`

---

### Pattern: Swap (Using Pointers)

**When to use:** Exchange values of two variables.

**Template:**
```c
int	temp;

temp = *a;
*a = *b;
*b = temp;
```

**Pitfalls:**
- Forgetting temp variable
- Wrong order of assignments
- Forgetting `&` when calling

**Example:** `c_01/ex02/ft_swap.c:14-21`

---

### Pattern: Reverse Array

**When to use:** Reverse elements in array in-place.

**Template:**
```c
int	i;
int	temp;

i = 0;
while (i < (size / 2))  // Only swap half
{
	temp = arr[size - 1 - i];
	arr[size - 1 - i] = arr[i];
	arr[i] = temp;
	i++;
}
```

**Pitfalls:**
- Using `i <= size / 2` (double-swaps middle if odd)
- Wrong index calculation

**Example:** `c_01/ex07/ft_rev_int_tab.c:14-27`

---

### Pattern: Character Classification

**When to use:** Check if character is letter, digit, etc. (can't use `isalpha()`).

**Template:**
```c
// Check if lowercase
if (c >= 'a' && c <= 'z')
	return (1);

// Check if uppercase
if (c >= 'A' && c <= 'Z')
	return (1);

// Check if digit
if (c >= '0' && c <= '9')
	return (1);
```

**Pitfalls:**
- Using magic numbers instead of characters (`97` vs `'a'`)
- Wrong ranges (off-by-one)

**Example:** `c_02/ex02/ft_str_is_alpha.c:22`

---

### Pattern: Case Conversion

**When to use:** Convert letter to uppercase or lowercase.

**Template:**
```c
// To uppercase
if (c >= 'a' && c <= 'z')
	c = c - 32;  // Or: c = c - ('a' - 'A')

// To lowercase
if (c >= 'A' && c <= 'Z')
	c = c + 32;  // Or: c = c + ('a' - 'A')
```

**Why:** ASCII difference between 'a' and 'A' is 32.

**Pitfalls:**
- Modifying non-letters
- Wrong direction (+ vs -)

**Example:** `c_02/ex07/ft_strupcase.c:19-27`

---

### Pattern: Print Number

**When to use:** Print integer using only `write()` (no `printf()`).

**Template:**
```c
void	ft_putchar(char c)
{
	write(1, &c, 1);
}

void	ft_putnbr(int nb)
{
	if (nb == -2147483648)  // INT_MIN special case
	{
		write(1, "-2147483648", 11);
		return;
	}
	if (nb < 0)
	{
		write(1, "-", 1);
		nb = -nb;
	}
	if (nb >= 10)
	{
		ft_putnbr(nb / 10);  // Recursive: print higher digits
		ft_putchar((nb % 10) + '0');  // Print last digit
	}
	else
		ft_putchar(nb + '0');
}
```

**Pitfalls:**
- Forgetting INT_MIN case → overflow
- Not converting digit to char (`+ '0'`)

**Example:** `c_00/ex07/ft_putnbr.c:19-40`

---

## Quick Reference: ASCII Values

| Character | Decimal | Use Case |
|-----------|---------|----------|
| `'0'` | 48 | Digits start |
| `'9'` | 57 | Digits end |
| `'A'` | 65 | Uppercase start |
| `'Z'` | 90 | Uppercase end |
| `'a'` | 97 | Lowercase start |
| `'z'` | 122 | Lowercase end |
| `' '` | 32 | Space (first printable) |
| `'\0'` | 0 | String terminator |
| `'\n'` | 10 | Newline |

**Case conversion:** `'a' - 'A' = 32` (add 32 for lowercase, subtract for uppercase)

---

## Quick Reference: Common Mistakes Checklist

Before submitting, check:

- [ ] All strings null-terminated? (`dest[i] = '\0'`)
- [ ] Loop variables incremented? (`i++` inside loop)
- [ ] Array bounds checked? (`i < size` not `i <= size`)
- [ ] Pointers: Used `&` when passing address? (`func(&x)` not `func(x)`)
- [ ] Pointers: Used `*` when dereferencing? (`*ptr = 5` not `ptr = 5`)
- [ ] NULL pointers handled? (if required)
- [ ] Division by zero checked? (if dividing)
- [ ] INT_MIN handled? (if negating integers)
- [ ] Return statement present? (if function returns value)
- [ ] Correct return type? (`int` vs `char*` vs `void`)
- [ ] Includes correct? (`<unistd.h>` for `write()`)
- [ ] Header format correct? (42 style)

---

## L. Next Steps: Header Files (Advanced)

> **Skip this section for your first 2 weeks. Come back later!**

### What Goes in a `.h` File

**What is a `.h` file?** A **header file** (`.h` file) contains function declarations (not the actual code, just the signatures). It's used when you have multiple files that need to share functions.

**Evidence from repository:** No `.h` files found in early exercises.  
**When you'll need it:** Later projects (libft, etc.) when you have multiple files.

**Typical structure:**
```c
#ifndef FT_EXAMPLE_H
# define FT_EXAMPLE_H

void	ft_function_name(int param);

#endif
```

**Purpose:**
- Declare function prototypes (so other files know what functions exist)
- Share constants, types, etc.
- Include in `.c` files: `#include "ft_example.h"`

**What is a function prototype?** A **function prototype** is a declaration that tells the compiler a function exists, what it returns, and what parameters it takes - without showing the actual code.

**Note:** For now, focus on single-file exercises. Headers come later!

---

**Last tip:** When stuck, look for similar patterns in the repository. Most exercises reuse the same building blocks!

---

## 📖 Need Help? Check the Glossary

If you encounter any term you don't understand, scroll back to the **Quick Lexicon (Glossary)** section at the beginning of this document. All technical terms are defined there, and many are also explained inline when first introduced.

**Remember:** Learning to program takes practice. Don't be discouraged if concepts don't click immediately. Keep coding, keep referring to this guide, and you'll get it!
