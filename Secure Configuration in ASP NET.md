# 🔐 Secure Configuration in ASP.NET Core

Securely managing configuration is crucial for protecting sensitive data like API keys, connection strings, and secret tokens.

---

## ✅ 1. Use `appsettings.json` for Non-Sensitive Defaults

```json
{
  "AppSettings": {
    "ApiBaseUrl": "https://example.com/api",
    "PageSize": 10
  }
}
```

---

## 🔐 2. Keep Secrets Out of Source Control

### 🔧 a. User Secrets (Dev Only)

```bash
dotnet user-secrets init
dotnet user-secrets set "JwtSettings:SecretKey" "your-super-secret-key"
```

Access with:

```csharp
builder.Configuration["JwtSettings:SecretKey"]
```

✅ Not checked into Git!

---

### 🌍 b. Environment Variables (Preferred in Prod)

```bash
export JwtSettings__SecretKey=your-super-secret-key
```

> `:` in keys becomes `__` in env vars.

Access with:

```csharp
builder.Configuration["JwtSettings:SecretKey"]
```

---

## 🧩 3. Use Strongly-Typed Configuration

### Define a config class:

```csharp
public class JwtSettings
{
    public string SecretKey { get; set; }
    public int ExpiryMinutes { get; set; }
}
```

### Register in Program.cs:

```csharp
builder.Services.Configure<JwtSettings>(
    builder.Configuration.GetSection("JwtSettings"));
```

### Use via DI:

```csharp
public class AuthService(IOptions<JwtSettings> jwtOptions)
{
    private readonly JwtSettings _settings = jwtOptions.Value;
}
```

---

## 🚫 Avoid Common Pitfalls

- ❌ Never store secrets in `appsettings.json`
- ✅ Use `.gitignore` to exclude `secrets.json`
- ✅ Use **User Secrets** for development
- ✅ Use **Environment Variables** or **Secret Managers** for production
- ✅ Only log what's needed in production

---

## 🛡️ Summary Table

| Source                    | Use Case                  | Secure? |
|---------------------------|---------------------------|---------|
| `appsettings.json`        | Non-sensitive config       | ❌      |
| `appsettings.{env}.json`  | Env-specific overrides     | ❌      |
| User Secrets              | Dev-only secrets           | ✅      |
| Environment Variables     | Prod secrets               | ✅✅     |
| Key Vault / Secret Manager| Enterprise-grade security  | ✅✅✅   |

---

## 🔐 Pro Tips

- Use `IOptionsSnapshot` or `IOptionsMonitor` to read updated config at runtime.
- Use `dotnet user-secrets list` to view local secrets.
- Use [ASP.NET Data Protection](https://learn.microsoft.com/en-us/aspnet/core/security/data-protection/introduction) APIs to encrypt data at rest.
- Don't forget to validate configuration on startup using `builder.Services.AddOptions<JwtSettings>().Validate(...)`.

---
