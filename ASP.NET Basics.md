## 1. Introduction
- **ASP.NET**: Web framework by Microsoft
- **.NET Core vs .NET Framework**: Cross-platform vs Windows-only
- **MVC vs Web API vs Blazor**: Different approaches for web apps

## 2. Setup
- **Install .NET SDK**: `dotnet --version`
- **Create Project**: `dotnet new webapp -o MyApp`
- **Run**: `dotnet run`

## 3. Project Structure
- **Program.cs**: Entry point
- **Startup.cs**: Configure services & middleware
- **appsettings.json**: Configurations
- **Controllers/**: Handles requests
- **Views/**: UI templates (Razor)
- **Models/**: Data structures

## 4. Middleware
- **Definition**: Pipeline handling requests/responses
- **Common Middleware**: `UseRouting()`, `UseEndpoints()`, `UseAuthentication()`

## 5. Routing
- **Conventional Routing**: `app.UseEndpoints(endpoints => {...})`
- **Attribute Routing**: `[Route("api/[controller]")]`

## 6. Controllers & Actions
- **Controller**: `public class HomeController : Controller {}`
- **Action Methods**: `return View()`, `return Json()`, `return Redirect()`

## 7. Views & Razor
- **Razor Syntax**: `@Model.Property`, `@foreach`, `@if`
- **Layout Pages**: `_Layout.cshtml`
- **Partial Views**: `@Html.Partial("_MyPartial")`

## 8. Models & Data Binding
- **Models**: `public class User { public string Name { get; set; } }`
- **Data Binding**: `@model User`, `<input asp-for="Name" />`

## 9. Dependency Injection (DI)
- **Service Registration**: `builder.Services.AddScoped<IMyService, MyService>();`
- **Constructor Injection**: `public HomeController(IMyService service) {}`

## 10. Entity Framework Core (EF Core)
- **DB Context**: `public class AppDbContext : DbContext {}`
- **Migrations**: `dotnet ef migrations add InitialCreate`
- **CRUD Operations**: `context.Users.Add(user);`

## 11. Authentication & Authorization
- **Identity**: `builder.Services.AddIdentity<User, Role>()`
- **JWT Auth**: `AddAuthentication().AddJwtBearer()`
- **Authorize Attribute**: `[Authorize]`

## 12. API Development
- **RESTful Services**: `[HttpGet]`, `[HttpPost]`, `[HttpPut]`, `[HttpDelete]`
- **Swagger**: `builder.Services.AddSwaggerGen();`

## 13. Configuration & Logging
- **Config Files**: `appsettings.json`
- **Logging**: `ILogger<T>`

## 14. Deployment
- **Docker**: `FROM mcr.microsoft.com/dotnet/aspnet`
- **Hosting**: IIS, Azure, AWS, Linux

## 15. Unit Testing
- **Testing Frameworks**: xUnit, NUnit
- **Mocking**: Moq library

## 16. Performance Optimization
- **Caching**: `ResponseCache`, Redis
- **Compression**: `UseResponseCompression()`

## 17. SignalR (Real-time Communication)
- **Setup**: `app.UseEndpoints(endpoints => { endpoints.MapHub<MyHub>("/myhub"); })`

## 18. Blazor Basics
- **Blazor Server vs WebAssembly**
- **Components**: `.razor` files
- **Event Handling**: `@onclick="MyMethod"`

## 19. Background Services
- **Hosted Services**: `IHostedService`
- **Worker Services**: `BackgroundService`

## 20. Security Best Practices
- **Data Protection**: `DataProtectionProvider`
- **CORS**: `AddCors()`
- **CSRF**: Anti-forgery tokens `@Html.AntiForgeryToken()
