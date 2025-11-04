
# 🧠 C# Q&A (With Concept Explanations, Cross Questions & Examples)

---

## 🟩 1. Value Types vs Reference Types

**Concept Explanation:**  
In C#, *value types* store the actual data (like `int`, `bool`, `struct`) directly on the **stack**, while *reference types* (like `class`, `string`, `object`) store a reference (address) to data on the **heap**. Stack is faster but temporary, heap is managed by Garbage Collector.

**Q: What’s the difference between stack and heap memory?**  
- **Stack:** Stores value types and method calls. Automatically cleared after method ends.  
- **Heap:** Stores reference types. Cleaned by Garbage Collector when not used.

**Example:**
```csharp
int a = 10;        // stored on stack
Person p = new();  // reference stored on stack, object on heap
```

**Cross Questions:**  
- **Q:** How are structs stored in memory?  
  **A:** Structs are value types, so they stay on stack (unless part of a class).  
- **Q:** What happens when you pass a struct by reference?  
  **A:** You modify the original struct instead of copying it.

**Key Takeaway:** Stack = fast, local. Heap = global, managed.

---

## 🟩 2. Boxing & Unboxing

**Concept Explanation:**  
Boxing and Unboxing help convert value types to objects and back. It’s useful when dealing with non-generic collections or APIs expecting `object`, but it adds performance overhead.

**Q: What is boxing and unboxing?**  
- **Boxing:** Converts value type → object.  
- **Unboxing:** Extracts object → value type.

**Example:**
```csharp
int x = 10;
object obj = x;       // Boxing
int y = (int)obj;     // Unboxing
```

**Cross Questions:**  
- **Q:** Why is boxing costly?  
  **A:** It requires new memory allocation on the heap.  
- **Q:** How to avoid boxing?  
  **A:** Use generics like `List<int>` instead of `ArrayList`.

**Key Takeaway:** Avoid boxing in performance-critical code.

---

## 🟩 3. ref, out, and in Parameters

**Concept Explanation:**  
These keywords help pass variables differently into methods:  
- `ref`: pass by reference (value can change).  
- `out`: for output only (must assign inside method).  
- `in`: pass by reference but read-only.

**Q: What’s the difference between `ref`, `out`, and `in`?**  

| Keyword | Purpose | Must Initialize? | Can Modify? |
|----------|----------|------------------|--------------|
| `ref`    | Pass existing value by reference | ✅ Yes | ✅ Yes |
| `out`    | Used for returning multiple values | ❌ No | ✅ Yes |
| `in`     | Pass reference as read-only | ✅ Yes | ❌ No |

**Example:**
```csharp
void Demo(ref int a, out int b, in int c) {
    a += 5;       // ok
    b = 20;       // required
    // c = 30;    // not allowed
}
```

**Cross Question:**  
- **Q:** Can async methods use ref parameters?  
  **A:** No, because async methods work as state machines, and ref variables can change unexpectedly.

**Key Takeaway:** Use `ref` for modify, `out` for return, `in` for read-only.

---

## 🟩 4. Nullable Types

**Concept Explanation:**  
By default, value types (like int, bool) cannot store `null`. Nullable types (`int?`, `bool?`) allow assigning `null` to value types safely.

**Q: How do nullable types work?**  
They wrap the value inside a `Nullable<T>` structure that can store either a value or `null`.

**Example:**
```csharp
int? age = null;
if (age.HasValue)
    Console.WriteLine(age.Value);
```

**Cross Questions:**  
- **Q:** Difference between `Nullable<T>` and `T?`?  
  **A:** `T?` is a short form of `Nullable<T>`.  
- **Q:** How to provide default for null?  
  **A:** `int result = age ?? 18;`

**Key Takeaway:** Use `?` and `??` to handle null safely.

---

## 🟩 5. Extension Methods

**Concept Explanation:**  
Extension methods let you add new methods to existing classes without changing their original code. They are defined as static methods but called as instance methods.

**Q: What are extension methods?**  
A static method that extends an existing type with new functionality.

**Example:**
```csharp
public static class StringExtensions {
    public static bool IsCapitalized(this string str)
        => !string.IsNullOrEmpty(str) && char.IsUpper(str[0]);
}
```

**Cross Questions:**  
- **Q:** Can we override them?  
  **A:** No, they cannot override existing methods.  
- **Q:** How does compiler resolve them?  
  **A:** Checks instance methods first, then extension ones.

**Key Takeaway:** Great for adding reusable helper methods.

---

## 🟩 6. Dynamic Keyword

**Concept Explanation:**  
`dynamic` allows skipping compile-time type checking. The type is decided at runtime. It’s flexible but can cause runtime errors if misused.

**Q: What is `dynamic` type?**  
A type whose operations are checked at runtime.

**Example:**
```csharp
dynamic d = "Hello";
d = 123;   // works fine, runtime handled
```

**Cross Questions:**  
- **Q:** Difference between `dynamic` and `object`?  
  **A:** `dynamic` doesn’t need casting; `object` does.  
- **Q:** When to avoid `dynamic`?  
  **A:** Avoid when performance or type safety is important.

**Key Takeaway:** Use for COM objects, reflection, or JSON APIs.

---

## 🟩 7. Async & Await

**Concept Explanation:**  
`async` and `await` make asynchronous code easier to read and write. Instead of blocking threads, async code waits for tasks to complete.

**Q: How does async/await work internally?**  
It creates a *state machine* that pauses execution at `await` and resumes when the awaited task completes.

**Example:**
```csharp
async Task<int> GetDataAsync() {
    await Task.Delay(1000);
    return 10;
}
```

**Cross Questions:**  
- **Q:** What if you don’t use `await`?  
  **A:** Code runs synchronously, task won’t complete automatically.  
- **Q:** Can we use multiple awaits?  
  **A:** Yes, sequentially or parallel with `Task.WhenAll()`.

**Key Takeaway:** Async improves responsiveness, not execution speed.

---

## 🟩 8. Tasks & Threads

**Concept Explanation:**  
A `Thread` is a physical thread managed by OS. A `Task` is a higher-level abstraction that represents an operation that can run asynchronously using thread pool threads.

**Q: What is the difference between `Thread`, `Task`, and `async`?**  

| Concept | Description |
|----------|-------------|
| Thread | OS thread running code manually |
| Task | Represents async operation handled by thread pool |
| async/await | Syntax to simplify async programming |

**Cross Questions:**  
- **Q:** What is the Thread Pool?  
  **A:** A collection of reusable threads managed by CLR.  
- **Q:** How does `Task.Run()` work?  
  **A:** It schedules work on a thread pool thread asynchronously.

**Key Takeaway:** Prefer `Task` and `async` for scalability.

---

# 🧠 C# Advanced Q&A (Part 2 — With Concepts, Examples & Cross Questions)

---

## 🟩 9. Dependency Injection (DI)

**Concept Explanation:**  
Dependency Injection is a design pattern used to make classes loosely coupled by providing their dependencies from outside rather than creating them inside. It improves testability and flexibility.

**Q: What is Dependency Injection (DI) and why is it used?**  
It allows objects to receive their dependencies from external sources (like configuration or container) instead of creating them directly.

**Example:**
```csharp
public interface IMessageService {
    void Send(string message);
}
public class EmailService : IMessageService {
    public void Send(string message) => Console.WriteLine($"Email: {message}");
}

public class Notification {
    private readonly IMessageService _service;
    public Notification(IMessageService service) => _service = service;
    public void Notify() => _service.Send("Hello DI!");
}
```
**Real-life Example:** In ASP.NET Core, DI is used to inject services (e.g., logging, configuration) automatically.

**Cross Questions:**  
- **Q:** What are DI lifetimes in .NET Core?  
  **A:** `Singleton`, `Scoped`, and `Transient`.  
- **Q:** Why is DI better than `new`?  
  **A:** It removes tight coupling and makes unit testing easier.

**Key Takeaway:** DI = flexible, testable, and maintainable code.

---

## 🟩 10. Garbage Collection (GC)

**Concept Explanation:**  
Garbage Collector automatically manages memory in .NET. It frees objects in heap that are no longer in use, preventing memory leaks.

**Q: How does Garbage Collection work?**  
GC tracks objects on heap and removes those with no active references.

**Example:**
```csharp
Person p = new Person();
p = null;       // object becomes eligible for GC
GC.Collect();   // forces GC manually (not recommended)
```

**Cross Questions:**  
- **Q:** What are GC generations?  
  **A:** 0 (short-lived), 1 (medium), 2 (long-lived) — GC checks young objects more often.  
- **Q:** When should you call `GC.Collect()`?  
  **A:** Only in rare cases, like after large memory releases.

**Key Takeaway:** GC optimizes memory automatically — avoid manual calls.

---

## 🟩 11. Memory Management

**Concept Explanation:**  
Memory management in .NET includes allocation, garbage collection, and cleanup using `IDisposable` and `using`.

**Q: What are weak references?**  
A weak reference lets you reference an object without preventing GC from collecting it.

**Example:**
```csharp
WeakReference objRef = new WeakReference(new Person());
if (objRef.IsAlive)
    Console.WriteLine("Object still exists");
```

**Cross Questions:**  
- **Q:** How do `IDisposable` and `using` work?  
  **A:** They release unmanaged resources like file handles or database connections.  
- **Q:** What is a memory leak?  
  **A:** When objects are unintentionally kept alive, preventing GC from reclaiming memory.

**Key Takeaway:** Always dispose unmanaged resources properly.

---

## 🟩 12. Records & Structs (C# 9+)

**Concept Explanation:**  
Records are immutable reference types introduced in C# 9 for data modeling. Structs are value types used for small, lightweight data.

**Q: What are record types?**  
They are special classes optimized for storing data with built-in equality and immutability.

**Example:**
```csharp
public record Person(string Name, int Age);
var p1 = new Person("Ankita", 32);
```

**Cross Questions:**  
- **Q:** How do records differ from classes?  
  **A:** Records use value-based equality, while classes use reference equality.  
- **Q:** Are records reference or value types?  
  **A:** Reference types (unless defined as `record struct`).

**Key Takeaway:** Records simplify immutable data handling.

---

## 🟩 13. Pattern Matching (C# 9+)

**Concept Explanation:**  
Pattern matching allows checking types and conditions in cleaner, expressive ways using `is`, `switch`, and `when` patterns.

**Q: What is pattern matching in C#?**  
A feature that simplifies conditional logic based on type or property values.

**Example:**
```csharp
object obj = 5;
if (obj is int number && number > 0)
    Console.WriteLine("Positive integer");
```

**Cross Questions:**  
- **Q:** Example with switch expression?  
  **A:**  
  ```csharp
  string result = obj switch {
      int n when n > 0 => "Positive",
      int n when n < 0 => "Negative",
      _ => "Zero or not int"
  };
  ```

**Key Takeaway:** Pattern matching = cleaner conditional logic.

---

## 🟩 14. Tuples

**Concept Explanation:**  
Tuples group multiple values into a single structure without creating a class.

**Q: What is a tuple?**  
A data structure that holds multiple values of possibly different types.

**Example:**
```csharp
(string name, int age) person = ("Ankita", 32);
Console.WriteLine(person.name);
```

**Cross Questions:**  
- **Q:** Difference between `Tuple<T>` and ValueTuple `(T1, T2)`?  
  **A:** `ValueTuple` is faster and allows naming elements.  
- **Q:** Can we return tuples from methods?  
  **A:** Yes, very useful for multiple return values.

**Key Takeaway:** Tuples simplify returning multiple results.

---

## 🟩 15. Reflection

**Concept Explanation:**  
Reflection lets you inspect and interact with metadata (like classes, methods, and properties) at runtime.

**Q: What is reflection in C#?**  
A mechanism to examine or modify program structure at runtime.

**Example:**
```csharp
Type t = typeof(string);
foreach (var m in t.GetMethods())
    Console.WriteLine(m.Name);
```

**Cross Questions:**  
- **Q:** Can reflection access private members?  
  **A:** Yes, using BindingFlags, but it should be avoided for security reasons.  
- **Q:** Performance impact?  
  **A:** Reflection is slower, use sparingly.

**Key Takeaway:** Reflection = powerful but use carefully.

---

## 🟩 16. Attributes

**Concept Explanation:**  
Attributes add metadata to code elements (like methods, classes) to give the compiler or runtime extra information.

**Q: What are attributes in C#?**  
Decorators that provide additional information or behavior hints.

**Example:**
```csharp
[Obsolete("Use NewMethod instead")]
void OldMethod() { }
```

**Cross Questions:**  
- **Q:** How to create a custom attribute?  
  **A:**  
  ```csharp
  [AttributeUsage(AttributeTargets.Class)]
  public class MyAttribute : Attribute { }
  ```

**Key Takeaway:** Attributes = metadata for classes/methods.

---

## 🟩 17. Generics (Advanced)

**Concept Explanation:**  
Generics make code reusable by allowing methods and classes to operate with any data type safely.

**Q: What are generic constraints?**  
They restrict the types that can be used as generic arguments.

**Example:**
```csharp
public class Repo<T> where T : class {
    public void Add(T item) => Console.WriteLine(item);
}
```

**Cross Questions:**  
- **Q:** What is covariance and contravariance?  
  **A:** Covariance allows a derived-to-base conversion; contravariance allows base-to-derived in generics.  
- **Q:** Benefit of generics?  
  **A:** Type safety and no boxing.

**Key Takeaway:** Generics = reusable and type-safe code.

---

## 🟩 18. Unsafe Code

**Concept Explanation:**  
Unsafe code allows pointer operations for performance-critical tasks, but should be avoided unless absolutely necessary.

**Q: What is unsafe code in C#?**  
Code that uses pointers and bypasses CLR safety checks.

**Example:**
```csharp
unsafe {
    int a = 10;
    int* p = &a;
    Console.WriteLine(*p);
}
```

**Cross Questions:**  
- **Q:** When should it be used?  
  **A:** Only for low-level memory access, like interop or performance optimization.  
- **Q:** Is unsafe code recommended in production?  
  **A:** No, it can cause memory corruption.

**Key Takeaway:** Unsafe = powerful but risky. Use rarely.

---

