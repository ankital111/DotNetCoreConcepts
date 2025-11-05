# 🧠 Unit 2 — OOP + Advanced C#

## 🎯 Goal:
Understand and confidently explain **object-oriented programming** and **advanced design practices** with **real-world C# examples** and **interview reasoning**.

---

## 🔹 1. Encapsulation

### 📘 Concept:
Encapsulation means **binding data (fields)** and **methods** that operate on that data into a **single unit (class)** and restricting direct access via **access modifiers**.

### 🧩 Example:
```csharp
public class BankAccount
{
    private decimal balance; // encapsulated field

    public void Deposit(decimal amount)
    {
        if (amount > 0)
            balance += amount;
    }

    public decimal GetBalance() => balance; // controlled access
}
```

### 💬 Interview Q&A:
**Q:** What is encapsulation?  
**A:** Wrapping data and methods into one unit and controlling access using access modifiers.

**Cross Q:**  
- Why use private fields instead of public? → To prevent unauthorized modification of internal state.  
- How is encapsulation different from abstraction? → Encapsulation hides data, abstraction hides complexity.

---

## 🔹 2. Inheritance

### 📘 Concept:
Inheritance allows a class (**derived**) to acquire the properties and behavior of another (**base**) class, enabling **code reuse**.

### 🧩 Example:
```csharp
public class Vehicle
{
    public void Start() => Console.WriteLine("Vehicle started");
}

public class Car : Vehicle
{
    public void Drive() => Console.WriteLine("Car is driving");
}
```

### 💬 Interview Q&A:
**Q:** What is inheritance in C#?  
**A:** It’s the mechanism by which one class derives from another.

**Cross Q:**  
- Can C# support multiple inheritance? → No, only via interfaces.  
- What’s the access level of protected members? → Accessible within the class and its derived classes.

---

## 🔹 3. Polymorphism

### 📘 Concept:
Polymorphism means **“many forms”** — allows the same interface or method to behave differently based on the object’s type.

### 🧩 Example:
```csharp
public class Animal
{
    public virtual void Speak() => Console.WriteLine("Animal speaks");
}

public class Dog : Animal
{
    public override void Speak() => Console.WriteLine("Dog barks");
}
```

### 💬 Interview Q&A:
**Q:** What is polymorphism?  
**A:** It allows the same method to have different implementations in derived classes.

**Cross Q:**  
- Difference between compile-time and runtime polymorphism?  
  → Compile-time: Method Overloading  
  → Runtime: Method Overriding  
- What if you don’t use `virtual` or `override`?  
  → The method will be hidden, not overridden.

---

## 🔹 4. Abstraction

### 📘 Concept:
Abstraction hides implementation details and shows only **essential information**. Implemented via **abstract classes** or **interfaces**.

### 🧩 Example:
```csharp
public abstract class Payment
{
    public abstract void Pay();
}

public class CreditCardPayment : Payment
{
    public override void Pay() => Console.WriteLine("Paid by Credit Card");
}
```

### 💬 Interview Q&A:
**Q:** What is abstraction?  
**A:** Hiding implementation and exposing only essential functionalities.

**Cross Q:**  
- When to use abstract class vs interface?  
  → Abstract: shared implementation, Interface: contract only.  
- Can we instantiate abstract classes? → No.

---

## 🔹 5. Interfaces vs Abstract Classes

| Feature | Abstract Class | Interface |
|----------|----------------|------------|
| Inheritance | Single | Multiple |
| Members | Can have implementation | Only declarations (C# 8+ default methods) |
| Fields | Yes | No |
| Access Modifiers | Can use | Public by default |
| Use When | Common base behavior | Common contract only |

### 🧩 Example:
```csharp
public interface ILogger { void Log(string message); }
public abstract class BaseLogger { public void LogTime() => Console.WriteLine(DateTime.Now); }
```

**Cross Q:**  
- Can interface have static methods? → Yes (C# 8+).  
- Can abstract class implement interface? → Yes, partially.

---

## 🔹 6. Method Overriding vs Hiding

### 📘 Concept:
- **Overriding:** Redefine base class method using `override`.
- **Hiding:** Use `new` to hide base method.

### 🧩 Example:
```csharp
class Base
{
    public virtual void Show() => Console.WriteLine("Base");
}

class Derived : Base
{
    public override void Show() => Console.WriteLine("Derived Override");
}
```

or  
```csharp
class Derived : Base
{
    public new void Show() => Console.WriteLine("Derived Hiding");
}
```

### 💬 Interview Q&A:
**Q:** Difference between override and new?  
**A:** `override` replaces base implementation (polymorphic), `new` hides it.

**Cross Q:**  
- If you call via base reference, which executes?  
  → Override → Derived method  
  → New → Base method

---

## 🔹 7. Dependency Injection (DI) & Loose Coupling

### 📘 Concept:
Dependency Injection (DI) removes hard-coded dependencies. Dependencies are **injected** externally (via constructor, property, or method).

### 🧩 Example:
```csharp
public interface IMessageService
{
    void Send(string msg);
}

public class EmailService : IMessageService
{
    public void Send(string msg) => Console.WriteLine($"Email: {msg}");
}

public class Notification
{
    private readonly IMessageService _service;

    public Notification(IMessageService service)
    {
        _service = service; // injected
    }

    public void Notify() => _service.Send("Hello Dependency Injection!");
}
```

### 💬 Interview Q&A:
**Q:** What is dependency injection?  
**A:** Providing required dependencies externally instead of creating them.

**Cross Q:**  
- How does DI improve testability? → Enables mocking dependencies.  
- Types of DI? → Constructor, property, method.

---

## 🔹 8. SOLID Principles

| Principle | Meaning | Example |
|------------|----------|----------|
| **S** | Single Responsibility | Each class has one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Derived classes replace base without breaking behavior |
| **I** | Interface Segregation | No fat interfaces |
| **D** | Dependency Inversion | Depend on abstractions, not concretions |

### 🧩 Example:
```csharp
public interface IPaymentService { void Pay(); }
public class PayPalPayment : IPaymentService { public void Pay() => Console.WriteLine("PayPal"); }

public class Checkout
{
    private readonly IPaymentService _payment;
    public Checkout(IPaymentService payment) => _payment = payment;
    public void Process() => _payment.Pay();
}
```

**Cross Q:**  
- Which SOLID principle does DI support? → Dependency Inversion.  
- How does SRP help? → Reduces coupling, easier maintenance.

---

## 🔹 9. Design Patterns (Common)

| Pattern | Type | Use Case | Example |
|----------|------|-----------|----------|
| **Singleton** | Creational | One instance globally | Logger |
| **Factory** | Creational | Creates objects without exposing logic | ShapeFactory |
| **Repository** | Structural | Abstracts DB logic | `UserRepository` |
| **Strategy** | Behavioral | Switch algorithms at runtime | Sorting algorithms |
| **Observer** | Behavioral | Notify multiple subscribers | Event-based systems |
| **CQRS** | Architectural | Separate read/write models | Command & Query segregation |

### 🧩 Example — Factory Pattern:
```csharp
public interface IShape { void Draw(); }
public class Circle : IShape { public void Draw() => Console.WriteLine("Circle"); }

public class ShapeFactory
{
    public static IShape GetShape(string type)
    {
        return type switch
        {
            "circle" => new Circle(),
            _ => throw new ArgumentException("Invalid type")
        };
    }
}
```

**Cross Q:**  
- Why use Factory over DI? → Factory decides runtime creation; DI is compile-time wiring.  
- Difference between Singleton and Static? → Singleton = one instance with state, static = no instance.

---

## 📊 Summary Table — Key Review Points

| Concept | Definition | Example | Key Differentiator |
|----------|-------------|----------|--------------------|
| Encapsulation | Hiding internal data | `private balance` | Data security |
| Inheritance | Reuse base class | `class Car : Vehicle` | Code reuse |
| Polymorphism | Same method, different behavior | `override Speak()` | Dynamic behavior |
| Abstraction | Hide complexity | `abstract class Payment` | Simplifies usage |
| Interface vs Abstract | Contract vs implementation | `ILogger`, `BaseLogger` | Interface = multiple inheritance |
| Overriding vs Hiding | Override changes, new hides | `override` / `new` | Polymorphic vs non-polymorphic |
| DI & Loose Coupling | Inject dependencies | Constructor injection | Testable & maintainable |
| SOLID | 5 design principles | SRP, OCP, DIP | Reduces coupling |
| Design Patterns | Reusable solutions | Factory, Singleton, CQRS | Standard design practices |

---

✅ **Key Differentiator for Interviews:**
Be ready to justify design choices like:
- “Why use Factory over DI?”
- “How did SOLID reduce code changes?”
- “When to use abstract class instead of interface?”
- “Why prefer DI for testing?”

---
