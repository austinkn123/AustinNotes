## oop pillars

- Polymorphism
- encapsulation
- abstraction
- inheritance

## encapsulation:

- restricting methods and variables to a class

## Static classes

live in memory differently so a new instance is not needed and the method will not change

- Needed for easy access

cant put own code in interface

abstract = signature ( declaration) + body

- doesnt support multiple inheritance
- has constructors
- dont have to use all methods

interface = signature ( declaration )

- supports multiple inheritances
- no constructor
- have to use all methods

NEVER hardcode the access token

Created when configuring Program.cs

## MVC:

- **M**odels: Classes that represent the data of the app. The model classes use validation logic to enforce business rules for that data. Typically, model objects retrieve and store model state in a database.

- **V**iews: Views are the components that display the app's user interface (UI). Generally, this UI displays the model data.

- C

  ontrollers: Classes that:

  - Handle browser requests.
  - Retrieve model data.
  - Call view templates that return a response.

## HTTP endpoint:

- Is a targetable URL in the web application, such as `https://localhost:5001/HelloWorld`.
- Combines:
  - The protocol used: `HTTPS`.
  - The network location of the web server, including the TCP port: `localhost:5001`.
  - The target URI: `HelloWorld`.

## Model Binding:

Definition: maps the named parameters from the query string to parameters in the method

The model binding system:

- Retrieves data from various sources such as route data, form fields, and query strings.
- Provides the data to controllers and Razor pages in method parameters and public properties.
- Converts string data to .NET types.
- Updates properties of complex types.

https://localhost:7169/HelloWorld/Welcome**?**name=Rick**&**numtimes=4

- `?` (question mark) in the above URL is a separator, and the query string follows.
- The `&` character separates field-value pairs.

## IActionResult:

- Defines a contract that represents the result of an action method.

In Program.cs:

app.MapControllerRoute(

name: "default", pattern: "{controller=Home}/{action=Index}/{id?}");

- the `Movies` controller, the `Details` method, and an `id` value

## Unit testing:

- definition =
- Used to test code quality
  - write code that were independently testable
- tedious
- for controllers:
  - dont test endpoints
- cant unit test db access
- goal = less mocks and test cases
- backend = testing services NOT ENDPOINTS

code:

- solid
  - keep things modular
  - inherited classes can be used and seperated with diff calls

## defensive programming:

- be prepared for errors
- try catch is still good
  - exceptions are good
- testing
  - validation
  - if statements over try/catch

constraints = need both constraints and if statements



## microservices



## SOLID Principles:

- Single-responsibility principle

   = there should never be more than one reason for a class to change.

  - In other words, **a class should have only one primary responsibility**. If a class contains methods that change different models or have multiple distinct purposes, it can become harder to understand, maintain, and modify.

- Open–closed principle

   = software entities should be open for extension but closed for modification.

  - designing software components (e.g., classes, modules, functions) in a way that allows them to be extended or enhanced to accommodate new functionality without requiring changes to their existing source code

- **Liskov substitution principle** = An inherited class should not try to change the members of its parent class, or the way it behaves. The principle is being violated if one of the child class members throws an exception.

- **Interface segregation principle** = when a class implements an interface where it requires all its members

- Dependency inversion principle

   = high-level classes should not depend on low-level classes

  - High-level modules (e.g., abstractions, interfaces) should not depend on low-level modules (e.g., concrete implementations).
  - Both high-level and low-level modules should depend on abstractions (e.g., interfaces, abstract classes).