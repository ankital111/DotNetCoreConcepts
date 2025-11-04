# C# Core Concepts (Q&A with Examples)

This guide helps you understand and revise C# fundamentals with clear answers, examples, and additional cross-questions often asked .

---

## 🟩 1. C# Overview

**Q1. What is C# and why is it used?**  
C# (pronounced *C Sharp*) is an object-oriented, type-safe, modern programming language developed by Microsoft.  
It’s mainly used for:
- Building web, desktop, mobile, and cloud applications.  
- Game development with Unity.  
- Runs on the .NET Framework or .NET Core (now unified as .NET 5+).

**Example:**
```csharp
using System;
class HelloWorld
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

**Cross Question:**  
👉 Why is C# called a type-safe language?  
Because it prevents type errors by ensuring variables are used according to their declared data types at compile-time.

---

**Q2. How is C# different from Java?**

| Feature | C# | Java |
|----------|----|------|
| Platform | .NET CLR | JVM |
| Memory Mgmt | Garbage Collected | Garbage Collected |
| Delegates/Events | Supported | Not natively supported |
| Properties | Built-in | Not built-in |
| Evolving | Rapid (Microsoft updates often) | Slower |

**Cross Question:**  
👉 Can C# run on JVM?  
No, C# runs on the CLR (Common Language Runtime). But tools like IKVM used to allow Java interoperability.

---

**Q3. What platforms can C# run on?**  
- Windows (.NET Framework)  
- Cross-platform (.NET Core / .NET 5/6/7/8)  
- Mobile (Xamarin / MAUI)  
- Web (ASP.NET Core)  

---

## 🟩 2. Structure of a C# Program

**Q1. What are namespaces, classes, and methods?**
- **Namespace**: Logical grouping of classes (like a folder).  
- **Class**: Blueprint of objects (contains data and methods).  
- **Method**: Block of code that performs an action.

**Example:**
```csharp
namespace DemoApp
{
    class Program
    {
        static void Main()
        {
            Console.WriteLine("Hi!");
        }
    }
}
```

**Cross Question:**  
👉 Can a namespace contain another namespace?  
Yes, namespaces can be nested.

---

**Q2. Why do we use `Main()` method? Can a C# program have multiple Main methods?**  
`Main()` is the entry point of execution.  
Yes, multiple classes can have `Main()` but only one is defined as the startup in project settings.

**Cross Question:**  
👉 Can `Main()` return a value?  
Yes, it can return `int` to indicate status (0 = success).

---

## 🟩 3. Data Types

**Q1. What are value types and reference types?**  
- **Value Types:** Stored directly in memory (int, float, struct, bool).  
- **Reference Types:** Store memory reference (class, string, array, object).

**Cross Question:**  
👉 Where are these stored?  
Value types → Stack, Reference types → Heap.

---

**Q2. What happens when you assign one struct to another?**  
A **copy** is made (since structs are value types).

**Example:**
```csharp
struct Point { public int X, Y; }
Point p1 = new Point { X = 10, Y = 20 };
Point p2 = p1;
p2.X = 50; // Does not affect p1
```

---

**Q3. Difference between `int` and `Int32`?**  
No difference. Both represent 32-bit integers.  
`int` → keyword alias for `System.Int32`.

---

## 🟩 4. Variables & Constants

**Q1. Difference between `var`, `dynamic`, and `object`**

| Type | Compile-time | Runtime | Type Safety |
|------|---------------|----------|--------------|
| `var` | Known | Known | Strongly typed |
| `dynamic` | Unknown | Determined at runtime | Weakly typed |
| `object` | Known | Can store any type | Requires casting |

**Cross Question:**  
👉 Can `var` be null?  
No, unless used with nullable types.

---

**Q2. When should you use `var` vs explicit typing?**  
- Use `var` when type is obvious from right-hand side.  
- Use explicit typing for clarity and readability.

---

**Q3. Can constants be assigned at runtime?**  
No. `const` must be assigned at compile-time.  
Use `readonly` for runtime constants.

---

## 🟩 5. Operators

**Q1. What types of operators are available in C#?**  
Arithmetic, Logical, Comparison, Bitwise, Assignment, Conditional (`?:`), Null (`??`), and Null-conditional (`?.`).

---

**Q2. Difference between `==` and `Equals()`?**  
- `==` compares **values or references** (depending on type).  
- `Equals()` checks for **content equality** and can be overridden.

**Example:**
```csharp
string a = "Hi", b = "Hi";
Console.WriteLine(a == b);     // True
Console.WriteLine(a.Equals(b)); // True
```

**Cross Question:**  
👉 If you override `Equals()`, should you override `GetHashCode()`?  
Yes, to maintain consistency in collections.

---

**Q3. What are `??` and `?.` operators?**
- `??`: Null coalescing — provides default if null.  
- `?.`: Null conditional — avoids NullReferenceException.

---

## 🟩 6. Control Statements

**Q1. What are conditional statements in C#?**  
`if`, `else if`, `else`, `switch`, and `?:` (ternary operator).

---

**Q2. Difference between `switch` and `if-else`?**  
- `if-else`: For range or complex conditions.  
- `switch`: For checking discrete values.

**Cross Question:**  
👉 Can switch use strings or enums?  
Yes, from C# 7 onwards.

---

## 🟩 7. Loops

**Q1. What loops are supported?**  
`for`, `foreach`, `while`, `do-while`, and `goto` (rarely used).

---

**Q2. Difference between `for` and `foreach`?**  
- `for`: Manual index, can modify elements.  
- `foreach`: Read-only iteration.

---

**Q3. How to exit from multiple nested loops?**  
Use **labels** or **return**.

**Example:**
```csharp
outer:
for (int i = 0; i < 3; i++)
{
    for (int j = 0; j < 3; j++)
    {
        if (j == 1) break outer;
    }
}
```

---

## 🟩 8. Arrays

**Q1. What is an array and how do you declare it?**
```csharp
int[] numbers = new int[3] { 1, 2, 3 };
```

---

**Q2. Difference between `Array` and `List<>`?**

| Feature | Array | List<> |
|----------|--------|--------|
| Size | Fixed | Dynamic |
| Namespace | System | System.Collections.Generic |
| Performance | Slightly faster | More flexible |

---

**Q3. Can arrays be resized?**  
No, but you can use `Array.Resize()` or convert to `List<>`.

---

## 🟩 9. Strings

**Q1. How are strings stored in memory?**  
Strings are **immutable reference types**, stored on the **heap**.

---

**Q2. What is string interning?**  
Interning stores identical strings in a shared memory pool to optimize memory.

---

**Q3. Difference between `StringBuilder` and `string`?**

| Feature | string | StringBuilder |
|----------|----------|---------------|
| Mutability | Immutable | Mutable |
| Best for | Small text | Large/frequently modified text |
| Namespace | System | System.Text |

**Cross Question:**  
👉 Is `StringBuilder` thread-safe?  
No, but `StringBuilder` can be made thread-safe using `lock`.

---

## 🟩 10. Type Casting

**Q1. Difference between implicit and explicit casting?**
- **Implicit:** Auto conversion (safe).  
- **Explicit:** Requires cast (can lose data).

**Example:**
```csharp
int i = 10;
double d = i;      // Implicit
int j = (int)d;    // Explicit
```

---

**Q2. What is boxing and unboxing?**
- **Boxing:** Value → Object  
- **Unboxing:** Object → Value

```csharp
int x = 10;
object obj = x;     // boxing
int y = (int)obj;   // unboxing
```

**Cross Question:**  
👉 Is boxing expensive?  
Yes, because it involves memory allocation on the heap.

---

**Q3. When does InvalidCastException occur?**
When casting an object to an incompatible type.

```csharp
object obj = "Hello";
int i = (int)obj; // ❌ InvalidCastException
```

---

### ✅ Next Topics (Upcoming Sections)
Would include:
- OOP Concepts (Encapsulation, Inheritance, Polymorphism, Abstraction)  
- Exception Handling  
- Collections & Generics  
- LINQ  
- Async/Await  
- File Handling  
- Delegates & Events

---
**End of Part 1 — C# Fundamentals**  
