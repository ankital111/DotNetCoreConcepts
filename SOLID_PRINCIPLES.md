# SOLID Principles in C# (.NET 8)

SOLID is an acronym for five design principles that make your software **scalable, maintainable, testable, and reusable.**

| Letter | Principle                       | Key Idea                                           |
| :----: | :------------------------------ | :------------------------------------------------- |
|  **S** | Single Responsibility Principle | One class = One responsibility                     |
|  **O** | Open/Closed Principle           | Open for extension, closed for modification        |
|  **L** | Liskov Substitution Principle   | Derived classes must be replaceable for their base |
|  **I** | Interface Segregation Principle | Prefer small, specific interfaces                  |
|  **D** | Dependency Inversion Principle  | Depend on abstractions, not concrete classes       |

---

# 🧱 C# SOLID Principles (with Real Example)

## 🧠 What are SOLID Principles?

**SOLID** is a set of **5 design principles** in Object-Oriented Programming that make your code:
✅ More **maintainable**
✅ More **scalable**
✅ Easier to **test**
✅ Easier to **extend** without breaking old code

> **SOLID** = **S**ingle Responsibility, **O**pen-Closed, **L**iskov Substitution, **I**nterface Segregation, **D**ependency Inversion

---

# 🧩 Example Project: Notification System

Imagine a .NET Core **Notification Service** that can send:

* Email Notifications
* SMS Notifications
* WhatsApp Notifications

---

## **1️⃣ Single Responsibility Principle (SRP)**

**💡 Each class should have only one reason to change.**

### ❌ Wrong

```csharp
class NotificationService
{
    public void SendEmail() { /* ... */ }
    public void SendSMS() { /* ... */ }
    public void LogToDatabase() { /* ... */ }
}
```

> Problem: One class does **too many things** — sending notifications *and* logging.

### ✅ Correct

```csharp
class EmailService
{
    public void SendEmail() { /* Send Email */ }
}

class SMSService
{
    public void SendSMS() { /* Send SMS */ }
}

class Logger
{
    public void Log(string message) { /* Write to DB */ }
}
```

> ✔ Each class has **one job** — easier to test and maintain.

---

## **2️⃣ Open/Closed Principle (OCP)**

**💡 Classes should be open for extension, but closed for modification.**

### ❌ Wrong

```csharp
class NotificationService
{
    public void Send(string type)
    {
        if (type == "Email") { /* send email */ }
        else if (type == "SMS") { /* send SMS */ }
    }
}
```

> Problem: Adding WhatsApp means **modifying** this class.

### ✅ Correct

```csharp
interface INotification
{
    void Send();
}

class EmailNotification : INotification
{
    public void Send() => Console.WriteLine("Email Sent!");
}

class SMSNotification : INotification
{
    public void Send() => Console.WriteLine("SMS Sent!");
}

class NotificationService
{
    public void Notify(INotification notification)
    {
        notification.Send();
    }
}
```

> ✔ You can add a new notification type (e.g., WhatsApp) without changing existing code.

---

## **3️⃣ Liskov Substitution Principle (LSP)**

**💡 Subclasses should be replaceable for their parent class without breaking behavior.**

### ✅ Correct Example

```csharp
abstract class Bird
{
    public abstract void Fly();
}

class Sparrow : Bird
{
    public override void Fly() => Console.WriteLine("Sparrow flying!");
}
```

> ✔ Works fine — every subclass of `Bird` can **fly**.

### ❌ Wrong Example

```csharp
class Ostrich : Bird
{
    public override void Fly() => throw new Exception("Ostrich can’t fly!");
}
```

> ❌ Violates LSP — you can’t replace `Bird` with `Ostrich` safely.

### ✅ Fixed Version

```csharp
interface IFlyingBird { void Fly(); }
interface IBird { }

class Ostrich : IBird { }
class Sparrow : IBird, IFlyingBird { public void Fly() { } }
```

> ✔ Separate behaviors properly.

---

## **4️⃣ Interface Segregation Principle (ISP)**

**💡 Don’t force classes to implement methods they don’t use.**

### ❌ Wrong

```csharp
interface INotification
{
    void SendEmail();
    void SendSMS();
}
```

> Problem: What if a class only needs to send email?

### ✅ Correct

```csharp
interface IEmailNotification { void SendEmail(); }
interface ISMSNotification { void SendSMS(); }

class EmailService : IEmailNotification
{
    public void SendEmail() => Console.WriteLine("Email Sent!");
}
```

> ✔ Small, focused interfaces = more flexibility.

---

## **5️⃣ Dependency Inversion Principle (DIP)**

**💡 High-level modules should depend on abstractions, not on concrete classes.**

### ❌ Wrong

```csharp
class NotificationManager
{
    private EmailService _email = new EmailService();
    public void Send() => _email.SendEmail();
}
```

> Problem: `NotificationManager` is tightly coupled with `EmailService`.

### ✅ Correct (Using Abstraction)

```csharp
interface INotification
{
    void Send();
}

class EmailNotification : INotification
{
    public void Send() => Console.WriteLine("Email Sent!");
}

class NotificationManager
{
    private readonly INotification _notification;
    public NotificationManager(INotification notification)
    {
        _notification = notification;
    }

    public void Notify() => _notification.Send();
}
```

> ✔ Now you can inject any type (Email, SMS, WhatsApp) without changing the manager.

---

## 🧾 Key Takeaways

| Principle | Meaning                             | Real-Life Example                               |
| --------- | ----------------------------------- | ----------------------------------------------- |
| **S**     | One class = one job                 | Separate EmailService and Logger                |
| **O**     | Extend, don’t modify                | Add new notification types easily               |
| **L**     | Subclasses must behave like parents | Bird 🐦 example                                 |
| **I**     | Small, focused interfaces           | IEmail, ISMS instead of big interface           |
| **D**     | Depend on abstraction               | Use `INotification` not `EmailService` directly |

---

### 🧠 In Real Projects

In a real .NET Core app, these principles appear in:

* Controllers and Services separation (SRP)
* Interface-driven DI containers (DIP)
* Repository pattern (OCP + DIP)
* DTO and ViewModel separation (SRP)
* Abstraction of external APIs (OCP)

---

### 💡 Final Tip

> Following **SOLID** makes your app easier to refactor, test, and scale — especially in microservices or large enterprise projects.


## 1. Single Responsibility Principle (SRP)

> A class should have only one reason to change.

Each class or module should focus on one task.

### Wrong Example:

```csharp
public class EmployeeService
{
    public void AddEmployee(Employee emp)
    {
        // Save employee to database
    }

    public void GenerateReport()
    {
        // Also generate PDF report (not related)
    }
}
```

### Correct Example:

```csharp
public class EmployeeService
{
    private readonly IEmployeeRepository _repository;
    public EmployeeService(IEmployeeRepository repository)
    {
        _repository = repository;
    }

    public void AddEmployee(Employee emp)
    {
        _repository.AddAsync(emp);
    }
}

public class ReportService
{
    public void GenerateReport(List<Employee> employees)
    {
        // Logic for PDF or Excel report
    }
}
```

**In your project:**

* `EmployeeService` handles business logic
* `EmployeeRepository` handles database logic
* `ReportService` or `LoggingService` handle their own concern

---

## 2. Open/Closed Principle (OCP)

> Software entities should be open for extension, but closed for modification.

You should be able to add new features without modifying existing code.

### Wrong Example:

```csharp
public class SalaryCalculator
{
    public decimal CalculateBonus(Employee emp)
    {
        if (emp.Department == "HR") return emp.Salary * 0.10m;
        else if (emp.Department == "IT") return emp.Salary * 0.20m;
        return 0;
    }
}
```

### Correct Example:

```csharp
public interface IBonusCalculator
{
    decimal Calculate(Employee emp);
}

public class HRBonusCalculator : IBonusCalculator
{
    public decimal Calculate(Employee emp) => emp.Salary * 0.10m;
}

public class ITBonusCalculator : IBonusCalculator
{
    public decimal Calculate(Employee emp) => emp.Salary * 0.20m;
}
```

Adding a new department means adding a new class—not changing old code.

---

## 3. Liskov Substitution Principle (LSP)

> Derived classes must be substitutable for their base classes.

### Correct Example:

```csharp
public abstract class Employee
{
    public abstract decimal GetBonus();
}

public class PermanentEmployee : Employee
{
    public override decimal GetBonus() => 1000;
}

public class ContractEmployee : Employee
{
    public override decimal GetBonus() => 500;
}
```

If subclasses behave differently but still respect the base contract, LSP is followed.

---

## 4. Interface Segregation Principle (ISP)

> Clients should not be forced to depend on interfaces they do not use.

### Wrong Example:

```csharp
public interface IEmployeeOperations
{
    void AddEmployee();
    void GenerateReport();
    void SendEmail();
}
```

### Correct Example:

```csharp
public interface IEmployeeRepository
{
    void AddEmployee();
}

public interface IReportService
{
    void GenerateReport();
}

public interface INotificationService
{
    void SendEmail();
}
```

Separate small interfaces make the system more flexible.

---

## 5. Dependency Inversion Principle (DIP)

> High-level modules should not depend on low-level modules. Both should depend on abstractions.

### Wrong Example:

```csharp
public class EmployeeController
{
    private EmployeeRepository _repo = new EmployeeRepository(); // tightly coupled
}
```

### Correct Example:

```csharp
public class EmployeeController : ControllerBase
{
    private readonly IEmployeeRepository _repo;

    public EmployeeController(IEmployeeRepository repo)
    {
        _repo = repo; // abstraction injected
    }
}
```

**Dependency Injection setup:**

```csharp
builder.Services.AddScoped<IEmployeeRepository, EmployeeRepository>();
```

---

## Benefits of SOLID

| Principle | Benefit                                    |
| :-------- | :----------------------------------------- |
| **S**     | Each class easier to maintain              |
| **O**     | Add features without breaking old ones     |
| **L**     | Derived classes behave correctly           |
| **I**     | Interfaces small & focused                 |
| **D**     | Easily testable & replaceable dependencies |

---

## Tips

* **Why SOLID principles?** → Improve readability, maintainability, and scalability.
* **Which SOLID principle uses Dependency Injection?** → Dependency Inversion.
* **Difference between SRP and OCP?** → SRP is about *responsibility*, OCP is about *extensibility*.
* **Example of LSP violation?** → Subclass throws `NotImplementedException`.
* **Why use interfaces?** → Abstraction, loose coupling, flexibility.

---

These principles will make your .NET 8 project clean, extensible, and professional-grade.
