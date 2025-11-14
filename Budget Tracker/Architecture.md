### Server Side:
#### Repository Method
- Why: Industry standard; most easily integrated with a react frontend
##### BudgetTracker.Core (The Innermost Layer)
- Purpose: This is the heart of your application. It contains the fundamental building blocks that are shared across all other projects.
- Contents:
	- Domain Models/Entities: Plain C# objects (POCOs) that represent the core concepts of your application, like User, Category, and Expense. These classes directly map to your database tables.
- Dependencies: This project has no dependencies on any other project in your solution. It is completely independent.
##### BudgetTracker.Application (The Logic Layer)
- Purpose: This layer defines the business logic and use cases. It orchestrates the flow of data using the core models but doesn't know how the data is stored or retrieved.
- Contents:
	- Interfaces: It contains the contracts for your repositories and services (e.g., IExpenseRepository). These interfaces define what the application should do (like "get all expenses"), but not how it should be done.
- Dependencies: It depends only on the Core project to use the domain models. It does not depend on Infrastructure.
##### BudgetTracker.Infrastructure (The Outermost Layer)
- Purpose: This layer is responsible for the technical implementation details. It handles all communication with external systems like databases, APIs, or the file system.
- Contents:
	- Repository Implementations: Concrete classes that implement the interfaces from the Application layer (e.g., ExpenseRepository). This is where you write your Dapper or Entity Framework code.
	- Data Context: Classes like your DapperContext that manage database connections.
- Dependencies: It depends on the Application project (to implement its interfaces) and external libraries like Dapper and Microsoft.Data.SqlClient.
#### Middleware:
- Purposes:
	- Request/response logging (HTTP level)
	- Authentication, CORS, compression
	- Global error handling
	- Rate limiting??
	- Middleware execution order is critical - they must be placed strategically with exception handling first, authentication before authorization, and static files before dynamic processing
	- Middleware should focus on a single responsibility and avoid heavy computations or long-running tasks
	- Middleware should not contain long-running tasks - offload to background services or use async processing instead
	- Keep middleware stack lean - each component has a performance cost, so avoid unnecessary components
	- Global exception handling middleware should catch unhandled exceptions and return standardized error responses. ASP.NET Core has built-in UseExceptionHandler middleware
#### Dependency Injection:
- - **Scrutor Decorators for:**
	- Validation, caching, transaction management per handler
	- Business operation logging (what command/query ran)
	- Authorization checks on specific operations
- Extension methods
- Scrutor
- Apply Decorators


```
var builder = WebApplication.CreateBuilder(args);

// 1. Use extension methods for organization
builder.Services
    .AddDataLayer(builder.Configuration)
    .AddApplicationLayer();

// 2. Use Scrutor for assembly scanning
builder.Services.Scan(scan => scan
    .FromCallingAssembly()
    .AddClasses(c => c.AssignableTo<IRepository>())
    .AsImplementedInterfaces()
    .WithScopedLifetime());

// 3. Apply decorators for cross-cutting concerns
if (builder.Configuration.GetValue<bool>("Features:EnableCaching")) {
    builder.Services.Decorate(typeof(IRepository<>), typeof(CachedRepository<>));
}

builder.Services.Decorate(typeof(IRepository<>), typeof(LoggingRepository<>));
```

- **Site (Frontend):**
	- 