# 📘 ASP.NET Core Notes (Minimal API Style)

---

## 🏁 `Program.cs` (Entry Point)
- Configures services and middleware
- Sets up app pipeline: routing, endpoints, DB, auth, etc.

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
```

---

## 📤 File Upload & Download

### Upload Endpoint
```csharp
app.MapPost("/upload", async (IFormFile file) =>
{
    var path = Path.Combine("Uploads", file.FileName);
    using var stream = File.Create(path);
    await file.CopyToAsync(stream);
    return Results.Ok("Uploaded");
});
```

### Download Endpoint
```csharp
app.MapGet("/download/{filename}", async (string filename) =>
{
    var path = Path.Combine("Uploads", filename);
    return Results.File(path, "application/octet-stream", filename);
});
```

---

## 🔀 Middleware
- Code that runs between request & response
- Used for logging, auth, error handling, etc.

```csharp
app.Use(async (context, next) =>
{
    Console.WriteLine("Middleware triggered");
    await next(); // call next middleware
});
```

---

## 🧾 Data Annotations vs Validation
- **Data Annotations**: metadata on models (`[Required]`, `[MaxLength]`, etc.)
- **Validation**: checking if incoming data matches model constraints

```csharp
public class Book {
    [Required]
    [MaxLength(30)]
    public string Title { get; set; }
}
```

---

## 🔐 JWT Authentication

### Setup
```csharp
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", options => {
        options.TokenValidationParameters = new TokenValidationParameters {
            // Validation config
        };
    });

app.UseAuthentication();
app.UseAuthorization();
```

### Protect Endpoint
```csharp
app.MapGet("/secret", [Authorize] () => "Top Secret");
```

---

## 🧩 Service Lifetimes

| Type      | Lifetime Description                    |
|-----------|------------------------------------------|
| Singleton | One instance for entire app              |
| Scoped    | One instance per request                 |
| Transient | New instance every time it's requested   |

---

## 📋 Logging Best Practices

### When to use what:
| Log Level   | When to Use                              |
|-------------|------------------------------------------|
| Information | Successful events like file uploaded     |
| Warning     | Edge cases like empty file upload        |
| Error       | Exceptions like disk error or save fail  |

### Example:
```csharp
_logger.LogInformation("File uploaded: {FileName}", file.FileName);
_logger.LogWarning("Empty file uploaded");
_logger.LogError(ex, "Failed to save file");
```

---

## 🛡️ `[Authorize]` Attributes

```csharp
[Authorize]                 // Requires token
[Authorize(Roles = "Admin")] // Role-based protection
```

---
