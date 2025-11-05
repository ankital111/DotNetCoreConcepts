# ✅ Middleware in C# (ASP.NET Core) — Complete Guide

## 🌱 1. What is Middleware?

Middleware is a component in the ASP.NET Core request pipeline that handles HTTP requests and responses. Each middleware can:
- Process the incoming request
- Modify the request or response
- Pass the control to the next middleware
- Or **stop** the pipeline

Think of middleware as links in a chain.

---

## 🧠 Analogy

When you go to a restaurant:
- The **waiter (middleware)** takes your request.
- Passes it to **kitchen (next middleware)**.
- Then returns the output (response).

Each person can decide to:
- Forward the request
- Or stop (e.g., “restaurant closed”)

---

## 🧱 Middleware Pipeline Example (Program.cs)

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();

app.Use(async (context, next) =>
{
    Console.WriteLine("Before Request");
    await next.Invoke();
    Console.WriteLine("After Request");
});

app.MapControllers();
app.Run();
```

---

## 🧑‍💻 Creating a Custom Middleware

### Step 1 — Create Middleware Class

```csharp
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");
        await _next(context);
        Console.WriteLine($"Response: {context.Response.StatusCode}");
    }
}
```

### Step 2 — Extension Method

```csharp
public static class MiddlewareExtensions
{
    public static IApplicationBuilder UseLoggingMiddleware(this IApplicationBuilder app)
    {
        return app.UseMiddleware<LoggingMiddleware>();
    }
}
```

### Step 3 — Register Middleware

```csharp
app.UseLoggingMiddleware();
```

---

## ⛔ Short-Circuiting the Pipeline

```csharp
app.Use(async (context, next) =>
{
    if (!context.Request.Headers.ContainsKey("Authorization"))
    {
        context.Response.StatusCode = 401;
        await context.Response.WriteAsync("Unauthorized!");
        return;
    }
    await next();
});
```

If `next()` is **not called**, remaining middlewares don’t run.

---

## 📌 Built-in Middleware Examples

| Middleware | Purpose |
|-----------|---------|
| `UseRouting()` | Matches route |
| `UseAuthentication()` | Authenticates user |
| `UseAuthorization()` | Checks user roles/permissions |
| `UseStaticFiles()` | Serve CSS, JS, Images |
| `UseExceptionHandler()` | Global error handler |

---

## 🔥 Difference Between `Use`, `Run`, and `Map`

| Method | Description | Calls Next Middleware? |
|--------|-------------|------------------------|
| `Use()` | Adds middleware | ✅ Yes |
| `Run()` | Terminal middleware | ❌ No |
| `Map()` | Creates branch pipeline | Conditional |

```csharp
app.Map("/admin", adminApp =>
{
    adminApp.Run(async context =>
    {
        await context.Response.WriteAsync("Admin Section");
    });
});
```

---

# 🎯 Interview Questions & Answers

### Q1. What is Middleware?
**Answer:** A component in the request pipeline that processes requests and responses.

**Cross Question:** What if middleware does not call `next()`?  
**Answer:** The pipeline stops.

---

### Q2. How do you create custom middleware?
**Answer:** Create a class with `InvokeAsync`, register it using `UseMiddleware`.

**Cross Question:** Can DI be used in middleware?  
**Answer:** Yes, via parameters in `InvokeAsync`.

---

### Q3. Why does middleware order matter?
**Answer:** Because each middleware may depend on the work of the previous one.

**Cross Question:** What happens if authorization comes before authentication?  
**Answer:** Authorization fails.

---

### Q4. Difference between Middleware and Filters?
| Middleware | Filters |
|-----------|---------|
| Works before MVC pipeline | Works inside MVC pipeline |
| Works on all requests | Works at controller/action level |

---

## 🧭 Summary

| Concept | Key Point |
|--------|-----------|
| Middleware | Handles HTTP pipeline |
| Order | Very important |
| Use() | Passes control |
| Run() | Ends pipeline |
| Map() | Branches the pipeline |

---

✨ You now understand Middleware clearly!
