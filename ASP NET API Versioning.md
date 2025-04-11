# API Versioning in ASP.NET Core - Quick Guide

## 1. Install Packages

```bash
dotnet add package Microsoft.AspNetCore.Mvc.Versioning
dotnet add package Microsoft.AspNetCore.Mvc.Versioning.ApiExplorer
```

## 2. Configure Services

```csharp
// Program.cs
builder.Services.AddApiVersioning(options =>
{
    options.DefaultApiVersion = new ApiVersion(1, 0);
    options.AssumeDefaultVersionWhenUnspecified = true;
    options.ReportApiVersions = true;
    options.ApiVersionReader = ApiVersionReader.Combine(
        new QueryStringApiVersionReader("api-version"),
        new HeaderApiVersionReader("X-Api-Version"),
        new MediaTypeApiVersionReader("ver")
    );
});

builder.Services.AddVersionedApiExplorer(options =>
{
    options.GroupNameFormat = "'v'VVV";
    options.SubstituteApiVersionInUrl = true;
});
```

## 3. Create Versioned Controllers

```csharp
// V1 Controller
[ApiController]
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/products")]
public class ProductsV1Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Products V1");
}

// V2 Controller
[ApiController]
[ApiVersion("2.0")]
[Route("api/v{version:apiVersion}/products")]
public class ProductsV2Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get() => Ok("Products V2");
}
```

## 4. Access API Versions

- **URL Path**: `/api/v1/products` or `/api/v2/products`
- **Query String**: `/api/products?api-version=1.0`
- **Header**: `X-Api-Version: 1.0`
- **Media Type**: `Content-Type: application/json;ver=1.0`

## 5. Deprecate Old Versions (Optional)

```csharp
[ApiVersion("1.0", Deprecated = true)]
```
