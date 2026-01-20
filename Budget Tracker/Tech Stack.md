
### Backend Stack

#### Core Framework

- **ASP.NET Core Web API** - .NET 9 
    - Why: Modern, fast, cross-platform, great tooling

### Database

- **SQL Server** - LocalDB or Docker container
    - Why: Free for dev, integrates well with .NET, good for learning
    - Alternative: PostgreSQL if you prefer open-source

### Data Access

- **Dapper** - Lightweight ORM
    - `Dapper` (core package)
    - `Microsoft.Data.SqlClient` (SQL Server driver)
    - Why: Fast, gives you SQL control, less magic than EF Core


### Authentication

- **JWT Bearer Tokens**
    - `Microsoft.AspNetCore.Authentication.JwtBearer`
    - `System.IdentityModel.Tokens.Jwt`
- **BCrypt.Net-Next** - Password hashing
    - Why: Industry standard, stateless auth for SPAs

### Validation

- **FluentValidation**
    - `FluentValidation.AspNetCore`
    - Why: Clean, testable validation rules

### Configuration

- **Built-in .NET Configuration** (appsettings.json)
- **User Secrets** for local dev (API keys, connection strings)

---

## Frontend Stack

### Core Framework

- **React 18** with **TypeScript**
    - Why: Type safety, better DX, industry standard

### Project Setup

- **Vite** (recommended) or Create React App
    - Why: Vite is faster, modern, better DX
    - Command: `npm create vite@latest expense-tracker-ui -- --template react-ts`

### Routing

- **React Router v6**
    - `react-router-dom`
    - Why: Standard routing solution, v6 is clean API

### State Management 

- **React Query (TanStack Query v5)**
    - `@tanstack/react-query`
    - Why: Perfect for server state (API calls, caching, refetching)
- **React Context + useState** for UI state (theme, modals)
    - Why: Built-in, sufficient for simple UI state

### HTTP Client

- **Axios**
    - Why: Interceptors for auth tokens, better error handling than fetch
    - Alternative: Native `fetch` if you want minimal dependencies

### Forms

- **React Hook Form**
    - `react-hook-form`
    - Why: Performant, less re-renders, good TypeScript support
    - Alternative: Formik (more verbose but also popular)

### Styling

- **Tailwind CSS**
    - Why: Fast development, utility-first, no CSS files to manage
    - Setup: PostCSS + Tailwind plugin

### UI Components (Optional)

- **Headless UI** or **Radix UI** (for modals, dropdowns)
    - Why: Accessible, unstyled components that work with Tailwind
    - Alternative: Build from scratch for learning

### Charts

- **Recharts**
    - Why: React-native, composable, good for simple charts
    - Alternative: Chart.js with react-chartjs-2 (more features)

### Date Handling

- **date-fns**
    - Why: Lightweight, tree-shakeable, functional
    - Alternative: Day.js (smaller) or Luxon (more features)

### Icons

- **Lucide React** or **React Icons**
    - Why: Large icon library, tree-shakeable


### Architecture:
- **Server Side:** 
	- Repository Method
		- Why: Industry standard; most easily integrated with a react frontend
	- **Middleware:**
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
	- Dependency Injection:
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