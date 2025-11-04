
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

