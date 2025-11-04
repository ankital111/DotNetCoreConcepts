# C# Advanced Questions and Answers

| **Topic** | **Main Question & Answer** | **Cross Questions & Answers** |
|------------|-----------------------------|--------------------------------|

### **1. Value Types vs Reference Types**
**Q:** What’s the difference between stack and heap memory?  
**A:** Stack stores value types and manages memory automatically in LIFO order. Heap stores reference types and is managed by the garbage collector.  

**Q:** How are structs stored in memory?  
**A:** Structs are value types, so they are stored on the stack by default, unless they are part of a class object.  

**Q:** What happens when you pass a struct by reference?  
**A:** Using `ref` or `out` passes a struct by reference, allowing modifications to affect the original instance.  

---

### **2. Boxing & Unboxing**
**Q:** What is boxing and unboxing?  
**A:** Boxing converts a value type to an `object` (heap allocation). Unboxing extracts the value type from the object.  

**Q:** Why is boxing costly?  
**A:** Boxing involves allocating memory on the heap and copying the value, which is slower.  

**Q:** How to avoid unnecessary boxing?  
**A:** Use generics instead of `object` to store value types efficiently.  

---

### **3. ref, out, in Parameters**
**Q:** What is the difference between `ref`, `out`, and `in`?  
**A:**  
- `ref`: Must be initialized before passing, allows reading/writing.  
- `out`: Must be assigned inside the method, used for output.  
- `in`: Passed by reference but read-only.  

**Q:** Can async methods use ref parameters?  
**A:** No, async methods cannot have `ref` or `out` parameters due to compiler-generated state machines.  

---

### **4. Nullable Types**
**Q:** How do nullable types work?  
**A:** Nullable types (`int?`) allow value types to represent null, wrapping them in `Nullable<T>`.  

**Q:** Difference between `Nullable<T>` and `T?` syntax?  
**A:** They are equivalent. `T?` is shorthand for `Nullable<T>`.  

**Q:** How to check for null?  
**A:** Use `HasValue` or null-coalescing operator `??`.  

---

### **5. Extension Methods**
**Q:** What are extension methods?  
**A:** Static methods that add functionality to existing types without modifying them.  

**Q:** Can we override them?  
**A:** No, they are static and resolved at compile-time, not runtime.  

**Q:** How does compiler resolve them?  
**A:** It searches for static classes with `this` keyword parameter in the same or imported namespace.  

---

### **6. Dynamic Keyword**
**Q:** What is `dynamic` type?  
**A:** `dynamic` bypasses compile-time type checking; binding occurs at runtime.  

**Q:** Difference between `dynamic` and `object`?  
**A:** Both can hold any type, but `dynamic` skips compile-time checks. `object` requires explicit casting.  

**Q:** When to avoid dynamic?  
**A:** Avoid when type safety and performance are priorities.  

---

### **7. Async & Await**
**Q:** How does async/await work internally?  
**A:** Compiler transforms async methods into state machines that execute asynchronously using `Task` objects.  

**Q:** What happens if you don’t use `await`?  
**A:** The task runs but exceptions may be unhandled; method continues without waiting.  

**Q:** Can we have multiple awaits?  
**A:** Yes, multiple awaits run sequentially unless tasks are started before awaiting (for concurrency).  

---

### **8. Tasks & Threads**
**Q:** Difference between `Thread`, `Task`, and `async`?  
**A:**  
- `Thread`: Low-level OS thread.  
- `Task`: Higher abstraction representing asynchronous work.  
- `async`: Keyword simplifying asynchronous programming with tasks.  

**Q:** What is the thread pool?  
**A:** A pool of pre-created threads reused for tasks to improve performance.  

**Q:** How does `Task.Run()` work?  
**A:** It queues work to the thread pool for execution.  

---

### **9. Dependency Injection**
**Q:** What is DI and why is it used?  
**A:** DI provides dependencies externally rather than creating them inside classes, improving modularity and testability.  

**Q:** What are lifetimes in .NET Core DI?  
**A:**  
- `Singleton`: One instance for entire app.  
- `Scoped`: One per request.  
- `Transient`: New instance each time.  

**Q:** What’s the difference between DI and IoC?  
**A:** IoC is a principle; DI is one way to implement it.  

---

### **10. Garbage Collection (GC)**
**Q:** How does GC work?  
**A:** GC reclaims memory of unused objects on the heap automatically.  

**Q:** What are generations in GC?  
**A:**  
- Gen 0: Short-lived objects.  
- Gen 1: Medium-lived.  
- Gen 2: Long-lived.  

**Q:** When to use `GC.Collect()`?  
**A:** Rarely; only when you must free large unused memory explicitly.  

---

### **11. Memory Management**
**Q:** What are weak references?  
**A:** References that don’t prevent GC from collecting the object.  

**Q:** How do `IDisposable` and `using` work?  
**A:** `IDisposable.Dispose()` releases unmanaged resources. `using` ensures Dispose is called automatically.  

---

### **12. Records & Structs (C# 9+)**
**Q:** What are record types?  
**A:** Immutable reference types designed for data models with built-in equality.  

**Q:** How do records differ from classes?  
**A:** Records use value-based equality; classes use reference equality.  

**Q:** Are records reference or value types?  
**A:** Records are reference types by default, but can be defined as `record struct`.  

---

### **13. Pattern Matching (C# 9+)**
**Q:** What is pattern matching?  
**A:** Pattern matching allows concise checks and destructuring of objects based on types and values.  

**Q:** Example using switch expressions:  
```csharp
string GetType(object obj) => obj switch
{
    int i => "Integer",
    string s => "String",
    null => "Null",
    _ => "Unknown"
};
```

**Q:** What are type, relational, and property patterns?  
**A:** Patterns that match by type, range, or property values.  

---

### **14. Tuples**
**Q:** What is a tuple?  
**A:** A lightweight data structure to group multiple values.  

**Q:** Difference between `Tuple<T>` and value tuple `(T1, T2)`?  
**A:** Value tuples are faster, support named fields, and are mutable.  

**Q:** Can tuples be returned from methods?  
**A:** Yes, ideal for returning multiple values without creating a class.  

---

### **15. Reflection**
**Q:** What is reflection?  
**A:** Allows runtime inspection and modification of types, properties, and methods.  

**Q:** Can reflection modify private members?  
**A:** Yes, using `BindingFlags.NonPublic`, though it’s discouraged.  

**Q:** Performance impact?  
**A:** Reflection is slower; avoid in performance-critical code.  

---

### **16. Attributes**
**Q:** What are attributes in C#?  
**A:** Metadata attached to code elements used for reflection or custom logic.  

**Q:** How to create a custom attribute?  
**A:** Derive from `System.Attribute`. Example:  
```csharp
[AttributeUsage(AttributeTargets.Class)]
public class InfoAttribute : Attribute
{
    public string Description { get; }
    public InfoAttribute(string desc) => Description = desc;
}
```

---

### **17. Generics (Advanced)**
**Q:** What are generic constraints?  
**A:** Rules applied to type parameters using `where` keyword (e.g., `where T : class`).  

**Q:** What’s covariance and contravariance?  
**A:**  
- **Covariance (`out`)**: Allows derived-to-base assignment.  
- **Contravariance (`in`)**: Allows base-to-derived assignment.  

**Q:** Example:  
```csharp
IEnumerable<string> strs = new List<string>();
IEnumerable<object> objs = strs; // Covariant
```

---

### **18. Unsafe Code**
**Q:** What is unsafe code?  
**A:** Code that uses pointers via `unsafe` keyword. Requires `/unsafe` compiler flag.  

**Q:** When should it be used?  
**A:** Only for performance-critical or interop scenarios.  

**Q:** Is it recommended in production?  
**A:** No, as it bypasses CLR safety checks.
