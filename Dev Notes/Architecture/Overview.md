**Architectural Patterns:**

- **RESTful API** - Resource-based endpoints using HTTP verbs
- **Minimal APIs** - Lightweight approach (.NET 6+)
- **CQRS** - Separate read/write operations
- **Clean Architecture** - Layered separation (Domain, Application, Infrastructure, Presentation)
- **Vertical Slice** - Feature-based organization instead of layers

**API-Specific Patterns:**

- **Repository Pattern** - Data access abstraction
- **Unit of Work** - Coordinate multiple repository operations
- **Mediator Pattern** - Decouple request/response handling (MediatR library)
- **API Gateway** - Single entry point for microservices
- **Backend for Frontend (BFF)** - Separate APIs per client type

**Implementation Patterns:**

- **Dependency Injection** - Built-in IoC container
- **Middleware Pipeline** - Request/response processing chain
- **Filters** - Cross-cutting concerns (authorization, validation, logging)
- **DTOs/ViewModels** - Separate internal models from API contracts
- **Result Pattern** - Structured error handling

**Common Combinations:**

- Clean Architecture + CQRS + MediatR
- Minimal APIs + Vertical Slice
- Traditional MVC Controllers + Repository + Unit of Work