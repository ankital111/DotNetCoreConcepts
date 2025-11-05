# 💻 C# Basics Visual Q&A (Part 1)

A clear and practical guide covering **C# fundamentals** — each topic is explained simply with examples, cross-questions, and key takeaways.

---

## 1️⃣ C# Overview

💡 **Concept:**  
C# (pronounced “C-sharp”) is an object-oriented, modern programming language developed by Microsoft. It’s part of the .NET platform and is used to build **web, desktop, mobile, cloud, and game applications**.

### 🧠 Main Question: What is C# and why is it used?
✅ **Answer:**  
C# is a type-safe, object-oriented language used for developing applications that run on the .NET Framework and .NET Core. It’s popular because it’s easy to learn, supports modern features, and provides strong memory management through garbage collection.

### 🔁 Cross Questions:
**Q1:** How is C# different from Java?  
👉 C# integrates tightly with the .NET ecosystem, supports properties, delegates, and LINQ, while Java runs on JVM and lacks some .NET features.  

**Q2:** What platforms can C# run on?  
👉 .NET Core and .NET 5+ make C# cross-platform — it runs on Windows, Linux, and macOS.

### ⚙️ Example:
```csharp
Console.WriteLine("Hello, C#!");
```
### 🔑 Key Takeaway:
C# is Microsoft’s flagship language for modern, secure, cross-platform development.

---

## 2️⃣ Structure of a C# Program

💡 **Concept:**  
A C# program is structured into **namespaces**, **classes**, and **methods**. The entry point is the `Main()` method.

### 🧠 Main Question: What are namespaces, classes, and methods?
✅ **Answer:**  
- **Namespace:** Groups related classes together.  
- **Class:** Blueprint that defines properties and methods.  
- **Method:** A block of code that performs a specific task.

### 🔁 Cross Questions:
**Q1:** Why do we use `Main()` method?  
👉 It’s the entry point where execution starts.

**Q2:** Can a C# program have multiple Main methods?  
👉 Yes, but only one will act as the entry point — defined during compilation.

### ⚙️ Example:
```csharp
namespace DemoApp {
    class Program {
        static void Main() {
            Console.WriteLine("Program Start");
        }
    }
}
```
### 🔑 Key Takeaway:
The `Main()` method defines where your application begins execution.

---

## 3️⃣ Data Types

💡 **Concept:**  
C# has **Value Types** (stored in stack) and **Reference Types** (stored in heap).

### 🧠 Main Question: What are value and reference types?
✅ **Answer:**  
- **Value types:** Hold actual data (e.g., int, float, struct).  
- **Reference types:** Hold memory addresses (e.g., class, array, string).

### 🔁 Cross Questions:
**Q1:** What happens when you assign one struct to another?  
👉 A new copy is created — changes in one do not affect the other.

**Q2:** Difference between `int` and `Int32`?  
👉 Both are same; `int` is an alias of `System.Int32`.

### ⚙️ Example:
```csharp
int a = 10;
int b = a; // value copied
b++;
Console.WriteLine(a); // 10
```
### 🔑 Key Takeaway:
Value types store data directly; reference types store references.

---

## 4️⃣ Variables & Constants

💡 **Concept:**  
Variables store data that can change; constants hold fixed values.

### 🧠 Main Question: Difference between `var`, `dynamic`, and `object`?
✅ **Answer:**  
- **var:** Type inferred at compile time.  
- **dynamic:** Type resolved at runtime.  
- **object:** Base type of all types; requires casting.

### 🔁 Cross Questions:
**Q1:** When should you use `var` vs explicit typing?  
👉 Use `var` for readability when type is obvious; explicit when clarity matters.

**Q2:** Can constants be assigned at runtime?  
👉 No, constants are compile-time fixed.

### ⚙️ Example:
```csharp
var name = "Ankita";
dynamic age = 30;
const double PI = 3.14;
```
### 🔑 Key Takeaway:
Use `var` for inferred types, `dynamic` for flexibility, `const` for fixed values.

---

## 5️⃣ Operators

💡 **Concept:**  
Operators perform operations on operands — arithmetic, comparison, logical, etc.

### 🧠 Main Question: What types of operators are available?
✅ **Answer:**  
Arithmetic, Relational, Logical, Bitwise, Assignment, Conditional (`?:`), and Null-coalescing (`??`).

### 🔁 Cross Questions:
**Q1:** Difference between `==` and `Equals()`?  
👉 `==` compares values or references depending on type, `Equals()` checks content equality.

**Q2:** What do `??` and `?.` do?  
👉 `??` gives a default value if null; `?.` safely accesses members.

### ⚙️ Example:
```csharp
string name = null;
Console.WriteLine(name ?? "Guest");
```
### 🔑 Key Takeaway:
Use `??` and `?.` for safer null handling and avoid exceptions.

---

## 6️⃣ Control Statements

💡 **Concept:**  
Used for decision making — like `if`, `else`, and `switch`.

### 🧠 Main Question: What are conditional statements?
✅ **Answer:**  
They control flow based on conditions using `if`, `else if`, and `switch`.

### 🔁 Cross Questions:
**Q1:** Difference between `switch` and `if-else`?  
👉 `switch` is better for discrete values; `if` for complex logical conditions.

**Q2:** Can we use `switch` with strings?  
👉 Yes, from C# 7.0 onwards.

### ⚙️ Example:
```csharp
string role = "Admin";
switch (role) {
    case "Admin": Console.WriteLine("Access Granted"); break;
    default: Console.WriteLine("Access Denied"); break;
}
```
### 🔑 Key Takeaway:
Use `switch` for cleaner multi-condition checks.

---

## 7️⃣ Loops

💡 **Concept:**  
Loops repeat code — `for`, `foreach`, `while`, `do-while`.

### 🧠 Main Question: What loops are supported?
✅ **Answer:**  
- **for** — fixed count iterations  
- **foreach** — collection iteration  
- **while/do-while** — conditional repetition

### 🔁 Cross Questions:
**Q1:** Difference between `for` and `foreach`?  
👉 `for` gives index control; `foreach` is simpler for collections.

**Q2:** How to exit multiple nested loops?  
👉 Use a flag or `goto` (not recommended).

### ⚙️ Example:
```csharp
foreach (var item in new int[] {1, 2, 3}) {
    Console.WriteLine(item);
}
```
### 🔑 Key Takeaway:
Choose loop type based on iteration logic and readability.

---

## 8️⃣ Arrays

💡 **Concept:**  
Arrays store multiple values of same type in contiguous memory.

### 🧠 Main Question: What is an array and how to declare it?
✅ **Answer:**  
An array is a fixed-size collection declared as `int[] nums = new int[3];`

### 🔁 Cross Questions:
**Q1:** Difference between `Array` and `List<>`?  
👉 Array is fixed-size; List is dynamic.

**Q2:** Can arrays be resized?  
👉 Not directly — must create a new array or use `List<>`.

### ⚙️ Example:
```csharp
int[] nums = { 1, 2, 3 };
Console.WriteLine(nums[1]); // Output: 2
```
### 🔑 Key Takeaway:
Arrays are efficient but have fixed size — prefer `List<>` for flexibility.

---

## 9️⃣ Strings

💡 **Concept:**  
Strings are immutable sequences of characters stored in the heap.

### 🧠 Main Question: How are strings stored in memory?
✅ **Answer:**  
Strings are reference types; once created, they cannot be changed — new objects are formed on modification.

### 🔁 Cross Questions:
**Q1:** What is string interning?  
👉 It stores identical strings in a shared pool to save memory.

**Q2:** Difference between `StringBuilder` and `string`?  
👉 `StringBuilder` is mutable; efficient for frequent changes.

### ⚙️ Example:
```csharp
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World");
Console.WriteLine(sb);
```
### 🔑 Key Takeaway:
Use `StringBuilder` for performance when modifying strings often.

---

## 🔟 Type Casting

💡 **Concept:**  
Type casting converts one data type to another.

### 🧠 Main Question: Difference between implicit and explicit casting?
✅ **Answer:**  
- **Implicit:** Safe conversion (int → double).  
- **Explicit:** Manual conversion (double → int).

### 🔁 Cross Questions:
**Q1:** What is boxing/unboxing?  
👉 Boxing: value → object. Unboxing: object → value.

**Q2:** When does `InvalidCastException` occur?  
👉 When incompatible types are cast manually.

### ⚙️ Example:
```csharp
int x = 10;
object obj = x; // boxing
int y = (int)obj; // unboxing
```
### 🔑 Key Takeaway:
Casting helps interoperability; use `as` or `is` for safe conversions.



2️⃣ Structure of a C# Program

💡 Concept:
A C# program is structured into namespaces, classes, and methods. The entry point is the Main() method.

🧠 Main Question: What are namespaces, classes, and methods?

✅ Answer:

Namespace: Groups related classes together.

Class: Blueprint that defines properties and methods.

Method: A block of code that performs a specific task.

🔁 Cross Questions

Q1: Why do we use Main() method?
👉 It’s the entry point where execution starts.

Q2: Can a C# program have multiple Main() methods?
👉 Yes, but only one will act as the entry point — defined during compilation.

⚙️ Example
