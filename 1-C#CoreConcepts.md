# 💻 C# Basics Visual Q&A (Part 1 – Extended Edition)

A clear and practical guide covering **C# fundamentals** — each topic is explained simply with examples, cross-questions, and key takeaways.

---

## 1️⃣ C# Overview

💡 **Concept:**  
C# (pronounced “C-sharp”) is an object-oriented, modern programming language developed by Microsoft. It’s part of the .NET platform and is used to build **web, desktop, mobile, cloud, and game applications**.

### 🧠 Main Question: What is C# and why is it used?
✅ **Answer:**  
C# is a type-safe, object-oriented language used for developing applications that run on the .NET Framework and .NET Core.  
It’s popular because it’s easy to learn, supports modern features, and provides strong memory management through garbage collection.

### 🔁 Cross Questions
**Q1:** How is C# different from Java?  
👉 C# integrates tightly with the .NET ecosystem, supports properties, delegates, and LINQ, while Java runs on JVM and lacks some .NET features.  

**Q2:** What platforms can C# run on?  
👉 .NET Core and .NET 5+ make C# cross-platform — it runs on Windows, Linux, and macOS.

### ⚙️ Example
```csharp
Console.WriteLine("Hello, C#!");

```

🔑 Key Takeaway

C# is Microsoft’s flagship language for modern, secure, cross-platform development.



## 2️⃣ Structure of a C# Program

### 🧩 Concept
Every C# program has a structure that includes **namespaces, classes, and methods**.  
It defines how your code is organized and executed.

### 💬 Main Question
**Q:** What are namespaces, classes, and methods?

**A:**  
- **Namespace**: Logical container to organize code and avoid name conflicts.  
- **Class**: Blueprint for objects that holds data (fields) and logic (methods).  
- **Method**: A block of code that performs a specific task.

### 🔍 Cross Questions
- Why do we use `Main()` method?  
  ➤ It’s the entry point where program execution starts.  
- Can a C# program have multiple `Main()` methods?  
  ➤ Yes, but only one can be the entry point — defined in project settings.

### 🧠 Example
```csharp
using System;

namespace DemoApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, Ankita!");
        }
    }
}


