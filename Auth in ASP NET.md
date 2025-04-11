# 🔐 Authentication & Authorization in ASP.NET

Authentication and Authorization are key components for securing web applications in ASP.NET.

---

## 🧾 1. Definitions

- **Authentication**: Who are you?
  - Verifies the identity of the user (e.g., via tokens, cookies).
- **Authorization**: What are you allowed to do?
  - Grants access to resources based on roles, policies, claims, etc.

---

## 🧱 2. Middleware for Auth

Order is crucial in the middleware pipeline.

```csharp
app.UseAuthentication();
app.UseAuthorization();
```

Place `UseAuthentication` before `UseAuthorization`.

---

## 🔐 3. JWT Authentication Setup

### Step 1: Add NuGet Package

```
Microsoft.AspNetCore.Authentication.JwtBearer
```

### Step 2: Configure in `Program.cs`

```csharp
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = "your-app",
            ValidAudience = "your-app",
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("your-secret-key"))
        };
    });

builder.Services.AddAuthorization();
```

### Step 3: Use Middleware

```csharp
app.UseAuthentication();
app.UseAuthorization();
```

---

## 🛡️ 4. Protecting Endpoints

### Option 1: Require Auth Globally

```csharp
app.MapControllers().RequireAuthorization();
```

### Option 2: Use `[Authorize]` Attribute

```csharp
[Authorize]
[HttpGet("secure-data")]
public IActionResult GetSecureData()
{
    return Ok("Only for authenticated users");
}
```

### Option 3: Allow Anonymous

```csharp
[AllowAnonymous]
[HttpGet("public")]
public IActionResult GetPublicData()
{
    return Ok("Accessible to all");
}
```

---

## 🧑‍🤝‍🧑 5. Role-Based Authorization

### Assign Role in Token

Include a role claim in your JWT:
```json
{
  "sub": "user1",
  "role": "admin"
}
```

### Use Role in Controller

```csharp
[Authorize(Roles = "admin")]
public IActionResult AdminOnly()
{
    return Ok("Hello Admin!");
}
```

---

## 🧩 6. Policy-Based Authorization

### Step 1: Define Policy

```csharp
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AdminOnly", policy =>
        policy.RequireRole("admin"));
});
```

### Step 2: Use Policy

```csharp
[Authorize(Policy = "AdminOnly")]
public IActionResult PolicyProtected()
{
    return Ok("Access granted by policy");
}
```

---

## 🧠 7. Custom Claims & Requirements

You can write custom requirements and handlers to perform complex logic.

### Example: Custom Requirement

```csharp
public class MinimumAgeRequirement : IAuthorizationRequirement
{
    public int MinimumAge { get; }
    public MinimumAgeRequirement(int age) => MinimumAge = age;
}
```

### Handler

```csharp
public class MinimumAgeHandler : AuthorizationHandler<MinimumAgeRequirement>
{
    protected override Task HandleRequirementAsync(
        AuthorizationHandlerContext context,
        MinimumAgeRequirement requirement)
    {
        var dobClaim = context.User.FindFirst(c => c.Type == "DateOfBirth");
        if (dobClaim != null &&
            DateTime.TryParse(dobClaim.Value, out var dob) &&
            DateTime.Today.Year - dob.Year >= requirement.MinimumAge)
        {
            context.Succeed(requirement);
        }

        return Task.CompletedTask;
    }
}
```

### Register Services

```csharp
builder.Services.AddSingleton<IAuthorizationHandler, MinimumAgeHandler>();

builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("AtLeast18", policy =>
        policy.Requirements.Add(new MinimumAgeRequirement(18)));
});
```

---

## 📌 Summary

- **Authentication**: Validates user identity (e.g., JWT, cookies).
- **Authorization**: Grants access to resources based on identity/roles/policies.
- Use `[Authorize]`, `[AllowAnonymous]`, and role/policy attributes.
- Place `UseAuthentication()` before `UseAuthorization()` in the middleware pipeline.

