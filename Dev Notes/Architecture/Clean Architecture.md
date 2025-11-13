# Clean Architecture:

## Definition: 

- software architecture aimed at building applications that we can maintain, scale, and test easily
  - separating the application into different layers that have distinct responsibilities

## Layers: (Inner to outer )

- ### Domain 

  - Contains application entitles and specifications. This is the deepest layer and don't have any external dependencies in this layer
    - Side Note: Can possibly contain business rules / logic

- ### Application

  - Contains the business rules / logic and only points to the Domain layer
    - Side Note: Can also have some of the business rules / logic in the Domain layer and the Application layer is the only way to reach that code

- ### Infrastructure

  - Contains external services such as databases, file storage, emails, etc
    - Ex: Can contain the implementations of the interfaces defined in the Domain layer

- ### Presentation (UI / DB / External Systems)

  - API layer that contains user interaction and fetching data to UI
    - https requests

## Advantages:

- The domain and application layer are always the center of the design and are known as the core of the system that why the core of the system is not dependent on external systems.
  - This architecture allows you to change the external system without affecting the core of the system.
- Highly Testable
  - since this architecture is so modular, testing becomes easier in this situation
- Highly scalable
  - can change the performance of the app based on which layer you choose

## Disadvantages:

- increased complexity / abstraction
  - can be a extra steep learning curve
- Setting up Dependency Injection can get a little tricky in this architecture because of where it might be called in the layers