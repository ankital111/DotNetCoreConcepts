
# 🧠 Chapter 3: Exception Handling in C#

---

## 🌟 1. What is Exception Handling?

### ✅ Simple Explanation:
An **exception** is an **unexpected error** that occurs during program execution.  
**Exception Handling** is a mechanism to handle runtime errors gracefully without crashing the program.

### 🧩 Example:

```csharp
try
{
    int num = 10;
    int result = num / 0; // ❌ Division by zero error
}
catch (Exception ex)
{
    Console.WriteLine("Something went wrong: " + ex.Message);
}
finally
{
    Console.WriteLine("Finally block executed!");
}
```

### 🧠 Output:
```
Something went wrong: Attempted to divide by zero.
Finally block executed!
```

---

## 🧩 2. Why Do We Need Exception Handling?

### ✅ Purpose:
- Prevent application crash
- Show user-friendly error messages
- Log and debug issues easily
- Ensure resources (files, DB connections) are released

---

## ⚙️ 3. Exception Handling Keywords

| Keyword | Description |
|----------|--------------|
| `try` | Block of code where an exception might occur |
| `catch` | Handles the exception |
| `finally` | Always executes (used to clean up resources) |
| `throw` | Used to manually throw an exception |
| `throws` | ❌ Not used in C#, used in Java |
| `System.Exception` | Base class for all exceptions |

---

## 🧠 4. Example with Multiple Catch Blocks

```csharp
try
{
    int[] arr = new int[3];
    arr[5] = 100; // ❌ Index out of range
}
catch (IndexOutOfRangeException ex)
{
    Console.WriteLine("Array index error: " + ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine("General error: " + ex.Message);
}
finally
{
    Console.WriteLine("Code execution completed.");
}
```

---

## 🎯 5. Nested try-catch Example

```csharp
try
{
    try
    {
        int num = int.Parse("abc"); // ❌ Format exception
    }
    catch (FormatException ex)
    {
        Console.WriteLine("Inner Catch: " + ex.Message);
    }
}
catch (Exception ex)
{
    Console.WriteLine("Outer Catch: " + ex.Message);
}
```

🧩 **Output:**
```
Inner Catch: Input string was not in a correct format.
```

---

## 🚨 6. throw vs throw ex

| Keyword | Description | Stack Trace Preserved? |
|----------|--------------|-----------------------|
| `throw;` | Re-throws the original exception | ✅ Yes |
| `throw ex;` | Throws a new exception object | ❌ No |

### Example:

```csharp
catch (Exception ex)
{
    Console.WriteLine("Error logged");
    throw; // ✅ Best practice
}
```

---

## 🧰 7. Custom Exception Class

You can create your **own exception** class by inheriting from `Exception`.

```csharp
public class AgeException : Exception
{
    public AgeException(string message) : base(message)
    {
    }
}

class Program
{
    static void ValidateAge(int age)
    {
        if (age < 18)
            throw new AgeException("Age must be 18 or older.");
    }

    static void Main()
    {
        try
        {
            ValidateAge(15);
        }
        catch (AgeException ex)
        {
            Console.WriteLine("Custom Exception: " + ex.Message);
        }
    }
}
```

---

## 💾 8. Common Exception Types in C#

| Exception | Description |
|------------|--------------|
| `NullReferenceException` | Accessing object that is null |
| `IndexOutOfRangeException` | Accessing array index that doesn’t exist |
| `DivideByZeroException` | Division by zero |
| `InvalidCastException` | Invalid type conversion |
| `FormatException` | Wrong format conversion (string → int) |
| `IOException` | File handling issues |
| `SqlException` | SQL-related error |
| `OutOfMemoryException` | Not enough memory |

---

## 🔁 9. Exception Handling with `using` (Dispose pattern)

For objects like **FileStream**, **SqlConnection**, etc., which must be closed,  
use `using` block — it automatically calls `Dispose()`.

```csharp
using (StreamReader reader = new StreamReader("data.txt"))
{
    Console.WriteLine(reader.ReadToEnd());
}
```

If exception occurs inside `using`, the object will still be disposed.

---

## ⚡ 10. Best Practices

✅ Use **specific exceptions** before general ones.  
✅ Always log exceptions.  
✅ Never hide exceptions silently.  
✅ Use `finally` or `using` to clean up resources.  
✅ Avoid catching `System.Exception` unless necessary.  
✅ Avoid throwing exceptions in performance-critical code.

---

# 💬 INTERVIEW QUESTIONS & ANSWERS

---

### 🧩 Q1. What is an exception?
**A:** An exception is an unexpected runtime error that interrupts the program’s normal flow.

**Cross Question:**  
👉 What is the difference between error and exception?  
**A:**  
- **Error:** System-level issue (like OutOfMemory).  
- **Exception:** Application-level issue that can be handled.

---

### 🧩 Q2. How does exception handling work in C#?
**A:** It works using `try`, `catch`, and `finally` blocks. Code that may throw an exception is in `try`, handled in `catch`, and cleanup code in `finally`.

**Cross Question:**  
👉 Can a `finally` block execute if there’s a `return` in the `try` block?  
**A:** Yes, `finally` always executes.

---

### 🧩 Q3. What happens if there’s no matching catch block?
**A:** The program terminates, and the CLR shows an unhandled exception message.

**Cross Question:**  
👉 What if there’s a `finally` block?  
**A:** It still executes before termination.

---

### 🧩 Q4. What is the difference between `throw` and `throw ex`?
**A:**  
- `throw;` rethrows the original exception (preserves stack trace).  
- `throw ex;` creates a new exception (stack trace lost).

---

### 🧩 Q5. Can we have multiple `catch` blocks?
**A:** Yes, but always put **specific exceptions** before general `Exception`.

---

### 🧩 Q6. Can we have a try block without a catch block?
**A:** Yes, but it must have a `finally` block.

**Example:**
```csharp
try
{
    // code
}
finally
{
    // cleanup
}
```

---

### 🧩 Q7. What is a custom exception?
**A:** It’s a user-defined exception created by inheriting from `System.Exception` for business-specific scenarios.

---

### 🧩 Q8. What is the role of `finally`?
**A:** `finally` is used for cleanup — releasing files, closing connections, etc. It always executes.

---

### 🧩 Q9. How do you log exceptions?
**A:**  
By using:
- `Console.WriteLine(ex.Message)`  
- `ex.StackTrace`  
- Logging frameworks like **Serilog**, **NLog**, **Log4Net**.

---

### 🧩 Q10. What is Exception Propagation?
**A:** If an exception is not handled in the current method, it is passed to the calling method.

---

### 🧩 Q11. Can you catch multiple exceptions in one catch block?
**A:** Yes (C# 6 and above):

```csharp
catch (Exception ex) when (ex is IOException || ex is FormatException)
{
    Console.WriteLine("Handled multiple exceptions.");
}
```

---

### 🧩 Q12. What are unhandled exceptions?
**A:** Exceptions that occur without a catch block.  
Handled using:
```csharp
AppDomain.CurrentDomain.UnhandledException += ...
```

---

# 🧾 Summary (Cheat Sheet)

| Concept | Example | Purpose |
|----------|----------|----------|
| `try-catch` | Handles exceptions | Prevent crashes |
| `finally` | Executes always | Cleanup |
| `throw` | Rethrow exception | Preserve stack |
| `custom exception` | Inherit `Exception` | Business rule validation |
| `using` | Dispose objects | Resource cleanup |
