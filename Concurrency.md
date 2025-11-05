
# C# Concurrency Cheat Sheet (Key Points + Examples + Short Q&A)

## 1. Thread
- A **thread** is the smallest unit of execution.
- Every C# program starts with one **Main thread**.

### Example:
```csharp
Console.WriteLine("This is the main thread");
```

### Create New Thread:
```csharp
using System.Threading;

Thread t = new Thread(() =>
{
    Console.WriteLine("Running in another thread");
});
t.Start();
```

### Short Q&A:
**Q:** Why use threads?  
**A:** To run multiple tasks at the same time and keep UI responsive.

---

## 2. Multithreading
- Running **multiple threads** simultaneously.
- Improves performance and responsiveness.

### Example:
```csharp
Thread t1 = new Thread(() => Console.WriteLine("Thread 1"));
Thread t2 = new Thread(() => Console.WriteLine("Thread 2"));
t1.Start();
t2.Start();
```

### Short Q&A:
**Q:** Do more threads always increase performance?  
**A:** No, too many threads cause CPU overhead.

---

## 3. Task (Task Parallel Library)
- **Task** is a high-level abstraction over threads.
- Easier to manage than `Thread`.

### Example:
```csharp
using System.Threading.Tasks;

Task.Run(() => Console.WriteLine("Task running asynchronously"));
```

### Short Q&A:
**Q:** Task vs Thread?  
**A:** Task is managed by .NET and is lightweight; Thread is lower level and heavier.

---

## 4. async / await
- Used for **asynchronous (non-blocking) programming**.
- Best for **I/O work** (API calls, DB queries).

### Example:
```csharp
public async Task FetchDataAsync()
{
    Console.WriteLine("Fetching...");
    await Task.Delay(2000);
    Console.WriteLine("Done");
}
```

### Short Q&A:
**Q:** Does `await` create a new thread?  
**A:** No, it releases the thread while waiting.

---

## 5. Parallel Programming
- Best for **CPU-bound tasks** (heavy calculations).
- Uses all CPU cores.

### Example:
```csharp
Parallel.For(1, 5, i =>
{
    Console.WriteLine($"Processing {i}");
});
```

### Short Q&A:
**Q:** When to use Parallel?  
**A:** When performing CPU-intensive loops/calculations.

---

## 6. CancellationToken (Graceful Stop)
```csharp
public async Task ProcessAsync(CancellationToken token)
{
    for(int i = 0; i < 5; i++)
    {
        token.ThrowIfCancellationRequested();
        await Task.Delay(500);
        Console.WriteLine($"Step {i}");
    }
}
```

---

## Quick Decision Guide
| Scenario | Use |
|---|---|
| UI should remain responsive | async/await |
| Doing heavy calculations | Parallel |
| Running background work | Task |
| Manually controlling execution | Thread |

---

## Final Summary
| Concept | Think Like |
|---|---|
| Thread | A worker |
| Multithreading | Multiple workers |
| Task | A managed job for a worker |
| async/await | Worker waits smartly without blocking |
| Parallel | All workers doing work at same time |

