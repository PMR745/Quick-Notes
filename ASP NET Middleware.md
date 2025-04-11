# 🧱 Middleware in ASP.NET

Middleware in ASP.NET handles HTTP requests/responses in a pipeline. Each component can process, modify, or short-circuit the pipeline.

---

## 📝 1. What is Middleware?

- Middleware is software that's assembled into an app pipeline to handle requests and responses.
- Each middleware:
  - Receives an HTTP context.
  - Can perform operations before and after calling the next middleware.
  - Can terminate the pipeline (e.g., for errors or specific routes).

---

## 🧬 2. Middleware Pipeline Structure

- The pipeline is configured in the `Program.cs` file (in .NET 6+ with Minimal APIs).
- Middleware components are added in the order they're registered.

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.UseMiddleware1();
app.UseMiddleware2();
app.UseMiddleware3();

app.Run();
```

---

## 🔧 3. Types of Middleware

| Middleware             | Purpose                                      |
|------------------------|----------------------------------------------|
| `UseRouting()`         | Matches the request to endpoints              |
| `UseAuthentication()`  | Checks authentication credentials             |
| `UseAuthorization()`   | Checks user access permissions                |
| `UseStaticFiles()`     | Serves static files like CSS/JS/images        |
| `UseEndpoints()`       | Executes the matched endpoint                 |

---

## 🛠️ 4. Creating Custom Middleware

### Step 1: Create Middleware Class

```csharp
public class MyMiddleware
{
    private readonly RequestDelegate _next;

    public MyMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        // Before next middleware
        Console.WriteLine("Request incoming");

        await _next(context); // Call the next middleware

        // After next middleware
        Console.WriteLine("Response outgoing");
    }
}
```

### Step 2: Register in the Pipeline

```csharp
app.UseMiddleware<MyMiddleware>();
```

---

## ⚙️ 5. Use, Run, and Map Middleware

- `app.Use()` → Adds middleware and calls the next.
- `app.Run()` → Final middleware; doesn't call next.
- `app.Map()` → Conditionally branches the pipeline.

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Middleware 1");
    await next();
});

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello from Run Middleware");
});
```

---

## 🧪 6. Order of Middleware

Order matters! For example:

```csharp
app.UseStaticFiles();
app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
app.UseEndpoints(...);
```

Each middleware should be in the correct place or it can break functionality.

---

## 🕵️ 7. Built-in Middleware Examples

- `UseDeveloperExceptionPage()` - shows detailed error info in dev.
- `UseHttpsRedirection()` - redirects HTTP to HTTPS.
- `UseCors()` - handles Cross-Origin Resource Sharing.
- `UseSession()` - enables session state management.

---

## 📌 Summary

- Middleware runs in a pipeline and order matters.
- Use built-in and custom middleware for flexible request handling.
- Always register middleware properly in `Program.cs`.

